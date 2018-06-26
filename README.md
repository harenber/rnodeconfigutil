# RNode Configuration Utility

## Intro

Configure, flash, backup and upgrade your RNode with this handy utility. The only required option is the serial port the device is attached to. To show basic device info, use the -i option.

RNode can operate in two modes, host-controlled (default) and TNC mode:

- When RNode is in host-controlled mode, it will stay in standby when powered on, until the host specifies frequency, bandwidth, transmit power and other required parameters. This mode can be enabled by using the -N option of this utility.

- When RNode is in TNC mode, it will configure itself on powerup and enable the radio immediately. This mode can be enabled by using the -T option of this utility (the utility will guide you through the settings if you don't specify them directly).

For a complete description of RNodes capabilities, documentation and more, please refer to the [RNode repository](https://github.com/markqvist/RNode_Firmware).

```
usage: rnodeconf.py [-h] [-i] [-T] [-N] [-b] [-d] [-f] [-r] [-u] [-k] [-p]
                    [--model model] [--hwrev revision] [--freq Hz] [--bw Hz]
                    [--txp dBm] [--sf factor] [--cr rate]
                    [port]

RNode Configuration and firmware utility. This program allows you to change
various settings and startup modes of RNode. It can also flash and update the
firmware, and manage device EEPROM.

positional arguments:
  port              serial port where RNode is attached

optional arguments:
  -h, --help        show this help message and exit
  -i, --info        Show device info
  -T, --tnc         Switch device to TNC mode
  -N, --normal      Switch device to normal mode
  -b, --backup      Backup EEPROM to file
  -d, --dump        Dump EEPROM to console
  -f, --flash       Flash firmware and bootstrap EEPROM
  -r, --rom         Bootstrap EEPROM without flashing firmware
  -u, --update      Update firmware
  -k, --key         Generate a new signing key and exit
  -p, --public      Display public part of signing key
  --model model     Model code for EEPROM bootstrap
  --hwrev revision  Hardware revision EEPROM bootstrap
  --freq Hz         Frequency in Hz for TNC mode
  --bw Hz           Bandwidth in Hz for TNC mode
  --txp dBm         TX power in dBm for TNC mode
  --sf factor       Spreading factor for TNC mode
  --cr rate         Coding rate for TNC mode
```

## Dependencies

The config utility requires Python 2.7, pyserial and cryptography.io. To install:

```
sudo apt install python python-pip
sudo pip install pyserial cryptography
```

## Installation

Just clone or download this repository, place wherever you'd like and run rnodeconf (remember to set executable permissions):

```
git clone https://github.com/markqvist/rnodeconfigutil.git
cd rnodeconfigutil
chmod a+x rnodeconf
./rnodeconf --help
```

## Examples

### Show device info

Print info like serial number, hardware revision, model and firmware version.

```
./rnodeconf /dev/ttyUSB0 -I
```

### Set RNode to TNC mode

If you just specify the -T option, the utility will ask you for the necessary parameters.

```
./rnodeconf /dev/ttyUSB0 -T
```

You can also specify all the options on the command line.

```
./rnodeconf /dev/ttyuUSB0 -T --freq 868000000 --bw 125000 --txp 2 --sf 7 --cr 5
```

### Set RNode to host-controlled mode

Use the -N option to set the device to host-controlled mode.

```
./rnodeconf /dev/ttyUSB0 -N
```
