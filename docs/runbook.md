# Runbook: segment a home network for remote work

Works with most ISP routers that have a guest Wi-Fi. Takes about 1–2 hours. Never store passwords in documents; keep them in a password manager.

## 0. Inventory first
List every device: name, wired or Wi-Fi, MAC address, the app/account that controls it. Do a ping sweep (see [verification.md](verification.md)) and look at the router's device list. Identify every unknown device before you change anything. *In my case one "unknown" device was the printer, which was also running its own Wi-Fi hotspot.*

## 1. Router access
Find the model and admin login on the sticker. Log in at the gateway IP (often `192.168.1.1` or `192.168.0.1`). **Change the admin password** and save it in the password manager.

## 2. Update
Check that the firmware is current or set to auto-update. (ISP routers are often updated by the ISP, so check the version anyway.)

## 3. Harden the router
- WPS **off** (the PIN/push-button pairing is a known weakness)
- UPnP / NAT-PMP **off** (re-enable only if something genuinely needs it)
- Remote/WAN admin **off** where the ISP allows it
- No DMZ, delete port forwards nobody needs
- Firewall: block unknown inbound for **IPv4 and IPv6**. Check that the IPv6 pinhole table is empty. Turn off ping replies from the internet

## 4. Main (home) Wi-Fi
- A new SSID that doesn't reveal names or the address
- Passphrase: **16+ random characters**
- Security: WPA2/WPA3 mixed (use WPA3-only if every device supports it)
- Changing the password means every IoT device must rejoin through its app, so plan time for that

## 5. Work Wi-Fi (the guest network)
- Enable it with a different SSID and passphrase, WPA2/WPA3
- Turn **client/AP isolation ON**. If the UI has no switch, don't assume; **test it** (step 8)
- Check that it gets its own subnet, separate from the home network

## 6. Join devices by zone
- **Work laptops join the work Wi-Fi only**, then *forget* the home SSID so they can't drift back
- Everything else stays on the home Wi-Fi
- Corporate VPN on for all work traffic

## 7. Harden devices
Follow [security-checklist.md](security-checklist.md): firmware, MFA on every cloud account, turn off side channels (Wi-Fi Direct, RTSP, unused services), personal laptop on the *Public* network profile.

## 8. Verify (don't trust, test)
Run the tests in [verification.md](verification.md). The work laptops must be invisible from the home zone, and the home zone must be unreachable from the work zone.

## Moving house
Photograph the router settings pages (not the passwords) before the move. On the new router, repeat steps 1–8. Reusing the same SSIDs and passphrases makes devices reconnect automatically.
