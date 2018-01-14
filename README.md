# brusa-amc-unix

This repository allows you to connect to and monitor Solectria/Brusa AMC motor controllers (AMC 230, AMC 320, AMC 325, etc) that 
are used in many older electric vehicles.

It contains both `AMC_E.exe` (for configuration) and `MONLOG_E.exe` (for live monitoring). Both are MS-DOS applications and can be run in DOSBox.

## Serial Connection

You will most likely need a serial adapter (see compatibility note) and you will need an [AMC RS422 to RS232 adapter](http://www.wolftronix.com/amc_adapter/index.html). The adapter link explains how to connect to the controller's internal serial port with the adapter.

On Unix based computers (macOS, Linux, etc), serial devices appear in `/dev/` for example `/dev/tty.usbserial-AL00K7J4`. Because this
changes from computer to computer, `launch.sh` will search for a serial device automatically and will write it to the config file.

This script does not officially support Windows and Windows manages serial ports in a slightly different way. In Windows, serial ports are labeled `COM1`, `COM2`, etc. This script will not look for devices however it is very simple to hardcode the serial device in launch.sh.


## Configuration

This repo contains a template config and `launch.sh` will replace certain special template "variables" with computed values when it runs. If you need to make changes to the DOSBox config, they can be made in `amc-dosbox.conf`. The changes will be reflected in the generated config file.

## Serial Adapter Compatibility

Wolftronix has [tested](https://www.youtube.com/watch?v=DD5D5CqYThc&index=6&list=PLQdu_G7xyFIQz7z3yqhWUcRPp7SVei3qV) multiple adapters when connecting through DOSBox on Windows 10 and only one of the 3+ that he has tested work. There is a good chance that adapters compatible with macOS are compatible with Linux and possibly other *nixes as well.

| Adapter | Windows 10 | macOS | Linux | Native MS-DOS compat. |
|---------|------------|-------|-------|-------|
| CH340   | ✖          | ?     | ?     | ✖     |
| Prolific PL2030 | ✖  | ?     | ?     | ✔     |
| FTDI D2XX | ✔        | ?     | ?     | ✔     |
| Utek UT-980 | ?      | ✔     | ?     | ?     |

Windows versions that are 32bit have native MS-DOS compatibility (XP, 32bit Vista, etc) can run `AMC_E.exe` and `MONLOG_E.exe` directly. 
Windows 10 and any x64 copies of Windows must use DOSBox or another emulator. This is a [hardware limitation](https://www.xylos.com/blog/en/2012/04/legacy-16-bit-applications-on-64-bit-operating-systems/) with x86.

Adapters not listed have not been tested and have unknown compatibility.

