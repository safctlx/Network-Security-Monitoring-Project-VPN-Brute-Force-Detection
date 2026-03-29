# Network Security Monitoring Project – VPN & Brute Force Detection using WireGuard & ELK Stack

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Lab Architecture](#lab-architecture)
- [Data Flow](#data-flow)
- [Technology Used](#technology-used)
- [Implementation Steps](#implementation-steps)
  - [VPN Setup](#vpn-setup)
    - [Wireguard Configuration Guide](docs/WireGuardVPN.md)
    - [ELK Stack Configuration Guide](docs/ELK-Stack.md)
  - [Log Collection and Forwarding](#log-collection-and-forwarding)
  - [Attack Simulation](#attack-simulation)
  - [Visualization and Detection](#visualization-and-detection)
- [Key Outcomes](#key-outcomes)
- [Screenshots](#screenshots)

---

## Overview

This project demonstrates a self-built networking and cybersecurity lab designed to simulate how a client connects to a VPN via a VPN tunnel and how brute-force attacks can be simulated and detected in a controlled environment. The lab integrates a VPN server with centralized logging and visualization to mimic a basic Security Operations Center (SOC) workflow.

The goal of this project is to showcase hands-on experience in:

1. How VPN works, showing practically how any request passes through a VPN
2. Network Security
3. Telemetry forwarding and log analysis
4. Threat detection using SIEM tools

---

## Prerequisites

Before attempting this project, it is recommended to be familiar with:

- Linux OS and commands
- Public and private key concepts
- Networking concepts: subnetting, DHCP, VPN, client-server architecture, NAT, IP forwarding, Firewall
- Log analysis and SIEM (Security Information and Event Management), Endpoint Security
- SSH remote connection and Metasploit basics

---

## Lab Architecture

This lab consists of three virtual machines. The IP addresses used here are examples and may vary in different setups:

1. **Kali Linux (VPN Client and Attacker) → IP: 192.168.201.17**
   - Acts as WireGuard VPN client and attacker machine (GUI interface)
   - Used for SSH connections to other machines

2. **WireGuard VPN Server (Headless Server) → IP: 192.168.202.173**
   - Provides secure communication between client and internal network
   - Entry point for monitored traffic
   - Filebeat agent installed for log forwarding

3. **ELK Stack Server (Elasticsearch + Kibana + Logstash, Headless) → IP: 192.168.202.174**
   - Collects, stores, and visualizes logs
   - Used for detecting suspicious activities
   - Components installed: Elasticsearch, Kibana, Logstash

---

## Data Flow

1. **VPN Traffic:**  
   `Kali VPN Client → VPN Server → Internet (Outside World)`

2. **SIEM Simulation:**  
   `Kali Linux → WireGuard VPN → Log Forwarding → Elasticsearch → Kibana Dashboard`

---

## Technology Used

- Linux OS (Ubuntu & Kali Linux, GUI and headless)
- WireGuard VPN
- Elasticsearch, Kibana, Logstash
- Log Analysis
- SIEM Concepts

---

## Implementation Steps

### VPN Setup

- Configure WireGuard VPN on client and server
- Set up the WireGuard interface

### Log Collection and Forwarding

- Install Filebeat and Logstash to configure log collection and forwarding
- Forward logs to Elasticsearch

### Attack Simulation

- Performed brute-force attack attempts from Kali Linux against the VPN server using Metasploit
- Generated multiple failed authentication logs along with successful logins

### Visualization and Detection

- Created Kibana dashboards to monitor:
  - Failed login attempts
  - Source IP activity
  - Authentication trends
  - Identified indicators of compromise (IoCs)
- Detected brute-force attack patterns through repeated failed login attempts

---

## Key Outcomes

- Established a secure VPN connection and ensured traffic flow through the VPN tunnel
- Simulated brute-force attacks and successfully detected attack patterns via log analysis
- Visualized authentication anomalies in real-time using Kibana
- Built a functional mini-SOC environment for security monitoring

---

## Screenshots

- **IP of Elasticsearch Headless Server**  
  ![01 - Elasticsearch IP](Screenshots/01-elasticsearch-ip.png)

- **IP of VPN Server (WireGuard interface wg0)**  
  ![02 - VPN Server wg0](Screenshots/02-vpn-server-wg0.png)

- **IP of Kali Linux (VPN Client, wg0)**  
  ![03 - Kali Client wg0](Screenshots/03-kali-client-wg0.png)
