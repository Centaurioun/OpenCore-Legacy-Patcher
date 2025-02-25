# Build and run from source

OpenCore Legacy Patcher at its core is a python-based TUI/CLI based application. This means that to run the project from source, you simply need to invoke the OpenCore-Patcher.command file via Python.

For developers wishing to validate mainline changes, you may use these nightly links:

* [GUI (Graphical Based App)](https://nightly.link/dortania/OpenCore-Legacy-Patcher/workflows/build-app-wxpython/main/OpenCore-Patcher.app%20%28GUI%29.zip)
* [TUI (Text Based App)](https://nightly.link/dortania/OpenCore-Legacy-Patcher/workflows/build-app/main/OpenCore-Patcher-TUI.app.zip)

**Warning**: These binaries should not be used without first consulting the [CHANGELOG](./CHANGELOG.md). Do not distribute these links in forums, instead direct to this file.

* Users running new builds of the project without understanding what has changed are at higher of bricking their installation as they do not read any warnings provided in the CHANGELOG. We wish to minimize these situations as much as possible.

## Getting Started

To start, ensure you have python 3.6 or newer installed. Additionally ensure that they were downloaded from the Official source, [python.org](https://www.python.org/downloads/macos/).

* Python installations either preinstalled or provided with Xcode/Xcode Tools are unsupported due to reliablility issues

Once Python is installed, open Terminal and run the following:

```sh
# Move into a directory to store the project
cd ~/Developer
# Clone project
git clone https://github.com/dortania/OpenCore-Legacy-Patcher
# Move into Project directory
cd ./OpenCore-Legacy-Patcher
# Install Python dependacies used by the project
pip3 install -r requirements.txt
```

## Running OpenCore Legacy Patcher

To run the project from source, simply invoke via python3:

```sh
# Launch TUI
python3 OpenCore-Patcher.command
```

```sh
# Launch GUI
python3 OpenCore-Patcher-GUI.command
```

Note that the OpenCore-Patcher.command file can be run as both a TUI and a CLI utility for other programs to call. If no core arguments are passed, the TUI is initialized. Otherwise the CLI will start:

```sh
# Launch CLI
python3 OpenCore-Patcher.command --build --model iMac12,2 --verbose
```

See `-h`/`--help` for more information on supported CLI arguments.

## Generating prebuilt binaries

The main goal of generating prebuilt binaries is to strip the requirement of a local python installation for users. For developers, there's very little benefit besides enabling dark mode support in the GUI. For development, simply use the OpenCore-Patcher.command file with a python3 installation.

* Note that due to PyInstaller's linking mechanism, binaries generated on Catalina and newer are not compatible with High Sierra and older
  * To ensure the largest compatibility, generate binaries on macOS Mojave. These binaries will be compatible with macOS 10.9 to macOS 12.
  * Currently our build system is a [Macmini8,1 provided by MacStadium](https://www.macstadium.com/opensource) running macOS Mojave (10.14.6).

```sh
# Install PyInstaller
pip3 install pyinstaller
# Move into project directory
cd ~/Developer/OpenCore-Legacy-Patcher/
# Create the pyinstaller based Application (replace OpenCore-Patcher.spec with OpenCore-Patcher-GUI.spec for GUI binary)
pyinstaller OpenCore-Patcher.spec
# Post PyInstaller clean up (only for the TUI)
./after_pyinstaller.sh
# Open build folder
open ./dist/
```

Once done, you'll find the application generated at `./dist/OpenCore-Patcher.app`:

![](./images/build-dist.png)