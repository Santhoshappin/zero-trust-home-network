# Security checklist (template)

Copy this and tick items off for your own home.

## Router
- [ ] Admin password changed from factory default (stored in a password manager)
- [ ] Firmware current / auto-update on
- [ ] WPS off
- [ ] UPnP / NAT-PMP off
- [ ] Remote / WAN management off (or confirmed ISP-only)
- [ ] No DMZ, no unneeded port forwards (IPv4 **and** IPv6)
- [ ] Firewall drops unknown inbound; IPv6 pinhole table empty; WAN ping replies off
- [ ] Home Wi-Fi: WPA2/WPA3, 16+ character random passphrase, neutral SSID
- [ ] Work Wi-Fi (guest): own SSID + passphrase, own subnet, client isolation on **and tested**

## Work devices
- [ ] Connected to the work Wi-Fi only; home SSID forgotten
- [ ] Corporate VPN for all work traffic
- [ ] OS and endpoint protection up to date (managed by employer IT)
- [ ] Not used for personal browsing, games or media servers

## Home devices
- [ ] Personal laptop: network profile **Public**, firewall on, full AV scan, disk encryption
- [ ] Printer: Wi-Fi Direct / Wireless Direct **off**, firmware updated
- [ ] Cameras: firmware updated, account MFA on, RTSP / local streaming accounts off unless needed
- [ ] Robot vacuum and other IoT: firmware updated, account MFA on
- [ ] TV / streaming boxes: auto-updates on, no sideloaded or unknown apps
- [ ] Phones/tablets: OS updated; private Wi-Fi MAC address on
- [ ] Every cloud account behind a device (Google, Apple, camera, vacuum…): unique password + MFA
- [ ] No unused services running (media servers, file shares, remote desktop)

> The LastPass breach started with an old, unpatched media server on an engineer's home PC. Anything running at home that is reachable from the network needs patching or removing.
