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

### 2.) tailscale-policy.json (Active policy)
* Purpose: Creates a single source of truth.
* Security model: Enforces the princpile of least privelege and implicit deny. By removing the default "allow all" from Tailscale, every connection must now be explicitly authorized by a rule.
* Logic: This is to make an identity based tagging system (tag:personal-client, tag:parsec:parsec-ollama-host) which ensures that management devices have the full access while future guest nodes (like the future tag:gf-client) are mircor sgemented to stritcly the 11434 port for Ollama queries.
* Validation: This process indluded a built in automated security test which verifies the firewall logic everytime a change is saved to a prevent any configuration drift.

### 3.) Config intergrity & Anti drift measures
To Ensure a better security stance, and to scale this system out futher I had implemented several new measures to prevent configuration drift which was a new concept to me, it's essentially to prevent the gradual deviation of the live environment from it's secure documented state.
* Policy as code (Iac): The [tailscalepolicy.json](./Configs/tailscalepolicy.json) being in this repository has allowed me to establish a "single source of truth" which means any future manual changes in the Tailscale console can be audited against this current file to ensure they align with my original security stance
* Automated policy validation: Thanks to Gemma the test section with the ACL config acts as a continous validation layer. Everytime an update is proposed it'll automatically check against my security logic. 
*Identity based persistence: Using tags over the IP addresses helps ensure the security policy remains static even if hardware is replaced or the network interface changes at some point, this helps prevent the possibility of firewall rot which is typically caused from obsolote IP based rules.

### 4.)  connectivity-check.sh
* Purpose: a simple Bash script used on the Linux client to verify end to end connectivity.
* Function: Performs a curl request to the Ollama API tags endpoint to ensure the encrypted tunnel is passing the traffic correctly. 

# Sanitization Standards: 
To maintain the security of this public repository, all configurations in this folder follow these strict sanitization rules:
* IP redaction: All internal Tailscale IPs are replaced with [REDACTED TAILSCALE IP]
*  Identity Protection: Real names, MagicDNS handles and unique node IDS are scrubbed with generic labels such as primary host, windows, and Linux
*  No secrets: No API keys, Auth keys or private Wireguard keys are ever committed to this repository
