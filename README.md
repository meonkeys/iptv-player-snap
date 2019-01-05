# adam-player: fork of ogra1/omxplayer-snap

This is source code for creating a [snap](https://en.wikipedia.org/wiki/Snappy_(package_manager)) to loop videos on a raspberry pi 3 B+ with Ubuntu Core installed.

This is a derivative work of [ogra1/omxplayer-snap](https://github.com/ogra1/omxplayer-snap).

This is mostly a proof of concept to kick the tires on Ubuntu Core. If you are looking for a simple plug-and-play raspberry pi video looper, check out <https://learn.adafruit.com/raspberry-pi-video-looper/>.

## How to create an ubuntu core raspberry pi video looper

1. install ubuntu core 18
    1. [prep SD card](https://www.ubuntu.com/download/iot/installation-media)
    1. [run first-boot setup](https://www.ubuntu.com/download/iot/raspberry-pi-2-3)
1. change `/boot/uboot/config.txt` (as instructed in `snap info omxplayer-pi`)
    1. comment `dtoverlay=vc4-kms-v3d`
    1. reboot
1. build [customized video looper](https://github.com/meonkeys/iptv-player-snap)
    1. [set up dev env on raspberry pi](https://developer.ubuntu.com/core/get-started/developer-setup) 
    1. copy [customized video looper](https://github.com/meonkeys/iptv-player-snap) onto raspberry pi
    1. start the build and grab a cuppa (takes ~30min)
1. `sudo snap install --devmode adam-player_0.1_armhf.snap`
1. `sudo snap stop adam-player`
1. give permissions for the video looper to read files in `$HOME`
    1. `snap interfaces` shows that `adam-player` wants access to the `home` plug
    1. run: `snap connect adam-player:home :home` to grant access
1. copy a video to `$HOME` dir
1. `sudo vi /var/snap/adam-player/current/channel`
    1. file should contain one line with the full path to the video in your `$HOME` dir
1. `sudo snap start adam-player`

Video should play automatically on boot.

## links to learn more

* <https://tutorials.ubuntu.com/tutorial/create-your-first-snap>
* <https://developer.ubuntu.com/core/get-started/developer-setup>
* [snapcraft forum](https://forum.snapcraft.io)
* [snap for omxplayer](https://github.com/meonkeys/omxplayer-snap)
* [example omxplayer IPTV snap](https://github.com/meonkeys/iptv-player-snap)
* [my original question on askubuntu](https://askubuntu.com/questions/1106478/auto-play-and-keep-omxplayer-pi-running-on-ubuntu-core-18)
* <https://docs.snapcraft.io/configuration-in-snaps/510>
* [sample video](https://commons.wikimedia.org/w/index.php?title=File%3ACuriosity%27s_Seven_Minutes_of_Terror.ogv)
* <https://forum.snapcraft.io/t/what-is-the-canonical-way-to-find-a-snaps-source-code-and-build-scripts/9298>

# Copyleft and License

* Copyright ©2019 Adam Monsen &lt;haircut@gmail.com&gt;
* License: AGPL v3 or later (see COPYING)

All upstream code uses upstream licensing. See individual source files for details.
