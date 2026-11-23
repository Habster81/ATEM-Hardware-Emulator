# Habster ATEM Hardware Emulator

<img src="icon.png" alt="ATEM Hardware Emulator" width="128">

Plan an ATEM Constellation setup in **ATEM Software Control** before a physical switcher is available. The emulator provides a selectable switcher model on the same Windows PC, so you can explore the inputs, keyers, SuperSource and Multiview options for your planned setup.

[Windows installer and manual](https://www.habster.ch/ATEM-Hardware-Emulator/?lang=en) · [Deutsch](#deutsch)

## Quick start

**Requirements:** Windows 11 x64 and Blackmagic ATEM Switchers 10.2. Connection and model identification were tested with the Blackmagic SDK 10.2.1.

1. Install and launch **Habster ATEM Hardware Emulator**. The **ATEM 2 M/E Constellation HD** is selected on first launch.
2. Open **ATEM Software Control** on the same PC. Choose **File → Connection → Manual IP Address**.
3. Enter `127.0.0.1` and click **Connect**.
4. To switch models, click **Stop**, select another model and click **Start**. Then reconnect in ATEM Software Control.


In **Settings**, you can switch between English and German, enable Windows startup and system tray operation, or check for updates manually or on launch.

## Supported models

| Model | SDI inputs | Aux outputs | Upstream keyers | DSKs | SuperSource |
| --- | ---: | ---: | ---: | ---: | ---: |
| 1 M/E Constellation HD / 4K | 10 | 6 | 4 | 1 | 0 |
| 2 M/E Constellation HD / 4K | 20 | 12 | 8 | 2 | 1 |
| 4 M/E Constellation HD / 4K | 40 | 24 | 16 | 4 | 2 |
| Constellation 8K in HD mode | 40 | 24 | 16 | 4 | 2 |

The emulator provides a model-specific starting state. It does not apply or save switcher changes or video format changes. The 4K and 8K models start in HD mode. Testing of the settings pages in ATEM Software Control is still incomplete.

The **4K Plus** development profile fails SDK synchronization and is unavailable in the version 0.4.0 model selector. The **Constellation IP** models need profiles for ATEM Switchers 11.0.

## Build and contribute

The Windows build uses **Qt 6 with a matching MinGW kit**, **CMake**, **Ninja** and **Inno Setup 7**. Run this command from the project directory.

```powershell
.\packaging\build.cmd
```

Use `-Qt`, `-MinGW` and `-Inno` to specify custom tool paths. The build writes the installer, release notes, source ZIP and SHA-256 manifest to `ATEM-Hardware-Emulator/releases/<Version>/`.

- [main.cpp](main.cpp) contains the Qt interface and local ATEM UDP server.
- [profiles/](profiles/) contains the device profiles. Run `node profiles/generate-profiles.mjs` to regenerate the derived profiles. The standard Windows build uses the included profiles.
- [packaging/](packaging/) contains the Windows build and packaging files.

Pull requests for new or corrected profiles are welcome. For bug reports, include your ATEM Software Control version, the selected switcher model and the steps to reproduce the issue.

## License

The source code is available under the [MIT License](LICENSE). The prebuilt Windows release includes separate [English](packaging/LICENSE.txt) and [German](packaging/LICENSE.de.txt) installer agreements.

## Deutsch

Der **Habster ATEM Hardware Emulator** stellt auf einem Windows-11-PC einen virtuellen ATEM Constellation bereit. Damit kannst du in **ATEM Software Control** einen Aufbau vorbereiten und die Bedienelemente von sieben Mischermodellen erkunden, bevor die Hardware verfügbar ist.

Emulator starten und auf demselben PC in ATEM Software Control unter **File → Connection → Manual IP Address** mit `127.0.0.1` verbinden. Die Profile sind für ATEM Switchers 10.2 vorgesehen. Änderungen am virtuellen Mischer werden nicht gespeichert.

[Windows-Installer](https://www.habster.ch/ATEM-Hardware-Emulator/?lang=de) · [Deutsches Handbuch](https://www.habster.ch/ATEM-Hardware-Emulator/?tab=manual&lang=de) · [MIT-Lizenz](LICENSE)

