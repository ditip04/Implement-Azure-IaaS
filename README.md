Project Title
Implementation of Implement Azure IaaS
________________________________________
Objective
The objective of this project is to deploy infrastructure across multiple Azure regions and establish secure private communication between application and database tiers using Azure Virtual Network (VNet) Peering. The solution demonstrates how organizations can securely connect resources hosted in different Azure regions without exposing traffic to the public internet.
________________________________________
Business Scenario
Client is a globally distributed organization with its headquarters located in the East US region and a branch office located in the Southeast Asia region. The organization plans to deploy a multi-tier application in Azure where:
•	The Database Tier resides in the Headquarters region (East US).
•	The Application Tier resides in the Branch region (Southeast Asia).
•	Communication between the application and database tiers must occur over a private Azure network.
•	Test virtual machines are deployed to validate connectivity between both regions.
To meet these requirements, Azure Virtual Network Peering was implemented between two VNets located in different Azure regions.
________________________________________
Solution Architecture
Headquarters Environment
•	Region: East US
•	Virtual Network: OSSHQData
•	Address Space: 10.1.0.0/16
•	Subnet: DataSubnet
•	Virtual Machine: OSS-HQ-DATA
•	VM Size: Standard DS1 v2
Branch Environment
•	Region: Southeast Asia
•	Virtual Network: OSSBRAPP
•	Address Space: 10.2.0.0/16
•	Subnet: AppSubnet
•	Virtual Machine: OSS-BR-APP
•	VM Size: Standard DS1 v2
Connectivity
•	Azure Global VNet Peering established between both VNets.
•	Private communication enabled over Microsoft's backbone network.
•	ICMP traffic allowed for connectivity testing.
________________________________________
Resources Created
Resource Type	Resource Name
Resource Group	ODL-az-2283056
Virtual Network	OSSHQData
Virtual Network	OSSBRAPP
Virtual Machine	OSS-HQ-DATA
Virtual Machine	OSS-BR-APP
Network Security Group	OSS-HQ-DATA-NSG
Network Security Group	Oss-br-app-nsg
VNet Peering	Hq-to-br
VNet Peering	Br-to-hq
________________________________________
Implementation Steps
Step 1: Create Virtual Networks
Created two Virtual Networks in separate Azure regions:
OSSHQData
•	Region: East US
•	Address Space: 10.1.0.0/16
•	Subnet: 10.1.1.0/24
OSSBRAPP
•	Region: Southeast Asia
•	Address Space: 10.2.0.0/16
•	Subnet: 10.2.1.0/24
________________________________________
Step 2: Deploy Virtual Machines
Deployed two Azure virtual machines:
OSS-HQ-DATA
•	Region: East US
•	Size: Standard DS1 v2
•	Connected to OSSHQData
OSS-BR-APP
•	Region: Southeast Asia
•	Size: Standard DS1 v2
•	Connected to OSSBRAPP
________________________________________
Step 3: Configure Network Security
Configured Network Security Group (NSG) rules to allow ICMP traffic.
Inbound Rule:
•	Protocol: ICMP
•	Source: Any
•	Destination: Any
•	Action: Allow
Outbound Rule:
•	Protocol: ICMP
•	Source: Any
•	Destination: Any
•	Action: Allow
Additionally, operating system firewall settings were verified to allow ICMP traffic.
________________________________________
Step 4: Configure VNet Peering
Established bidirectional VNet peering between the two virtual networks.
Peering Configuration
HQ to Branch
•	Peering Name: Hq-to-br
•	Allow Virtual Network Access: Enabled
Branch to HQ
•	Peering Name: Br-to-hq
•	Allow Virtual Network Access: Enabled
After configuration, the peering status displayed:
Connected
________________________________________
Step 5: Connectivity Validation
Verified connectivity using private IP addresses assigned to both virtual machines.
Validation Methods
•	Ping Test
•	Effective Route Verification
•	Network Watcher Connectivity Check
Example:
OSS-BR-APP → Ping → OSS-HQ-DATA Private IP
OSS-HQ-DATA → Ping → OSS-BR-APP Private IP
Successful responses confirmed private connectivity between both Azure regions.
________________________________________
Challenges Encountered
During implementation, connectivity testing initially failed despite successful VNet peering. Troubleshooting included:
•	Verifying VNet address spaces were non-overlapping.
•	Confirming peering status was connected.
•	Reviewing effective routes on network interfaces.
•	Validating Network Security Group rules.
•	Checking operating system firewall settings.
•	Using Azure Network Watcher for diagnostics.
After correcting network and firewall configurations, connectivity was successfully established.
________________________________________
Benefits of VNet Peering
•	Low latency communication.
•	High bandwidth connectivity.
•	Traffic remains on Microsoft's private backbone.
•	No public internet exposure.
•	Simplified network architecture.
•	Cost-effective compared to VPN gateways.
________________________________________
Project Outcome
The project successfully demonstrated the deployment of a multi-region Azure infrastructure using Virtual Network Peering. Two virtual networks located in East US and Southeast Asia were connected securely, enabling private communication between application and database tiers. Connectivity was validated through network testing, fulfilling all business and technical requirements.
________________________________________
Conclusion
Azure Virtual Network Peering provides a secure, scalable, and efficient solution for connecting resources across regions. By implementing Global VNet Peering, Client achieved private communication between its application and database environments while maintaining security and performance requirements. This deployment serves as a practical example of designing and implementing cross-region network connectivity in Microsoft Azure.

