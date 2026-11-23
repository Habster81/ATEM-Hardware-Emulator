# Habster ATEM Hardware Emulator

<img src="ATEM-Hardware-Emulator/icon.png" alt="Habster ATEM Hardware Emulator" width="128">

Plane ein ATEM-Constellation-Setup in **ATEM Software Control**, bevor ein physischer Mischer zur Verfügung steht. Der Emulator stellt auf demselben Windows-PC ein auswählbares Mischermodell bereit. Damit kannst du prüfen, welche Eingänge, Keyer, SuperSource- und Multiview-Optionen das jeweilige Modell für deinen Aufbau bietet.

[Windows-Installer und Handbuch](https://www.habster.ch/ATEM-Hardware-Emulator/) · [English overview](#english-overview)

## Schnellstart

**Voraussetzungen:** Windows 11 x64 und Blackmagic ATEM Switchers aus der 10.2-Reihe. Der Verbindungsaufbau und die Modellkennung wurden mit dem Blackmagic SDK 10.2.1 getestet.

1. Installiere und öffne den **Habster ATEM Hardware Emulator**. Beim ersten Start ist der **ATEM 2 M/E Constellation HD** ausgewählt.
2. Öffne **ATEM Software Control** auf demselben PC. Wähle **File → Connection → Manual IP Address**.
3. Gib `127.0.0.1` ein und klicke auf **Connect**.
4. Für einen Modellwechsel im Emulator **Stoppen**, ein anderes Modell wählen und **Starten**. Verbinde dich danach erneut in ATEM Software Control.

<img src="ATEM-Hardware-Emulator/manual/main-de.png" alt="Emulatorfenster mit ausgewähltem Modell und der Verbindungsadresse 127.0.0.1" width="425">

In den **Einstellungen** kannst du zwischen Deutsch und Englisch wechseln, den Windows-Autostart und den Betrieb im Infobereich aktivieren oder manuell und beim Programmstart nach Updates suchen.

## Unterstützte Modelle

| Modell | SDI-Eingänge | Aux-Ausgänge | Upstream-Keyer | DSK | SuperSource |
| --- | ---: | ---: | ---: | ---: | ---: |
| 1 M/E Constellation HD / 4K | 10 | 6 | 4 | 1 | 0 |
| 2 M/E Constellation HD / 4K | 20 | 12 | 8 | 2 | 1 |
| 4 M/E Constellation HD / 4K | 40 | 24 | 16 | 4 | 2 |
| Constellation 8K im HD-Modus | 40 | 24 | 16 | 4 | 2 |

Die App stellt einen modellspezifischen Startzustand bereit. Änderungen und Videoformatwechsel in ATEM Software Control werden noch nicht übernommen oder gespeichert. Die 4K- und 8K-Modelle starten im HD-Modus. Die Einstellungsseiten sind noch nicht vollständig geprüft.

Der **4K Plus** liegt als Entwicklungsprofil vor. Beim Synchronisieren mit dem SDK tritt ein Fehler auf, weshalb das Profil in Version 0.4.0 noch nicht zur Auswahl steht. Die **Constellation-IP-Modelle** benötigen eigene Profile für ATEM Switchers 11.0.

## Selbst bauen und weiterentwickeln

Der Windows-Build verwendet **Qt 6 mit passendem MinGW-Kit**, **CMake**, **Ninja** und **Inno Setup 7**. Führe im Projektverzeichnis den folgenden Befehl aus.

```powershell
.\packaging\build.cmd
```

Abweichende Installationspfade lassen sich mit `-Qt`, `-MinGW` und `-Inno` angeben. Der Build legt den Installer, die Versionshinweise, das Quellcode-ZIP und das SHA-256-Manifest unter `ATEM-Hardware-Emulator/releases/<Version>/` ab.

- [main.cpp](main.cpp) enthält die Qt-Oberfläche und den lokalen ATEM-UDP-Server.
- [profiles/](profiles/) enthält die Geräteprofile. Mit `node profiles/generate-profiles.mjs` kannst du die abgeleiteten Profile neu erzeugen. Für den normalen Windows-Build genügt der vorhandene Profilsatz.
- [packaging/](packaging/) enthält den Windows-Build und die Paketierung.
- [ATEM-Hardware-Emulator/](ATEM-Hardware-Emulator/) enthält die zweisprachige Downloadseite und das Handbuch.

Pull Requests für neue oder korrigierte Profile sind willkommen. Gib bei Fehlerberichten bitte die Version von ATEM Software Control, das gewählte Mischermodell und die Schritte an, mit denen sich das Problem nachstellen lässt.

### Downloadseite betreiben

Stelle `ATEM-Hardware-Emulator/` auf einem PHP-Webserver bereit. Der PHP-Prozess benötigt Schreibrechte in `releases/` für den Downloadzähler. Lade bei einer neuen Version zuerst den neuen Release-Ordner hoch und ersetze dann `latest.json` im Webroot. Frühere Installer können im Archiv verbleiben. Die Seite verlinkt das Quellcode-ZIP der neuesten Version. GitHub kann den Quellstand und Release-Dateien verwalten. Der PHP-Downloadzähler läuft auf dem PHP-Webserver.

## Lizenz

Der Quellstand steht unter der [MIT-Lizenz](LICENSE). Die vorgefertigte Windows-Ausgabe enthält die [deutsche](packaging/LICENSE.de.txt) und [englische Installationsvereinbarung](packaging/LICENSE.txt).

## English overview

Habster ATEM Hardware Emulator presents a local Constellation switcher profile so you can explore ATEM Software Control and plan a setup before the hardware is available. Run the emulator on Windows 11 x64, then connect from ATEM Software Control on the same PC using **File → Connection → Manual IP Address** and `127.0.0.1`.

Version 0.4.0 includes seven selectable SDI profiles for Blackmagic ATEM Switchers 10.2. Connectivity and model identification were tested with SDK 10.2.1. The emulator provides a starting state for planning. Switcher changes and video format changes are not applied or saved.

Run `packaging\build.cmd` with an existing Qt 6 MinGW kit, CMake, Ninja and Inno Setup 7 to build the installer and source archive. The source is available under the [MIT License](LICENSE). [English user manual](https://www.habster.ch/ATEM-Hardware-Emulator/?tab=manual&lang=en)
