# Research: breach examples (verified 2026-11-24)

## Binance, October 29, 2026 (~$6.3B)
- **Entry:** in September a fake recruiter on a job platform ran a "job interview" (fake HR video call, then a fake "CEO" chat). The engineer downloaded a "coding assignment" from a code repository. It contained 0-day malware that "was not detected by the endpoint security protection tools at the time" (Binance, via BleepingComputer). The malware replaced `pyenv` in the macOS Homebrew directory.
- **Lateral movement:** "By October 20, the attackers had used the compromised engineer's computer and an internal AI tool to compromise two additional employees working on Binance's wallet infrastructure." They obtained credentials plus a container deployment token. On October 29 they deployed a malicious script and reached the wallet signing service / "a service container involved in withdrawals" (CSO).
- **Attribution:** FBI says North Korea (TraderTraitor / Lazarus / APT38). Binance has not named the attackers itself.
- **Impact:** about $6.3B stolen. Roughly $2.85–3B frozen or intercepted; 95–98% of assets replenished (the sources differ). Binance covers losses from SAFU, and there's no evidence of private-key leakage. DOJ filed civil forfeiture for about $1.1B USDC (Nov 23).
- **Caveats (keep the post accurate):** the role is called "DevOps engineer" (CSO) or "software engineer" (Binance/BC). **Whether it was a home or a work device is NOT stated.** The findings are preliminary, and Binance has promised an independent review.

Sources:
- https://www.bleepingcomputer.com/news/security/binance-says-fake-job-interview-led-to-63-billion-crypto-heist/
- https://www.csoonline.com/article/4243225/a-compromised-devops-laptop-caused-the-6-3b-binance-breach.html
- https://www.darkreading.com/cyberattacks-data-breaches/binance-hack-test-attack-paths
- https://www.foxbusiness.com/fox-news-tech/us-recover-1b-crypto-stolen-north-korean-hackers-binance-heist
- Binance's incident report: https://www.binance.com/en/blog/community/3229153443759566763

## LastPass, 2022 (the home-network case)
- Attackers exploited a remote-code-execution flaw in third-party media software on a **DevOps engineer's home computer** and planted a keylogger. It captured the master password after MFA, and they used it to reach the corporate vault and the cloud backups of customer vaults. The engineer was one of only 4 people with those decryption keys.
- Ars Technica / PCMag reported the software was an old, long-patched **Plex Media Server**. LastPass never confirmed the name, so the post says "an unpatched media server app".
- LastPass afterwards "assisted the DevOps Engineer with hardening the security of their home network."

Sources:
- https://www.bankinfosecurity.com/attackers-hacked-into-lastpass-via-employees-home-computer-a-21335
- https://www.infosecurity-magazine.com/news/lastpass-data-breach-update/
- https://www.securityweek.com/lastpass-says-devops-engineer-home-computer-hacked/amp/
