# EWB-AWS-VPC-Peering-Project
AWS VPC Peering private networking project with EC2, route tables, security groups, and bastion host
# AWS VPC Peering: Private Network Connectivity Project
**EWB Cloud Labs – AWS Architect Associate**

* **Student Name:** Mannat Saini
* **Project Title:** Connect Two VPCs via VPC Peering & Prove Private Connectivity
* **Region:** Asia Pacific (Mumbai) / ap-south-1
* **Date:** October 2026

## Project Overview
This project establishes private, bidirectional network connectivity between two isolated Virtual Private Clouds (VPC A: `10.10.0.0/16` and VPC B: `10.20.0.0/16`) using AWS VPC Peering. Workload servers remain completely private with no direct internet access, while administrative access is securely handled via SSH ProxyJump through a public bastion host.

## Infrastructure Deployed
- **VPC A:** `10.10.0.0/16` (`vpc-0eafbc5eaea6cd1f4`) with attached Internet Gateway `ewb-igw-a`
  - Public Subnet: `10.10.1.0/24` hosting `ewb-bastion` (`10.10.1.10` / `15.206.117.187`)
  - Private Subnet: `10.10.2.0/24` hosting `ewb-app-a` (`10.10.2.10`)
- **VPC B:** `10.20.0.0/16` (`vpc-0b5436d63b1fdc9e5`) with no Internet Gateway
  - Private Subnet: `10.20.1.0/24` hosting `ewb-app-b` (`10.20.1.10`)
- **VPC Peering Connection:** `ewb-a-b-peer` (`pcx-042573d3643c3a83f`)

## Verification Summary
- **Baseline Isolation Test:** 100% packet loss prior to route resolution.
- **Forward Path Reachability:** 0% packet loss ping from App-A to App-B over the peering connection.
- **Reverse Path Reachability:** 0% packet loss ping from App-B back to App-A.
- **Private SSH Administration:** Interactive shell connected on App-B via bastion ProxyJump.
- **Controlled Failure Test:** 100% packet loss upon deleting the inbound ICMP rule on App-B, followed by immediate recovery to 0% loss upon restoration.
- **Cleanup:** All EC2 instances terminated, peering connection deleted, gateways detached/deleted, and custom VPCs removed.

## Repository Contents
- `MannatSaini_EWB_VPC_Peering.pdf` – Full comprehensive lab report document.
- Raw screenshots covering all architecture checkpoints, route tables, terminal verification tests, and cleanup confirmations.
