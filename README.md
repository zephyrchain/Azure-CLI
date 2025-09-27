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
- Enable dynamic routing with **Azure Route Server**
- Provide name resolution with **Azure Private DNS Resolver** (inbound and outbound endpoints)

---

## Prerequisites

Before running the script, ensure the following:

- **Azure Subscription**: The subscription must be active and have permissions to create resources.  
- **Azure CLI**: The Azure CLI must be installed and authenticated using the `az login` command.  
- **SSH Key Pair**: An SSH key pair is required for VM access. Generate one using the `ssh-keygen` command if you do not already have one.  

> ⚠️ Replace the placeholder subscription ID (`Add Subscription ID Here`) with your actual Azure Subscription ID in NIC creation commands and when associating the subscription to the DNS Resolver.


---

## Deployment Capabilities

### Resource Provisioning

- **Resource Group & VNet**
  - Creates a resource group
  - Defines a virtual network with `/21` address space
  - Subnets for Management, Untrust, Trust, and additional subnets for Route Server and DNS Resolver

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
- **Azure Route Server** deployed for dynamic BGP route exchange with the firewall

### DNS Resolution

- **Azure Private DNS Resolver**
  - Inbound endpoint for on-premises DNS queries
  - Outbound endpoint for forwarding DNS queries to external DNS servers
  - Subscription association for DNS Resolver functionality

---

## Configuration Notes

| Feature            | Description                                                                                   |
|--------------------|-----------------------------------------------------------------------------------------------|
| DNS Name           | The DNS label panmgmt001 is assigned to the management public IP address.                      |
| Zone Awareness     | All resources are deployed in **Availability Zone 2** for high availability.                  |
| BGP Configuration  | Verify that BGP peer IP addresses and Autonomous System Numbers (ASNs) are correctly configured. |
| VPN Shared Key     | Replace the placeholder value `"YourSharedKeyHere"` with your actual VPN shared key.          |
| DNS Resolver       | Confirm that the subscription is associated with the Azure Private DNS Resolver resource.      |

---

## Customization Guidance

Modify the following based on your environment:

- Subscription ID in NIC subnet paths and DNS Resolver association
- Source IPs in NSG rules
- BGP peer IPs and ASNs
- VPN shared key
- Route table next-hop IP
- DNS forwarding rules for outbound resolver

---

## Next Steps

- [Explore Palo Alto VM-Series documentation](https://docs.paloaltonetworks.com/cloud-ngfw-azure/deployment/cloud-ngfw-for-azure-deployment-architectures/)
- [Learn about Azure VPN Gateway](https://learn.microsoft.com/en-us/azure/vpn-gateway/)
- [Understand Azure NSG rules](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)

---

Happy deploying! 🔐🚀

---


License and Permitted Use

This repository is provided for learning, experimentation, and non-commercial use only.  
Commercial use, production deployment by for-profit organizations, resale, or using  
this project for monetary gain is prohibited.

Licensed under the [PolyForm Noncommercial License 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0/) — see the LICENSE file for details.
