# Jack in the Box — Firmware-Images

Signierte OTA-Images für ein privates Bastelprojekt: eine ESP32-C3-Box, die auf
Zuruf einen federgespannten Deckel aufspringen lässt und dazu einen Sound
abspielt.

**Hier liegen nur fertige Binaries.** Der Quellcode ist nicht öffentlich.
Dieses Repo existiert aus genau einem Grund: das Gerät steht hinter einem
fremden Router und muss sich seine Updates selbst abholen können — dafür
braucht es eine öffentlich erreichbare URL ohne Zugangsdaten. Ein Token in der
Firmware wäre ein Geheimnis auf einem Gerät, das anderswo steht.

## Inhalt

| Datei | Zweck |
|---|---|
| `manifest.json` | Was aktuell angeboten wird: Version, Pfad, Größe, SHA256, Signatur |
| `firmware-<version>.bin` | Das Image selbst |

```json
{
  "version": "0.5.0",
  "path":    "/Tomboy77/jack-in-the-box-firmware/main/firmware-0.5.0.bin",
  "size":    1069056,
  "sha256":  "…",
  "sig":     "…",
  "notes":   "…"
}
```

`path` ist bewusst nur ein Pfad, kein vollständiger Link: der Host ist in der
Firmware einkompiliert. Ein manipuliertes Manifest kann das Gerät damit nicht
auf einen anderen Server umlenken.

## Wie ein Update abläuft

1. Das Gerät holt `manifest.json` und vergleicht die Version mit seiner eigenen.
2. Es lädt das Image in den App-Slot, aus dem es gerade *nicht* läuft, und
   rechnet dabei den SHA256 mit.
3. Es prüft Prüfsumme **und** ECDSA-P256-Signatur. Erst wenn beide stimmen,
   schaltet es den Bootslot um.
4. Nach dem Neustart läuft die neue Firmware auf Bewährung: meldet sie sich
   nicht binnen weniger Minuten als funktionsfähig, fällt das Gerät von selbst
   auf die vorherige Version zurück.

Ein abgebrochener Download, eine falsche Prüfsumme oder eine ungültige Signatur
ändern am laufenden Gerät nichts — der Bootslot wird in diesen Fällen gar nicht
erst umgeschaltet.

## Signatur selbst prüfen

Der öffentliche Schlüssel steckt in der Firmware; der private liegt offline.
Ohne ihn lässt sich kein Image erzeugen, das ein Gerät annimmt.

```bash
python3 - <<'EOF'
import base64, hashlib, json
m = json.load(open("manifest.json"))
img = open("firmware-%s.bin" % m["version"], "rb").read()
print("Größe :", "ok" if len(img) == m["size"] else "ABWEICHUNG")
print("SHA256:", "ok" if hashlib.sha256(img).hexdigest() == m["sha256"] else "ABWEICHUNG")
EOF
```

Gegen den öffentlichen Schlüssel (`ota_pub.pem`, unten):

```bash
base64 -d <<< "$(python3 -c 'import json;print(json.load(open("manifest.json"))["sig"])')" > sig.der
openssl dgst -sha256 -verify ota_pub.pem -signature sig.der firmware-0.5.0.bin
```

## Öffentlicher Schlüssel

```
-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAENwIsckZLmqJWTO8CV4Bd6sQslEvJ
nASo8/SunCjbKSuxeOO4yO3iaEXoGwuTFnXn9BhJzcUUEtmCT/zDiVNS+Q==
-----END PUBLIC KEY-----
```

## Hinweis

Die Images sind auf genau eine Hardware zugeschnitten (ESP32-C3 SuperMini mit
festgelegter Beschaltung) und enthalten keine Zugangsdaten — ein fremdes Gerät,
das sie aufspielt, wäre funktionsfähig, aber ohne Konfiguration nutzlos.
Für Dritte ist hier also nichts zu holen; das Repo ist öffentlich, weil OTA
ohne öffentliche URL nicht funktioniert, nicht als Veröffentlichung.
