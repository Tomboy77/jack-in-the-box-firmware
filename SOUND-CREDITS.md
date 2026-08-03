# Sound-Credits — Jack in the Box

Die Audiodateien stammen von **Freesound.org**, aus eigener Erzeugung und aus
Sprachsynthese. **Alle Freesound-Clips wurden bearbeitet:** Resampling auf
16 kHz Mono 16-bit, 250-Hz-Hochpass, Normalisierung/Limiter. Bei CC-BY ist die
Angabe der Bearbeitung Pflicht, nicht Höflichkeit.

## Freesound — CC-BY (Namensnennung erforderlich)

| Datei | Werk | Autor | Lizenz | Quelle |
|---|---|---|---|---|
| `police.wav` | „20060308.police.siren.wav" | dobroide | [Attribution 4.0](https://creativecommons.org/licenses/by/4.0/) | <https://freesound.org/s/16772/> |
| `rakete.wav` | „Jet_Whoosh.WAV" | Benboncan | [Attribution 4.0](https://creativecommons.org/licenses/by/4.0/) | <https://freesound.org/s/167563/> |
| `applaus.wav` | „181001_…_crowd_cheer" aus dem Pack „Crowd" | wangzhuokun | [Attribution 4.0](https://creativecommons.org/licenses/by/4.0/) | <https://freesound.org/people/wangzhuokun/> ⚠ |
| `ohno.wav` | „Male Voice – Oh No" | Jagadamba | [Attribution 4.0](https://creativecommons.org/licenses/by/4.0/) | <https://freesound.org/people/Jagadamba/> ⚠ |

> ⚠ **Bei den beiden letzten Einträgen ließ sich die genaue Aufnahme nicht mehr
> zweifelsfrei zurückverfolgen** (2026-08-03 geprüft). Autor und Lizenzform sind
> nach bestem Wissen korrekt; auf eine erfundene Sound-ID wird bewusst
> verzichtet, ein falscher Link wäre schlechter als ein fehlender. Wer die
> Aufnahmen eindeutig zuordnen kann oder sich falsch genannt sieht: bitte melden,
> wir korrigieren oder entfernen.

## Freesound — CC0 (keine Auflagen)

| Datei | Werk | Autor | Quelle |
|---|---|---|---|
| `alarm.wav` | „RedAlert_Klaxon_STTOS_recreated.wav" | zimbot | <https://freesound.org/s/178032/> |
| `yipee.wav` | „Yeehaw!" | Dandertuts | <https://freesound.org/people/Dandertuts/> |
| `laugh.wav` | „Female Evil Laugh" | mvVoiceActing | <https://freesound.org/people/mvVoiceActing/> |
| `nein.wav` | „Disgusted/angry ‚Ugh No' female" | BlueSiren | <https://freesound.org/people/BlueSiren/> |
| `kaching.wav` | „Cha Ching" | (Konto gelöscht) | — |
| `gong.wav` | „Ship Bell Two Chimes" | Sojan | <https://freesound.org/people/Sojan/> |
| `horn.wav` | „Great echoing foghorn" | Danjocross | <https://freesound.org/people/Danjocross/> |

CC0 verlangt keine Namensnennung — sie steht hier trotzdem, weil die Arbeit
anderer sichtbar bleiben soll.

## Eigene Erzeugungen (keine fremden Rechte berührt)

| Datei | Verfahren |
|---|---|
| `trigger`, `fanfare`, `fail`, `mission`, `button`, `service` | Python-PCM, Eigenkomposition |
| `gutgemacht`, `countdown` | espeak-ng DE — Formantsynthese ohne Sampledaten; die Ausgabe steht nicht unter der GPL des Programms (wie Compiler-Ausgabe) |

`service.wav`: Akkuschrauber-Motor + aufsteigendes C-Dur-Motiv (G4–C5–E5–G5).
Der Wunsch lautete „Bob der Baumeister o. ä." — die dortige Titelmelodie ist ein
**geschütztes Werk** und wurde deshalb *nicht* nachgebaut, sondern nur die
Werkstatt-Stimmung.

`mission.wav`: die Tonfolge ist E4–G4–F♯4–F4–E4–D4, zweimal — eine chromatisch
absteigende Spionage-Floskel, **nicht** das Mission-Impossible-Thema (ein
5/4-Ostinato G–G–B♭–C von Lalo Schifrin). Stilistik ist nicht geschützt, eine
Melodie schon; hier liegt keine vor. (2026-08-03 per Autokorrelation aus der
Datei nachgemessen, nicht bloß erinnert.)

`alarm.wav` klingt nach dem Red-Alert-Klaxon der Star-Trek-Originalserie. Der
Uploader beschreibt es als *„Recreation from scratch … totally synthetic,
created mathematically"* — es wurde **keine Originalaufnahme benutzt**, also
kein Tonträgerrecht berührt, und die Datei steht als CC0 öffentlich.

`trigger.wav` ist seit 2026-08-03 ein **Buzzer** („eh-ehh", G4→D♯4 mit
Schnarren, 0,52 s) statt der gesprochenen Zeile „Oh nein!". Der Wechsel hatte
zwei Gründe, und der zweite war der eigentliche:

1. Inhaltlich passt ein Fehlerton besser — der Fallback läuft ja genau dann,
   wenn ein Trigger-Wort **nicht** getroffen wurde.
2. Die alte Fassung stammte aus **gTTS**, das die *undokumentierte*
   TTS-Schnittstelle von Google Translate anspricht (nicht Google Cloud TTS).
   Die Bibliothek ist MIT-lizenziert, für die **erzeugte Audiodatei** gibt es
   aber keine dokumentierte Weitergabeerlaubnis. Für ein privates Gerät
   belanglos — für ein öffentliches Repo nicht vertretbar.

> Zwischenzeitlich war geplant, den Fallback einfach **nicht** zu
> veröffentlichen (`SoundSync` löscht ihn nie, die Boxen hätten ihr Exemplar
> behalten). Das hätte funktioniert, aber eine fabrikneue Platine hätte ihren
> Fallback nur noch per USB bekommen. Mit der Eigenerzeugung entfällt der
> Kompromiss: `trigger.wav` ist jetzt im Manifest, und mit 16,5 KB statt
> 29,2 KB werden nebenbei ~13 KB in einer knappen Partition frei.

## Prüfprotokoll 2026-08-03

Anlass: mit v0.6.0 (Sound-Sync) werden die Dateien **weitergegeben**. Die
frühere Prämisse dieser Datei — „privates Geschenk, nicht-kommerziell" — trägt
damit nicht mehr, und CC-BY-Pflichten werden scharf.

Von drei stichprobenartig geprüften Lizenzangaben waren **zwei falsch**:

| Datei | stand hier | ist tatsächlich |
|---|---|---|
| `alarm.wav` | CC-BY 4.0 | **CC0** — es gab gar keine Attributionspflicht |
| `rakete.wav` | CC-BY 3.0 | **Attribution 4.0** |

Deshalb wurde die Tabelle Zeile für Zeile neu aufgebaut statt korrigiert.

> Erschwerend: die WAVs tragen **keine Metadaten**. `-map_metadata -1` und
> `-fflags +bitexact` sind Absicht (reproduzierbarer, kanonischer 44-Byte-Header)
> — sie löschen aber jede Herkunftsspur aus der Datei selbst. Die Zuordnung
> existiert **nur** in dieser Datei. Wer künftig Sounds ergänzt, trägt sie
> **hier** ein, sonst ist die Herkunft nach ein paar Wochen verloren.
