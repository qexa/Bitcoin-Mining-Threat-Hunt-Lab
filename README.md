# 🪙 Bitcoin / Cryptomining Threat Hunt Lab (Microsoft Defender XDR)

![Status](https://img.shields.io/badge/Lab-Ready-brightgreen)
![Hunting](https://img.shields.io/badge/KQL-Queries-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Platform](https://img.shields.io/badge/Platform-Microsoft%20Defender%20XDR-purple)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-orange)

## 📖 Overview
This repository provides a **hands-on threat hunting lab** to simulate and detect **unauthorized cryptocurrency mining (cryptojacking)** within Microsoft Defender XDR.  

You will learn how to:  
- Simulate miner-like activity safely in a lab environment.  
- Detect miner files, processes, scheduled tasks, and network traffic using **Advanced Hunting (KQL)**.  
- Build watchlists for known mining pools.  
- Apply an **Incident Response Playbook** to contain, eradicate, and recover from incidents.  

---

## 🎯 Objectives
- Practice **threat hunting** against realistic cryptomining scenarios.  
- Correlate telemetry across **file, process, network, DNS, performance, and persistence events**.  
- Strengthen detection and response playbooks against cryptojacking campaigns.  

---

## 🏗️ Lab Architecture

```mermaid
flowchart LR
    A[Attacker / Rogue User] -->|drops miner files| B[(Endpoint)]
    B -->|Scheduled Task| C[Persistence]
    B -->|High CPU Usage| D[Performance Anomaly]
    B -->|Stratum Protocol Traffic| E[Mining Pools]
    B -->|File/Process/Network Logs| F[Defender Sensors]
    F -->|Advanced Hunting KQL| G[Threat Hunts]
    G -->|Analyst Actions| H[Containment & Recovery]
