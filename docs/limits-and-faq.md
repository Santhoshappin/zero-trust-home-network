# Limits and FAQ

## What segmentation does NOT protect against

Network segmentation stops a hacked TV, camera or vacuum from reaching your work laptop *over the home network*. It's one layer, not the whole defence. It does **not** stop:

| Threat | Example | What actually helps |
|---|---|---|
| **Malware you run yourself** | Binance 2026: a fake job interview's "coding test" infected the engineer's own device | Never run untrusted code or "test tasks" on a work device. Use a separate sandbox/VM. Keep endpoint protection (EDR) on and up to date |
| **Phishing and stolen sessions** | A fake login page, or a stolen browser session cookie | Phishing-resistant MFA (passkeys/FIDO2), Conditional Access, short session lifetimes |
| **Compromise of the personal device you use for work** | LastPass 2022: corporate credentials typed on a personal home PC | Do work only on the managed work device. Never put corporate credentials on personal machines |
| **Attacks over the internet** | Exposed services, vulnerable VPN clients | Patching, no open ports, the corporate VPN/ZTNA kept updated |
| **Over-privileged access** | One account can reach production and the wallet signing system | Least privilege, just-in-time admin, separate admin accounts |
| **AI agents with too much access** | An internal AI tool used to move to more colleagues (Binance) | Scope agent permissions, log agent actions, require human approval for sensitive actions |

**In one line:** segmentation limits the blast radius *at home*. Identity, endpoint security and least privilege protect the work itself.

## FAQ

**Casting from my phone to the TV stopped working.**
Casting (Chromecast/AirPlay) needs both devices on the same network. Keep phones and TVs together in the home zone. That's the trade-off I chose.

**My work laptop can't print to the home printer.**
That's isolation working. Options: print from a personal device, email the file to the printer's cloud print service, or plug the printer into the laptop with USB when needed. Don't bridge the networks.

**The VPN or Teams is slow, or doesn't connect, on the guest network.**
Some guest networks have bandwidth limits or block some ports. Check the router's guest settings for limits. If the VPN fails, test on the home network once to rule out the VPN itself, then contact IT.

**I changed the Wi-Fi password, but it went back to the old one.**
Seen on ISP routers. Untick "show password" before typing, use only letters and digits, wait for the router to finish saving, then reload. If it still reverts, the ISP may be pushing settings remotely: change it in the ISP app/portal or call support.

**Do I have to re-pair all my smart devices?**
Only if you change the home Wi-Fi name or password. Reusing the same SSID and password keeps everything connected. Plan 30–60 minutes if you do change them.

**Is WPA3 enough?**
WPA3 protects the Wi-Fi link from outsiders. It does nothing about a device *inside* your network that is already compromised. That's why segmentation matters.

**My employer gave me a laptop. Am I allowed to do this?**
Connecting it to a separate, more secure network is almost always welcome, but check your company's remote-work policy and tell IT. Never change the security settings *on* the work laptop itself.

**Is a guest network as good as VLANs?**
No, but it's ~80% of the benefit for zero cost. VLANs on your own router add a third zone (IoT), firewall rules between zones and better monitoring. See [router-guide.md](router-guide.md) → Case C.
