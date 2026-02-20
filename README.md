# Personal-Labbing-&-Security-Lab

## Overview: 
Welcome to my personal home lab environment that I hope to learn from! This repository serves to be a place of documentation of my journey through practing different cybersecurity concepts, network engineering and local AI infrastructure! I aim to use this lab to bridge the gap between has theoritical concepts to more hands on implementation. 


## Hardware Architectures 🖥️ 
To support a more resource heavy AI model and multiple VM's for my other labs I've slowly built a custom desktop/workstation designed for such tasks. below is a table for the hardware used as well other hardware used with these labs.

### Primary Host (The Server)
| Component | Specification |
| :--- | :--- |
| **CPU** | AMD Ryzen 9 5900X (12 Cores / 24 Threads) |
| **GPU** | Nvidia RTX  3070 8gb |
| **Motherboard** | ASUS TUF Gaming X570-Plus WiFi |
| **Memory** | 32GB DDR4 @ 3600MHz CL16 |
| **Case** | Lian Li O11 Dynamic XL |
| **Networking** | Tailscale Overlay / Gigabit Ethernet |

### Remote Nodes (The Clients)
| Device | Role | Key Specifications |
| :--- | :--- | :--- |
| **Acer Predator Helios 300** | Remote Workstation | Dual-Boot (Linux Mint / Windows) |
| **Android Mobile** | Monitoring Node | Tailscale Access / AI Querying |
| **Meta Quest 3** | AR Interface | Remote Desktop / Immersive Workflow |> [!IMPORTANT]
> **Security Posture Note:** All remote nodes communicate with the Primary Host exclusively over a peer-to-peer WireGuard mesh (Tailscale). This ensures that management traffic, Parsec streams, and AI queries are encrypted end-to-end and are never exposed to the public internet, this is incredibly useful when I want to work on projects or tinker around when away from home

## Lab Roadmap & Modules 
This lab will be divided up into different domains, Each directory will contain it's own detailed documentation and configuration logs.

### Networking 🌐:
Focus: To create a zero trust architecture & create a way to have secure remote access to the host system.
* Key Project: Implementation of a tailscale bsed wireguard mesh network.
* Objective: Secure P2P connectivity between my mobile, laptop, and desktop without port forwarding.

### LLM Operations 🤖:
Focus: Learn more about local LLM Hosting & Private cloud AI
* Key Project: Self hosting Ollama with gemm 3 12b for private, offline intelligence.
* Objective: Offloading AI inference to the Ryzen 9 5900x via remote API calls.

## Current goals 📈:
* [ ] Complete CompTIA Security+ (SY0-701) Certification.
* [ ] Implement Open WebUI as a frontend for the local Ollama instance.
* [ ] Configure Tailscale ACLs for more granular access control between lab VMs.
