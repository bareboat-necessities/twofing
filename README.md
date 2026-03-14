# twogfing

twofing is a daemon which runs in the background and recognizes two-finger gestures performed on a touchscreen and converts them into mouse and keyboard events. This way, such gestures can be used in almost all existing applications (even ones where you wouldn’t expect it, like Wine applications) without having to modify them.

# Installation

## Install from GitHub APT repository (Debian Trixie)

For tagged releases (`v*`), CI publishes:

- architecture-specific `.deb` packages
- a flat APT repository (`Packages`, `Packages.gz`, `Release`)

You can consume the stable flat repository from the `apt` release tag:

```bash
echo "deb [trusted=yes] https://github.com/twofing/twofing/releases/download/apt ./" | \
  sudo tee /etc/apt/sources.list.d/twofing-github.list

sudo apt-get update
sudo apt-get install twofing
```

> Note: the published repository is currently unsigned, so `trusted=yes` is required.

## Build from source

```
sudo apt-get install \
  build-essential \
  libx11-dev \
  libxtst-dev \
  libxi-dev \
  x11proto-randr-dev \
  libxrandr-dev \
  xserver-xorg-input-evdev \
  xserver-xorg-input-evdev-dev
make
sudo make install
```

Create a x11 conf file and att the following section to it

```
Section "InputClass"
  Identifier "calibration"
  Driver "evdev"
  MatchProduct "{{ put your device name here, get it with xinput list }}"

  Option "EmulateThirdButton" "1"
  Option "EmulateThirdButtonTimeout" "750"
  Option "EmulateThirdButtonMoveThreshold" "30"
EndSection
```
## Special install script for Argonaut M7
An install script for the Argonaut M7 (courtesy of Mikhail Grushinskiy) can be found here: https://github.com/bareboat-necessities/my-bareboat/blob/master/twofing/rpi_twofing_install.sh
