# Verification: prove the segmentation works

Replace the placeholders with your own values: `<HOME_SUBNET>` (e.g. `192.168.1`), `<WORK_GATEWAY>`, `<HOME_DEVICE_IP>`.
PowerShell 7+.

## 1. From a home-zone device (e.g. a personal laptop on the home Wi-Fi)
Ping sweep the subnet and list every device that answered:

```powershell
1..254 | ForEach-Object -Parallel { Test-Connection "<HOME_SUBNET>.$_" -Count 1 -TimeoutSeconds 1 -Quiet } -ThrottleLimit 64 > $null
Get-NetNeighbor -AddressFamily IPv4 | Where-Object State -eq Reachable
```

✅ Expected: **the work laptops don't appear.**

## 2. From the work zone (a laptop on the work/guest Wi-Fi)
```powershell
ipconfig                                                    # must be a DIFFERENT subnet from the home network
Test-Connection <HOME_DEVICE_IP> -Count 2                   # camera / TV / printer: must FAIL
Test-NetConnection <HOME_SUBNET>.1 -Port 80                 # home router admin: must FAIL
Test-NetConnection <WORK_GATEWAY> -Port 443                 # router admin from the work side: must FAIL
Test-NetConnection <WORK_GATEWAY> -Port 53                  # DNS: OK to succeed
Test-NetConnection www.microsoft.com -Port 443              # internet: must succeed
```

✅ What I measured: all home devices and both admin pages were blocked, only DNS answered, and the internet and VPN worked.

## 3. Client isolation inside the work zone
With two devices on the work Wi-Fi, ping one from the other.
✅ Expected: **no reply.** If they can see each other, one compromised work device can attack the other.

## 4. Inbound from the internet
- Router firewall: unknown inbound dropped for IPv4 and IPv6, and the IPv6 pinhole/forwarding table is empty
- WAN ping replies off (the router is invisible to ping scans)
- Optional: run an external port scan of your public IP from a trusted online scanner. ✅ Expected: no open ports

## 5. Things still work (usability check)
- Phone → TV casting works
- Camera and vacuum apps work locally and remotely
- Work laptop: VPN connects, Teams/calls are fine

Re-run this list after every router firmware update, ISP change or house move.
