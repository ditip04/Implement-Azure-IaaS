# Implementation of IaaS Using Azure 

## 📌 Project Overview

This project demonstrates the implementation of **cross-region network connectivity in Microsoft Azure using Global Virtual Network (VNet) Peering**.

The solution connects two Azure Virtual Networks deployed in different geographical regions, enabling secure private communication between application and database tiers without routing traffic over the public internet.

## 🎯 Project Objectives

- Deploy Azure infrastructure across multiple geographical regions.
- Create and configure Azure Virtual Networks and subnets.
- Deploy virtual machines in separate Azure regions.
- Establish secure connectivity using Global VNet Peering.
- Configure Network Security Groups (NSGs) to control network traffic.
- Validate private communication between virtual machines.
- Troubleshoot network connectivity using Azure Network Watcher.

## 🏢 Business Scenario

Client's organization is a globally distributed organization with its headquarters in **East US** and a branch office in **Southeast Asia**.

The organization requires a multi-tier cloud infrastructure with the following architecture:

- **Headquarters (East US):** Hosts the database tier.
- **Branch Office (Southeast Asia):** Hosts the application tier.
- **Network Connectivity:** Application and database resources must communicate securely over a private network.
- **Connectivity Testing:** Test virtual machines are deployed in both regions to validate communication.

To achieve these requirements, Azure Global VNet Peering was implemented between the two virtual networks.

## 🏗️ Solution Architecture

### Architecture Overview

| Component | Headquarters (HQ) | Branch Office |
|---|---|---|
| Azure Region | East US | Southeast Asia |
| Virtual Network | OSSHQData | OSSBRAPP |
| Address Space | 10.1.0.0/16 | 10.2.0.0/16 |
| Subnet | DataSubnet | AppSubnet |
| Subnet Address | 10.1.1.0/24 | 10.2.1.0/24 |
| Virtual Machine | OSS-HQ-DATA | OSS-BR-APP |
| VM Size | Standard DS1 v2 | Standard DS1 v2 |
| Network Security Group | OSS-HQ-DATA-NSG | Oss-br-app-nsg |

### Network Connectivity

- **Peering Type:** Global VNet Peering
- **HQ-to-Branch Peering:** Hq-to-br
- **Branch-to-HQ Peering:** Br-to-hq
- **Virtual Network Access:** Enabled on both peerings
- **Peering Status:** Connected

## 🛠️ Azure Resources Deployed

| Resource Type | Resource Name |
|---|---|
| Resource Group | ODL-az-2283056 |
| Virtual Network | OSSHQData |
| Virtual Network | OSSBRAPP |
| Virtual Machine | OSS-HQ-DATA |
| Virtual Machine | OSS-BR-APP |
| Network Security Group | OSS-HQ-DATA-NSG |
| Network Security Group | Oss-br-app-nsg |
| VNet Peering | Hq-to-br |
| VNet Peering | Br-to-hq |

## ⚙️ Implementation Steps

### Step 1: Create Azure Virtual Networks

Created two virtual networks in separate Azure regions.

**Headquarters VNet – OSSHQData**
- Region: East US
- Address Space: 10.1.0.0/16
- Subnet: DataSubnet
- Subnet Range: 10.1.1.0/24

**Branch VNet – OSSBRAPP**
- Region: Southeast Asia
- Address Space: 10.2.0.0/16
- Subnet: AppSubnet
- Subnet Range: 10.2.1.0/24

### Step 2: Deploy Azure Virtual Machines

Deployed two virtual machines to represent the application and database tiers.

**OSS-HQ-DATA**
- Region: East US
- VM Size: Standard DS1 v2
- Virtual Network: OSSHQData
- Purpose: Database tier connectivity testing.

**OSS-BR-APP**
- Region: Southeast Asia
- VM Size: Standard DS1 v2
- Virtual Network: OSSBRAPP
- Purpose: Application tier connectivity testing.

### Step 3: Configure Network Security Groups (NSGs)

Configured NSG rules to permit ICMP traffic between the virtual machines for connectivity testing.

**Inbound Rules**
- Protocol: ICMP
- Source: Any
- Destination: Any
- Action: Allow

**Outbound Rules**
- Protocol: ICMP
- Source: Any
- Destination: Any
- Action: Allow

Additionally, verified the operating system firewall configurations to ensure ICMP traffic was permitted.

### Step 4: Configure Global VNet Peering

Established bidirectional Global VNet Peering between the headquarters and branch virtual networks.

**HQ-to-Branch Peering**
- Peering Name: Hq-to-br
- Remote VNet: OSSBRAPP
- Allow Virtual Network Access: Enabled

**Branch-to-HQ Peering**
- Peering Name: Br-to-hq
- Remote VNet: OSSHQData
- Allow Virtual Network Access: Enabled

After configuration, both peering connections displayed the status **Connected**.

### Step 5: Validate Cross-Region Connectivity

Tested private network communication between both virtual machines using their private IP addresses.

**Connectivity Tests**
1. From OSS-BR-APP, ping the private IP address of OSS-HQ-DATA.
2. From OSS-HQ-DATA, ping the private IP address of OSS-BR-APP.
3. Verify effective routes on the virtual machine network interfaces.
4. Perform connectivity diagnostics using Azure Network Watcher.

Successful ping responses confirmed private communication between the two Azure regions.

## 🔍 Challenges and Troubleshooting

During initial connectivity testing, communication between the virtual machines failed despite successful VNet Peering configuration.

The following troubleshooting activities were performed:

- Verified that both VNets had non-overlapping IP address spaces.
- Confirmed that both peering connections displayed a Connected status.
- Reviewed effective routes associated with the network interfaces.
- Checked NSG inbound and outbound security rules.
- Verified operating system firewall settings.
- Used Azure Network Watcher to investigate connectivity issues.

**Resolution:** Corrected the relevant network security and firewall configurations, successfully establishing communication between both virtual machines.

## 🔐 Benefits of Global VNet Peering

- **Private Connectivity:** Enables communication between resources without exposing traffic to the public internet.
- **Microsoft Backbone:** Routes inter-VNet traffic through Microsoft's private network.
- **Low Latency:** Provides efficient communication between geographically distributed resources.
- **High Bandwidth:** Supports high-throughput connectivity between virtual networks.
- **Simplified Architecture:** Eliminates the need to manage VPN gateways for VNet-to-VNet connectivity.
- **Scalability:** Supports distributed cloud architectures across multiple Azure regions.

## 📊 Project Outcome

Successfully implemented cross-region connectivity between two Azure Virtual Networks located in East US and Southeast Asia.

The project demonstrated the ability to:

- Deploy and configure Azure IaaS resources.
- Design network infrastructure across multiple Azure regions.
- Establish bidirectional Global VNet Peering.
- Configure NSGs and operating system firewalls.
- Validate private connectivity using ICMP and Azure Network Watcher.
- Troubleshoot cross-region network communication issues.

## 🧠 Key Skills Demonstrated

- Microsoft Azure IaaS
- Azure Virtual Networks (VNet)
- Global VNet Peering
- Azure Virtual Machines
- Network Security Groups (NSG)
- IP Addressing and Subnetting
- Private Network Connectivity
- Azure Network Watcher
- Network Troubleshooting
- Cloud Infrastructure Deployment

## 🏁 Conclusion

This project provided practical experience in designing and implementing secure cross-region network connectivity using Microsoft Azure Global VNet Peering.

By connecting the headquarters and branch office environments, the solution enabled private communication between application and database tiers while demonstrating essential cloud networking, infrastructure deployment, network security and troubleshooting skills.

The implementation reflects a real-world multi-region Azure networking scenario relevant to enterprise cloud infrastructure and administration.
