# Network-Design-Overview-for-Small-Business

## Building Layout:

### 1.	First Floor:
   
- Sales and Marketing Department: 120 users
- Human Resource and Logistics Department: 120 users

### 2.	Second Floor:

- Finance and Accounts Department: 120 users
- Administrator and Public Relations Department: 120 users
### 3.	Third Floor:

- ICT Department: 120 users
- Server Room: 12 devices
## Network Requirements:

- Hierarchical design with redundancy.
- Two routers and two multilayer switches for redundancy.
- Two ISP connections for internet redundancy.
- Wireless network for each department.
- Each department in separate VLANs and subnets.
  
## IP Addressing:

- Base network: 172.16.1.0/24.
- Public IPs: 195.136.17.0/30, 195.136.17.4/30, 195.136.17.8/30, 195.136.17.12/30.
## Configuration Steps:
### 1)	Subnetting:
-	Allocate subnets for each department and VLAN.
-	Example: 172.16.1.0/25 for Sales and Marketing, 172.16.1.128/25 for HR and Logistics, etc.

### 2)	Devices:
-	Routers and Multilayer Switches: Configure OSPF, static routing, PAT, Ether-channel and ACL.
-	DHCP Servers: Located in the server room for dynamic IP allocation.
-	Switchports: Configure port-security for Finance and Accounts.
### 3)	Security:
-	Configure SSH for remote login.
-	Set hostnames, passwords, and disable IP domain lookup.
-	Port-security using sticky method in Finance and Accounts department.(Violation shutdown)
### 4)	Redundancy:
-	Connect each router to both ISPs.
-	Use multilayer switches for inter-VLAN routing.
-	HSRP 
### 5)	Wireless Networks:
-	Configure a separate SSID for each department.
### 6)	Testing:
-	Ensure communication within and across departments.
-	Validate DHCP, inter-VLAN routing, SSH, and internet access.

## Implementation in Cisco Packet Tracer
-	Design the network topology with the specified devices.
-	Apply the configurations to simulate and test the network.


## Subnetting
Base Network: 172.16.1.0/24


| Department                | Host | Network Address | Subnet mask   | First IP      | Last IP       | Broadcast     |
|---------------------------|------|-----------------|---------------|---------------|---------------|---------------|
| Sales & Marketing         | 120  | 172.16.1.0      | 255.255.255.128 | 172.16.1.1    | 172.16.1.126  | 172.16.1.127  |
| HR & Logistics            | 120  | 172.16.1.128    | 255.255.255.128 | 172.16.1.129  | 172.16.1.254  | 172.16.1.255  |
| Finance & Account         | 120  | 172.16.2.0      | 255.255.255.128 | 172.16.2.1    | 172.16.2.126  | 172.16.2.127  |
| Admin & Public Relations  | 120  | 172.16.2.128    | 255.255.255.128 | 172.16.2.129  | 172.16.2.254  | 172.16.2.255  |
| ICT                       | 120  | 172.16.3.0      | 255.255.255.128 | 172.16.3.1    | 172.16.3.126  | 172.16.3.127  |
| Server                    | 12   | 172.16.3.128    | 255.255.255.240 | 172.16.3.129  | 172.16.3.142  | 172.16.3.143  |

## Network Configuration for Core and MLS

| Host              | Network Address | Subnet mask       | First IP      | Last IP       | Broadcast     |
|-------------------|-----------------|-------------------|---------------|---------------|---------------|
| Core1 vs MLS1     | 2               | 172.16.3.144      | 255.255.255.252 /30 | 172.16.3.145  | 172.16.3.146  | 172.16.3.147  |
| Core1 vs MLS2     | 2               | 172.16.3.148      | 255.255.255.252 /30 | 172.16.3.149  | 172.16.3.150  | 172.16.3.151  |
| Core2 vs MLS1     | 2               | 172.16.3.152      | 255.255.255.252 /30 | 172.16.3.153  | 172.16.3.154  | 172.16.3.155  |
| Core2 vs MLS2     | 2               | 172.16.3.156      | 255.255.255.252 /30 | 172.16.3.157  | 172.16.3.158  | 172.16.3.159  |
| MLS1 vs MLS2      | 2               | 172.16.3.160      | 255.255.255.252 /30 | 172.16.3.161  | 172.16.3.162  | 172.16.3.163  |

