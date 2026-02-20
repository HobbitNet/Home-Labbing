[⬅️ Back to Home](../README.md)
---

# Networking & Secure Connectivity 🌐
## Overview
This module is focused on the implementation of a zero trust overlay network that helps facililitate secure communication between the "HobbitNet" primary host and my remote client nodes. By taking advantage of a mesh VPN architecture, I have removed the need for edge perimeter vulnerabilities such as port forwarding.  

## Tech Stack 👨🏻‍💻: 
* Protocol; Wireguard (UDP based encryption). 
* Orchestration: Tailscale (P2P mesh VPN).
* Security model: Zero trust/Identity based access control.
* **Services Secured:** Ollama REST API (Port 11434).
    * Parsec Remote Desktop (low latency streaming).
    * Model Inference: Gemma 3 12b (Offloaded to Ryzen 9 5900X)

## Architectural Reasoning 🛡️: 
As a cybersecurity student, my primary objective was to reduce my attack surface of my home network. 

### 1.) Eliminating the need for port forwarding:
Traditionally remote access requires opening ports on the router, which would end up exposing services to public scan and automated exploitive attempts. By using NAT traversal through Tailscale, my desktop remains invisible to the public WAN while remaining accessible to authenticated nodes. 

### 2.) Encrypted tunnels: 
All traffic including queries for my AI model from my Acer predator laptop and desktop stream are all encapsulated in an end to end encrypted tunnel. Which ensures data integrity and confidentiality even when accessing the lab from public wifi.

## Implementation steps 📋: 

### 1.) Tailnet initialization: 
I configured the tailscale daemon on the windows host, and the Linux remote node

### 2.) Endpoint Verification:
I had utilized the tailscale ping to confirm direct p2p paths, all to ensure optimal latency for Parsec.

### 3.) Service binding: Modified Ollama's environment to listen on the tailscale interface IP rather than the localhost, enabling secure remote API calls. 

## Future Security Hardening 📈:
* [ ] Tailscale ACLs: Implement Access Control Lists to restrict the laptop's access to only specific ports on the desktop.
* [ ] Exit Nodes: Configure the desktop as an exit node to route all remote laptop traffic through the secure home fiber connection.
