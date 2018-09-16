# gst-conan
This is a tool for building [Gstreamer](https://gstreamer.freedesktop.org/) components as [Conan](https://conan.io/) packages
using the [Meson](https://mesonbuild.com/) build system via [gst-build](https://github.com/GStreamer/gst-build).

This tool is expected to work on the same platforms as [gst-build](https://github.com/GStreamer/gst-build), so most Linux
distros are covered (we guess).

First time users should look at the [machine setup instructions](#machine-setup-instructions).

## Usage
Read all about it.

```bash
git clone https://github.com/Panopto/gst-conan
cd gst-conan
./gst-conan --help
```

For example, create several conan packages for Gstreamer `1.14.2` like this.

```bash
./gst-conan create --rev 1.14.2 --version 1.14.2 --user my_user_name --channel my_channel
```

## Why does this tool exist?
It would be great if you could just map one Meson project into one Conan package, but there is a parent Meson project 
(under [gst-build](https://github.com/GStreamer/gst-build)) which is required to tie all the Meson projects together.
Some of the projects will not build without the parent project.

So ... this tool builds everything in one shot using [gst-build](https://github.com/GStreamer/gst-build) and then it
creates the Conan packages.

## Contributions are welcome
Your pull requests are welcome.

## Machine setup instructions

Below are instructions which cover the distros that we have tried.

### Ubuntu 18.04, Mint 19 (and maybe Debian)
There are two steps to get `gst-conan` working on your machine. 

#### 1. Edit `~/.bashrc`
Put this at the bottom of the file.

```bash
# This is where pip3 installs `--user` executables (such as meson)
PATH=$PATH:$HOME/.local/bin
```

Restart your terminal or execute `source ~/.bashrc`.

#### 2. Install stuff
```bash
sudo apt update
sudo apt install --yes git python-pip python3-pip ninja-build build-essential libmount-dev libselinux-dev gobject-introspection libglib2.0-dev libgirepository1.0-dev libxml2-dev libavfilter-dev
pip3 install setuptools wheel
pip3 install --user meson
pip3 install conan
```

## Legal disclaimer
The contents of this repo are licensed under [LGPL](license).

We (the maintainers of this repository) are not responsible for accurately representing the licensing status of third
party components (Gstreamer or otherwise).  If **you** use these scripts to build anything, then **you** are responsible
for doing **your own** research about legal restrictions regarding the components being built.

We believe that most of Gstreamer is under an LGPL license of some kind, but we aren't 100% sure.

Gstreamer may have components which are legally restrictive (not covered by LGPL).  For example, many
components of [gst-plugins-ugly](https://github.com/GStreamer/gst-plugins-ugly) are especially restrictive.

Gstreamer may also depend on third party components which are legally restrictive in some way (we haven't checked).

We encourage users to do their own research into legal matters.