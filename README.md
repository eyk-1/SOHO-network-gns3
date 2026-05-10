# SOHO Network — GNS3 Simulation
### CSE248 Computer Communication Networks | Spring 2026

A Small Office / Home Office (SOHO) network designed, configured, and simulated in GNS3 running on Ubuntu 24.04 inside VirtualBox. Built as the major project for CSE248 at el IBA

---

## Network Overview

| Device | Hostname | Model | Role |
|--------|----------|-------|------|
| Router | R1 | Cisco C3725 | Gateway, DHCP, NAT, Firewall |
| Switch | SW1 | GNS3 Ethernet Switch | Layer 2 LAN switching |
| PC1–PC4 | PC1–PC4 | GNS3 VPCS | End-user workstations |

### IP Addressing

| Device | Interface | IP Address | Mask |
|--------|-----------|------------|------|
| R1 | fa0/0 (LAN) | 192.168.1.1 | /24 |
| R1 | fa0/1 (WAN) | 203.0.113.2 | /30 |
| PC1–PC4 | eth0 | 192.168.1.10–.13 | /24 |

---

## Services Configured

- **DHCP** — R1 automatically assigns IPs to all 4 PCs from the 192.168.1.0/24 pool
- **NAT/PAT** — All PCs share the single WAN IP (203.0.113.2) for outbound traffic
- **Static Routing** — Default route via 203.0.113.1 (simulated ISP gateway)
- **Firewall ACL** — Extended ACL on fa0/1 blocking unsolicited inbound WAN traffic

---

## What's in This Repo

```
SOHO-network/
├── project-files/          # GNS3 project files (configs, topology)
│   ├── dynamips/           # Router startup configs
│   └── vpcs/               # PC startup configs
├── untitled.gns3           # Main GNS3 project file
└── README.md
```

---

## How to Open the Project

1. Install GNS3 on Ubuntu (see setup instructions below)
2. Download the Cisco C3725 IOS image — `c3725-adventerprisek9-mz.124-15.T14.bin`
   - Source: https://github.com/hegdepavankumar/Cisco-Images-for-GNS3-and-EVE-NG
3. Import the image in GNS3 via **Edit → Preferences → Dynamips → IOS Routers**
4. Open the `.gns3` project file in GNS3
5. Start all devices and run `dhcp` on each VPCS

> **Note:** The Cisco IOS image is not included in this repo due to GitHub file size limits. Use the link above to source the same image.

---

## Demo Video

🎥 [Watch the demo on Google Drive](https://drive.google.com/file/d/1-cCwXjRjDSv9fVDhJSJQ5kgovsitOLLv/view)

---

## VM Download

💾 [Download the exported Ubuntu VM (.ova)](https://drive.google.com/drive/u/1/folders/1AiqY1emCmwxSwZEzhu5-f3MXO3PGN2Vo)

> Exported from VirtualBox. Import via **File → Import Appliance** in VirtualBox.

---

## Setup (GNS3 on Ubuntu)

```bash
sudo add-apt-repository ppa:gns3/ppa
sudo apt update
sudo apt install gns3-gui gns3-server -y
sudo usermod -aG ubridge,libvirt,kvm,wireshark $(whoami)
sudo reboot
```

---
