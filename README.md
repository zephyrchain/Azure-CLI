# 🚀 Azure Palo Alto VM-Series Deployment Script

This repository contains a comprehensive Azure CLI script to deploy a Palo Alto VM-Series firewall in a production-grade environment within the **East US** region. The script automates the creation of networking components, virtual machines, and VPN connectivity required for a secure and scalable deployment.

---

## 📋 Prerequisites

Before running the script, ensure you have:

- ✅ An active Azure subscription  
- ✅ Azure CLI installed and authenticated (`az login`)  
- ✅ Permissions to create resources in your subscription  
- ✅ SSH key pair for VM access (`ssh-keygen` if not already generated)

> ⚠️ **Important:** Replace the placeholder subscription ID (`Add Subscription ID Here`) with your actual Azure Subscription ID in the NIC creation commands.

---

## 🛠️ What This Script Does

### 🔹 Resource Group & VNet Setup
- Creates a resource group and a virtual network with a `/16` address space  
- Defines three subnets for:
  - Management
  - Untrust
  - Trust interfaces

### 🔹 Public IP & NIC Configuration
- Allocates a static public IP for the management interface  
- Creates three NICs, each assigned to a specific subnet

### 🔹 Network Security
- Creates a Network Security Group (NSG) with rules to allow:
  - SSH access
  - HTTPS access  
- Associates the NSG with the management NIC

### 🔹 VM-Series Deployment
- Accepts legal terms for Palo Alto VM-Series image  
- Deploys the VM with:
  - Three NICs
  - Palo Alto image `bundle2:8.1.0`

### 🔹 VPN Gateway Setup
- Creates a local network gateway and public IPs for VPN  
- Configures a virtual network gateway with BGP settings  
- Establishes a site-to-site VPN connection

### 🔹 Routing Configuration
- Creates a route table and adds a route to direct traffic to the firewall  
- Associates the route table with the gateway subnet

---

## 📌 Notes

- **DNS Name:** The public IP for management is assigned the DNS name `panmgmt001`  
- **Zone Awareness:** Resources are deployed in **Zone 2** for high availability  
- **BGP Configuration:** Ensure BGP peer IPs and ASNs are correctly set for your environment  
- **Shared Key:** Replace `"YourSharedKeyHere"` with your actual pre-shared key for VPN

---

## 🔧 Customization

You may need to modify the following based on your environment:

- Subscription ID in NIC subnet paths  
- Source IP in NSG rules  
- BGP peer IPs and ASNs  
- VPN shared key  
- Route table next-hop IP

---

## 📞 Support

If you encounter issues or have questions, feel free to:

- Open an issue  
- Submit a pull request  

---

Happy deploying! 🔐🔥
