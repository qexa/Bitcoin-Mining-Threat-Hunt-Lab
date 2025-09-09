# Bitcoin / Cryptomining Threat Hunt Lab (Microsoft Defender XDR)

![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Platform](https://img.shields.io/badge/Platform-Microsoft%20Defender%20XDR-blue)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

## 🔎 Overview
A practical threat hunting lab built for **Microsoft Defender XDR** to simulate, detect, and respond to unauthorized cryptomining activity (e.g., Bitcoin, Monero).  

The lab provides **safe attacker simulations** and **ready-to-run detection content**, helping analysts sharpen their hunting skills against cryptojacking techniques such as high CPU usage, persistence, and suspicious mining pool traffic.  

---

## ⚡ Why This Lab?
Cryptojacking is a growing enterprise threat that silently consumes resources while degrading performance. This lab recreates real-world conditions where cryptomining may occur:

- Persistent **CPU/GPU spikes**  
- **User complaints** about sluggish performance  
- **Network beacons** to mining pools  
- **Suspicious persistence mechanisms**  

🎯 **Objective:** Detect, investigate, and eradicate cryptomining with Defender XDR.

---

## 🛠 Features
- **Simulation Mode** → Safe PowerShell scripts to mimic miner-like behavior (process, file, network, CPU load).  
- **Realistic Mode** → Optional loopback-only `xmrig` miner execution for advanced users (no external traffic).  
- **Detection Content** → 8 KQL queries for processes, file events, network activity, persistence, and resource anomalies.  
- **Threat Intel Integration** → Watchlist CSV of known mining pool domains.  
- **Response Toolkit** → IR playbook + automated cleanup script.  

---

## 🚀 Quick Start

```powershell
# 1. Clone the repository
git clone https://github.com/<your-org>/Bitcoin-Mining-Threat-Hunt-Lab.git
cd Bitcoin-Mining-Threat-Hunt-Lab

# 2. Run simulation (safe mode)
.\lab\attacker\simulate-cryptominer.ps1

# 3. Run detection queries
# Located in /detections/kql/ (execute in sequence)

# 4. Cleanup the environment
.\cleanup\cleanup.ps1
