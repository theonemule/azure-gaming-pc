# ARM Template for Gaming VM Setup

This ARM template deploys a gaming virtual machine ("gamevm") configured with specific network security rules and a public IP, making it ready for gaming scenarios. The deployment includes configuring network interfaces, security groups, and a public IP address.

### [Deploy to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ftheonemule%2Fazure-gaming-pc%2Fmain%2Ftemplate.json)

## Prerequisites

- Azure Subscription
- Azure CLI or PowerShell installed
- Sufficient permissions to create resources in the Azure subscription

## Template Overview

This template provisions the following resources:

- **Virtual Machine**:
  - Configured with Windows 11 (Windows-11, 21h2-pro)
  - Options for various VM sizes based on the gaming requirements (Standard_NG8ads_V620_v1, Standard_NG16ads_V620_v1, Standard_NG32ads_V620_v1)
  - Optional spot instance configuration for cost efficiency

- **Network Security Group**:
  - Security rules for RDP, VNC, and Parsec to facilitate remote access and gaming network configurations

- **Public IP Address**:
  - Static IPv4 address for the VM, making it accessible over the Internet

- **Virtual Network and Subnet**:
  - A virtual network with a default subnet to host the gaming VM

- **Network Interface**:
  - Connected to the created VM, subnet, and public IP with network security group rules applied

## Parameters

- `virtualMachines_gamevm_name`: Name of the virtual machine (Default: "gamevm")
- `adminUsername`: Administrator username for the VM
- `adminPassword`: Administrator password for the VM (Secure string)
- `virtualMachines_gamevm_sku`: SKU for the VM (Options: "Standard_NG8ads_V620_v1", "Standard_NG16ads_V620_v1", "Standard_NG32ads_V620_v1")
- `virtualMachines_gamevm_priority`: Deployment priority ("regular" or "spot", Default: "spot")
- `virtualNetworks_gamevm_name`: Name of the virtual network (Default: "gamevm-vnet")
- `networkInterfaces_gamevm_name`: Name of the network interface (Default: "gamevm-nic")
- `publicIPAddresses_gamevm_ip_name`: Name of the public IP address (Default: "gamevm-ip")
- `networkSecurityGroups_gamevm_nsg_name`: Name of the network security group (Default: "gamevm-nsg")

## Deployment

### Using Azure CLI

1. Clone this repository to your local machine.
2. Navigate to the directory containing this template.
3. Run the following command, replacing the placeholder values with your specific values:

```bash
az deployment group create \
  --name ExampleDeployment \
  --resource-group yourResourceGroupName \
  --template-file template.json \
  --parameters adminUsername='yourUsername' adminPassword='yourPassword'
