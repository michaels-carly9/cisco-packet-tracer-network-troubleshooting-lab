# Cisco Packet Tracer Network Troubleshooting Lab

## Overview
This lab was built in Cisco Packet Tracer to simulate a small enterprise network environment.

The network consists of:
- Cisco 2911 Router
- Two Cisco 2960 Switches
- Four Endpoints
- Two Subnets

The objective of this lab is to configure, validate, troubleshoot, and resolve common network issues using Cisco's IOS and standard network troubleshooting techniques. 


## Skills Demonstrated
- TCP/IP
- Routing
- Cisco IOS
- Network Troubleshooting
- Root Cause Analysis
- ICMP Testing
- Techincal Documentation


## Network Topology
![Network Topology](screenshots/01-Network-Topology.png)

The lab topology consists of one Cisco 2911 router, two Cisco 2960 switches, and four PCs.

## Updated Network Topology
![Updated Network Topology](screenshots/04-topology-with-server.png)

Added a server to the network topology to provide DNS services for name resolution testing and troubleshooting. 

## DNS Service Configuration

A server was added to the network to provide internal DNS services.

Server Configuration:
- IP Address: 192.168.20.100
- Subnet Mask: 255.255.255.0
- Default Gateway: 192.168.20.1

DNS Record:
- fileserver.local --> 192.168.20.100

## DNS Baseline Validation
![DNS Baseline Validation](screenshots/05-dns-baseline-validation.png)

A DNS lookup was validated by succesfully resolving the hostname fileserver.local to its configured IP address.

### Test Performed
- ping fileserver.local

### Result
- Success

The successful response confirmed that the DNS service was functioning correctly and was ready for troubleshooting scenarios involving name resolution failures.

## Router Configuration Verification
![Router Configuration Verification](screenshots/02-Router-Configuration-Verified.png)

Verified GigabitEthernet0/0 and GigabitEthernet0/1 were operational and configured correctly.

## Connectivity Validation
![Connectivity Validation](screenshots/03-Network-Connectivity-Validation.png)

Confirmed successful local and remote network connectivity using ICMP testing.

## Troubleshooting Incidents 

### Incident 001 - Incorrect Default Gateway 

#### Symptoms
![Symptoms](incidents/001-symptom.png)

PC3 successfully communicated with local devices on the 192.168.20.0/24 subnet.
Communication to remote networks failed.

Evidence:
- Successful ping to PC4
- Failed ping to PC1

#### Investigation
![Investigations](incidents/001-investigation.png)

IP configuration was examined on PC3.
An incorrect default gateway was indentified.
Expected Gateway: 192.168.20.1
Configured Gateway: 192.168.20.254

#### Resolution
![Resolution](incidents/001-resolution.png)

The default gateway was corrected from 192.168.20.254 to 192.168.20.1

#### Verification
![Verification](incidents/001-verification.png)

Connectivity to remote networks was restored.
PC3 successfully communicated with hosts located on the 192.168.10.0/24 subnet. Issue resolved. 

### Incident 002 - Router Interface Shutdown

#### Symptoms 
![Symptoms](incidents/002-symptom.png)

Users were unable to communicate with hosts located on the 192.168.20.0/24 network.

Evidence:
- Failed ping from PC1 to PC3
- Remote subnet inaccesible

#### Investigation
![Investigation](incidents/002-investigation.png)

Router interface status was examined using:

show ip interface brief

GigabitEthernet0/1 was found in an administratively down state

#### Resolution
![Resolution](incidents/002-resolution.png)

The disabled interface was re-enabled using:

interface g0/1 no shutdown

#### Verification
![Verification](incidents/002-verification.png)

Connectivity to the remote subnet was restored.

GigabitEthernet0/1 returned to an operational state and ICMP communication was successful.

### Incident 003 - IP Address Misconfiguration

#### Symptoms
![Symptoms](incidents/003-symptom.png)

PC4 was unable to communicate with local network devices.

Evidence:
- Failed ping to the default gateway.
- Failed ping to PC3.

#### Investigation
![Investigation](incidents/003-investigation.png)

A review of endpoint network settings identified an incorrect IP address assignment.

Expected: 192.168.20.11
Actual: 192.168.30.11

#### Resolution
![Resolution](incidents/003-resolution.png)

The endpoint IP address was corrected from 192.168.30.11 to 192.168.20.11.

#### Verification
![Verification](incidents/003-verification.png)

Connectivity was successfully restored. PC4 was able to communicate with the default gateway and other hosts on the local subnet.

### Incident 004 - Incorrect DNS Server Configuration

#### Symptoms
![Symptoms](incidents/004-symptom.png)

Users were unable to reach network resources using hostnames.

Evidence:
- Hostname resolution failed.
- Direct Communication using IP addresses remained successful.

#### Investigation
![Investigation](incidents/004-investigation.png)

The workstation DNS configuration was reviewed.
- Expected DNS Sever: 192.168.20.100
- Configured DNS Server: 192.168.20.200

#### Resolution
![Resolution](incidents/004-resolution.png)

The DNS server address was corrected to 192.168.20.100

#### Verification
![Verification](incidents/004-verification.png)

Hostname resolution was restored. The work station successfully resolved fileserver.local and communicated with the server.
<!-- insert screenshot and troubleshooting -->