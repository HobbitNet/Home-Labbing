[⬅️ Back to Networking](../README.md)
---

# Configuration Manifest: 

# Overview
This folder serves to contain sanitized templates & other configuration notes for the "HobbitNet" infrastructure. These files are here to serve as the definitive source for how services are bound and how the zero trust mesh is designed

## Key Configuration files 📄: 

### 1.) Ollama-service.env
* Purpose: To define the environment variables required to make the local AI API accessible across the Tailscale mesh.
* Key setting: OLLAMA_HOST=[REDACTED_TAILSCALE_IP]:11434 
* By binding it this, the service listens on the Tailscale virtual interface. This allows the Acer Predator remote node to submit inference requests securely. 

### 2.) tailscale-policy.hujson (Template)
* Purpose: A draft of access control list (ACL) logic which is intended for the next phase of lab hardening.
* Security model: Implementation of the principle of least privilege. 
* Logic: To restrict remote nodes such as the quest 3, laptop and mobile. So that they can only access specific ports (11434 for AI,8080 for WebUi) on the primary host

### 3.)  connectivity-check.sh
* Purpose: a simple Bash script used on the Linux client to verify end to end connectivity.
* Function: Performs a curl request to the Ollama API tags endpoint to ensure the encrypted tunnel is passing the traffic correctly. 

# Sanitization Standards: 
To maintain the security of this public repository, all configurations in this folder follow these strict sanitization rules:
* IP redaction: All internal Tailscale IPs are replaced with [REDACTED TAILSCALE IP]
*  Identity Protection: Real names, MagicDNS handles and unique node IDS are scrubbed with generic labels such as primary host, windows, and Linux
*  No secrets: No API keys, Auth keys or private Wireguard keys are ever committed to this repository
