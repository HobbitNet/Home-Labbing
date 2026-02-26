# Personal Labbing & Security

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

## Security Analysis: Local AI vs Cloud Based LLMs ☁️
As a student in cybersecurity, the decision to self hosting was driven by a risk to reward analysis of data privacy and attack surface management. 

### 1.)  Data sovereignty & privacy
* Local: Prompts & sensitive technical logs will never leave the local network. This mitigates my risk of data leakage to 3rd party providers
* Cloud (OpenAI/Google): Data is processed on external servers, this data is potentially being used for model training or even subjected to possible provider side breaches.

### 2.) Attack surface management
* Risk: Hosting an API (Ollama) can create a new entry point for attackers.
* Mitigation: Instead of approaching this through port forwarding, which opens ports on my router. I had utilized a zero trust overlay ([Tailscale](https://tailscale.com/)/Wireguard). This helps ensure the AI API is only visible to authenticated, encrypted nodes in my mesh network, this effectively makes it "invisible" to the public internet. 

### 3.) Attack surface management
* Offline Capability: My lab remains functional regardless of internet connectivity or external service outages.
* Model integrity: I control the specific AI version and the quantization of the model, ensuring consistent performance without any "stealth" updates from a provider

## Security Implementation: Zero Trust Architecture
As of Feburuary 25, I have trainstioned the Tailscale network from a defualt "allow all" state to a **Zero Trust (Deny-by-Default)** architecture using Tailscale ACLs and Gemma 3 to assist with learning how to setup up the JSON config file.

### Key Security Features:
* **Implicit Deny**: All lateral movement should now be blocked by default.
* **Micro-segmentation**: By using Tailscale tag (`tag:parsec-ollama-host`, `tag:personal-client`), I have isolated specific ports.
* **Least Privilege Access**:
    * **Admins**: Full access to Parsec (8000-9000) and Ollama (11434).
    * **Guests/External (Future)**: I had restricted guest accounts strictly to the Ollama API port, which prevents access to the host desktop or management interfaces.
* **Automated Policy Testing**: Thanks to Gemma 3 we managed to implement built in ACL tests which verify that the security rules are enforced correctly upon every update.


## Lab Roadmap & Modules 
This lab will be divided up into different domains, Each directory will contain it's own detailed documentation and configuration logs.

### [Networking](./Networking/): 
Focus: To create a zero trust architecture & create a way to have secure remote access to the host system.
* Key Project: Implementation of a tailscale based wireguard mesh network.
* Objective: Secure P2P connectivity between my mobile, laptop, and desktop without port forwarding.

### [LLM Operations](./AI-Operations/):
Focus: Learn more about local LLM Hosting & Private cloud AI
* Key Project: Self hosting Ollama with gemm 3 12b for private, offline intelligence.
* Objective: Offloading AI inference to the Ryzen 9 5900x via remote API calls.

## 📈 Current goals:
* [ ] Complete CompTIA Security+ (SY0-701) Certification.
* [ ] Implement Tailscale SSH for secure, keyless terminal management
* [x] Configure Tailscale ACLs for more granular access control between devices
