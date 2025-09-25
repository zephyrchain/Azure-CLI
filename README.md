# Azure Palo Alto VM-Series Deployment Script

## Overview

This repository provides an Azure CLI-based deployment solution for Palo Alto VM-Series firewalls in a production-grade environment within the **East US** region. It automates the provisioning of networking components, virtual machines, and VPN connectivity to ensure a secure and scalable infrastructure.

> ✅ Use this script to streamline firewall deployment, enforce network segmentation, and establish secure site-to-site VPN connectivity.

---

## Why Use This Script?

This deployment script helps you:

- Rapidly deploy Palo Alto VM-Series firewalls with best-practice configurations
- Automate resource provisioning for consistent and repeatable deployments
- Integrate VPN and BGP routing for hybrid connectivity
- Enhance security posture with NSGs and custom routing

---

## Prerequisites

Before running the script, ensure the following:

| Requirement | Description |
|------------|-------------|
| Azure Subscription | Must be active and have resource creation permissions |
| Azure CLI | Installed and authenticated (`az login`) |
| SSH Key Pair | Required for VM access (`ssh-keygen` if not already generated) |

> ⚠️ Replace the placeholder subscription ID (`Add Subscription ID Here`) with your actual Azure Subscription ID in NIC creation commands.

---

## Deployment Capabilities

### Resource Provisioning

- **Resource Group & VNet**
  - Creates a resource group
  - Defines a virtual network with `/16` address space
  - Subnets for Management, Untrust, and Trust interfaces

- **Public IP & NICs**
  - Static public IP for management
  - Three NICs assigned to respective subnets

- **Network Security**
  - NSG with rules for SSH and HTTPS
  - NSG associated with management NIC

### VM-Series Deployment

- Accepts legal terms for Palo Alto image
- Deploys VM with:
  - Palo Alto image `bundle2:8.1.0`
  - Three NICs

### VPN Gateway Setup

- Local network gateway and public IPs
- Virtual network gateway with BGP
- Site-to-site VPN connection

### Routing Configuration

- Route table with next-hop to firewall
- Route table associated with gateway subnet

---

## Configuration Notes

| Feature | Detail |
|--------|--------|
| DNS Name | `panmgmt001` assigned to management public IP |
| Zone Awareness | Resources deployed in **Zone 2** |
| BGP | Ensure peer IPs and ASNs are correctly set |
| VPN Key | Replace `"YourSharedKeyHere"` with actual key |

---

## Customization Guidance

Modify the following based on your environment:

- Subscription ID in NIC subnet paths
- Source IPs in NSG rules
- BGP peer IPs and ASNs
- VPN shared key
- Route table next-hop IP

---

## Next Steps

- [Explore Palo Alto VM-Series documentation](https://www.paloaltonetworks.com/resources/datasheets/vm-series-on-azure)
- [Learn about Azure VPN Gateway](https://learn.microsoft.com/en-us/azure/vpn-gateway/)
- [Understand Azure NSG rules](https://learn.microsoft.com/en-us/azure/networking/network-security-groups-overview)

---

## Support

If you encounter issues or have questions:

- Open an issue in this repository
- Submit a pull request with improvements

---

Happy deploying! 🔐🚀

---

Let me know if you'd like to add diagrams, code blocks, or tables for specific command breakdowns!
