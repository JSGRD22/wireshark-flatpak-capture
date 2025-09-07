# wireshark-flatpak-capture
**wireshark-flatpak-capture** is a simple bash script to allow the wireshark flatpak to capture packets via `tcpdump`.

> [!NOTE]
> This script is no longer maintained as I have found a better solution for this problem. Simply create a rootful distrobox and export wireshark, then editing the .desktop file's exec line to `Exec=pkexec env DISPLAY=$DISPLAY XAUTHORITY=$XAUTHORITY DBX_SUDO_PROGRAM="pkexec" /usr/bin/distrobox-enter --root -n [INSERT DISTROBOX NAME] -- wireshark %f`. (The default one does not work properly) This runs Wireshark as root in distrobox and provides access to not only network capture but also USB capture and other features.

I use an atomic linux distribution, which means the root directories are not easily modified. Additionally, layering wireshark via `rpm-ostree` has its own [issues](https://github.com/fedora-silverblue/issue-tracker/issues/50). Based on this [suggestion](https://discussion.fedoraproject.org/t/silverblue-wireshark-does-not-see-network-interfaces/88916/9), I wrote a simple script to use `tcpdump` to capture the packages and pipe the output to wireshark.

## Prerequisites
- [tcpdump](https://www.tcpdump.org/)
- [Wireshark flatpak](https://flathub.org/apps/org.wireshark.Wireshark)

## Installation
Copy `wireshark-capture` into `~/.local/bin` or any directory in PATH. Run `chmod +x wireshark-capture`. You're set!

## Usage
Simply run `wireshark-capture` in your terminal. The script will provide a list of available network interfaces. Choose the one you wish to monitor. Your system will then prompt you to authenticate with password or biometrics. Upon authenticating, the capture process will begin.
