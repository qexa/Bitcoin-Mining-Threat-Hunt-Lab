# Bitcoin / Cryptomining Threat Hunt Lab (Microsoft Defender XDR)

![Status](https://img.shields.io/badge/Lab-Ready-brightgreen)
![Hunting](https://img.shields.io/badge/KQL-Queries-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Platform](https://img.shields.io/badge/Platform-Microsoft%20Defender%20XDR-purple)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-orange)

> **Bitcoin / Cryptomining Threat Hunt Lab**  
> Hands-on lab for simulating and detecting unauthorized cryptomining (e.g., Bitcoin/Monero miners) in Microsoft Defender XDR.  
> Includes safe attacker simulation scripts, KQL detections, watchlists, and an IR playbook to help analysts practice hunting high CPU usage, persistence, and mining pool traffic.

---

## Why this Hunt?
- **Management directive** after security news of cryptojacking.
- **Unusual behavior**: sustained CPU/GPU spikes, user complaints of slow performance.
- Objective: **Detect and eradicate unauthorized mining activity**.

---

## Features
- **Simulation Mode**: Safe PowerShell scripts that simulate miner-like behavior (file, process, network, persistence, CPU load).
- **Realistic Mode**: Optional loopback-only xmrig run for advanced users (no external pools).
- **Ready-to-run KQL queries** (8 queries).
- **Watchlist CSV** of mining pool domains.
- **IR playbook** and **cleanup script**.

---

## Quick Start
1. Clone or unzip repo.
2. Run simulation:
   ```powershell
   .\lab\attacker\simulate-cryptominer.ps1
   ```
3. Run queries in `/detections/kql/` in order.
4. Cleanup:
   ```powershell
   .\cleanup\cleanup.ps1
   ```

---

## Repo Layout
```
Bitcoin-Mining-Threat-Hunt-Lab/
├─ README.md
├─ LICENSE
├─ .gitignore
├─ docs/
├─ lab/attacker/
├─ detections/kql/
├─ watchlists/
├─ playbooks/
├─ cleanup/
└─ artifacts/
```

---

## License
Licensed under MIT.
