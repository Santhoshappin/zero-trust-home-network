# Will this work on my router?

## Decision guide

```
Does your router have a guest Wi-Fi?
│
├─ YES → Is the guest network on a DIFFERENT subnet, or does it have an
│        "isolation" / "don't allow access to local network" option?
│        │
│        ├─ YES → ✅ Case A: use the guest Wi-Fi as your work network.
│        │
│        └─ NOT SURE → Join a laptop to the guest Wi-Fi and run the tests in
│                      verification.md. If home devices are reachable → Case B.
│
└─ NO, or the guest network can reach home devices → Case B or C.
```

**How to check the subnet:** connect a laptop to the guest Wi-Fi and run `ipconfig` (Windows) or `ifconfig` / `ip addr` (Mac/Linux). If the address starts differently from your home network (for example `192.168.168.x` vs `192.168.1.x`), it's a separate subnet. That's a good sign, but **still test it**.

### Case A: the router has an isolated guest network
Follow the [runbook](runbook.md) as written. This is what I used: an ISP router, no extra hardware.

### Case B: the guest network isn't isolated, or doesn't exist
Options, from cheapest up:
1. **Add a second router behind the main one** (an old router or a cheap travel router, ~30–50 €). Plug its WAN port into the main router and connect the work laptop to *its* Wi-Fi. The second router's NAT/firewall keeps home devices from reaching in. *(This is "double NAT": usually fine for VPNs and Teams.)*
2. **Put the IoT devices on the guest network instead**, and keep the work laptop on the main network with *only* trusted devices. This works if the guest network blocks access to the main network, even when it doesn't isolate guests from each other.
3. **Use Ethernet for the work laptop** on its own port or switch, if the router supports port isolation or a separate LAN.

### Case C: you want the "proper" setup
Use a router you own that supports **VLANs** (OpenWrt, UniFi, MikroTik, pfSense/OPNsense, or prosumer models), with three networks: **Home**, **IoT**, **Work**, plus firewall rules between them. This is the upgrade path in the main README.

## Where the settings usually live

Menu names change between models and firmware versions. Use these as a starting point and search the vendor's help site if they don't match.

| Router | Guest Wi-Fi + isolation | WPS | UPnP | Firmware |
|---|---|---|---|---|
| **TP-Link** (Archer, web UI) | Advanced → Wireless → Guest Network. Untick "allow guests to see each other and access my local network" | Advanced → Wireless → WPS | Advanced → NAT Forwarding → UPnP | Advanced → System → Firmware Update |
| **TP-Link Deco** (app) | More → Guest Network | Not exposed / off by default | More → Advanced → UPnP | More → Update Deco |
| **ASUS** (ASUSWRT) | Guest Network → set "Access Intranet" to **Disable** | Wireless → WPS | WAN → Internet Connection → Enable UPnP | Administration → Firmware Upgrade |
| **NETGEAR** | Guest Network. Untick "allow guests to see each other and access my local network" | Advanced → Advanced Setup → Wireless Settings | Advanced → Advanced Setup → UPnP | Advanced → Administration → Firmware Update |
| **AVM FRITZ!Box** | Wi-Fi → Guest Access (isolated from the home network by default). Untick "devices may communicate with each other" | Wi-Fi → Security → WPS | Home Network → Network → Network Settings ("permit access for applications") | System → Update |
| **Eero / Google Nest Wifi** (app) | Guest network in the app (isolated from the main network) | Not available | Advanced / Network settings → UPnP | Automatic |
| **ISP routers** (Telia, Telenor, Comhem/Tele2, BT, Comcast…) | Look for "Guest", "Visitor" or "Gäst". Often under an "Advanced" or "Expert" mode | Often under Wireless/Wi-Fi → WPS | Often under Advanced / Network / NAT | Usually managed by the ISP; check the version in the status page |

**Tip:** some ISP routers are partly managed remotely by the ISP (TR-069). A setting may revert after you save it. If that happens, use the ISP's app or customer portal, or call support.
