# Building a lab environment
## Purpose
This document will give you ideas on how to build an effective lab environment to play with and apply your knowledge with hands-on scenarios.
## Choosing a platform
When considering a lab build, you'll mainly come down to 2 different platforms:
- __Physical, self-owned hardware__: basically you build your own computer/server with enough ressources to sustain your VMs needs
- __Cloud-based offering__: you would rent a dedicated server from a cloud provider and configure everything remotely
With a cloud-based server, you would receive a public IP (or more) and credentials to connect the server and install it according to your needs. 
Usually, you would install the host system with an hypervisor, and then setup a virtual network with your VMs
### Example of self-owned build
<img width="805" alt="image" src="https://user-images.githubusercontent.com/13363451/187417619-aff7995b-74de-446e-acb5-efaf99bc7cd8.png">

### Example of cloud-based dedicated server
<img width="691" alt="image" src="https://user-images.githubusercontent.com/13363451/187416424-ec2fd44f-154b-4518-b278-a16534e968bc.png">

## Example of a lab setup
This is just an example of lab setup with enough VMs to simulate a small enterprise network.
### VM list
The VMs would be as follow:
| VM name   | OS |      Purpose      |  vCPU | RAM |
|----------|------|-------------|------|------|
| DC01 | Windows Server 2022 (desktop) |  ADDS Domain Controller + DNS + DHCP | 2 | 2 |
| DC02 | Windows Server 2022 (core) | ADDS Domain Controller + DNS | 2 | 2 |
| CLNT01 | Windows 11 Pro | Client and admin station | 2 | 4 |
| LNX01 | Ubuntu Server | Web Server + Mail Server | 2 | 4 |
| KALI01 | Kali Linux | Pentesting machine | 2 | 4 |
| FW01 | pFSense or Check Point GAIA or else | Router/Firewall | 2 | 4 |
|----------|------|TOTAL|12|20|
