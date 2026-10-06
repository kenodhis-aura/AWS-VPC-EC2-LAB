# AWS VPC & EC2 Networking Lab

Hands-on AWS networking lab demonstrating VPC design, subnetting, routing, Internet connectivity, security groups, EC2 deployment, and Linux-based connectivity troubleshooting.

## Project Overview

This project demonstrates the deployment of a basic AWS cloud network from the ground up.

The environment was built manually using the AWS Management Console and validated through an Amazon Linux 2023 EC2 instance.

## Objectives

- Create and configure an AWS VPC
- Apply IPv4 CIDR addressing and subnetting
- Create and configure a public subnet
- Attach an Internet Gateway
- Configure a public route table
- Associate the route table with the subnet
- Configure an EC2 security group
- Deploy an EC2 instance
- Establish SSH connectivity
- Validate Internet and DNS connectivity
- Verify AWS instance metadata
- Document the architecture and test results

## Lab Environment

| Component | Configuration |
|---|---|
| AWS Region | Europe (Stockholm) / `eu-north-1` |
| VPC | `aws-cloud-support-vpc` |
| VPC CIDR | `10.0.0.0/16` |
| Subnet | `public-subnet-1` |
| Subnet CIDR | `10.0.1.0/24` |
| Internet Gateway | `aws-cloud-support-igw` |
| Route Table | `aws-cloud-support-public-rt` |
| EC2 Instance | `aws-cloud-support-server` |
| Instance Type | `t3.micro` |
| Operating System | Amazon Linux 2023 |

## Network Architecture

```text
                         Internet
                            |
                            |
                  +-------------------+
                  |  Internet Gateway |
                  | aws-cloud-support |
                  |       -igw        |
                  +---------+---------+
                            |
                    0.0.0.0/0 Route
                            |
                  +---------+---------+
                  |       VPC         |
                  |   10.0.0.0/16     |
                  |                   |
                  |  +-------------+  |
                  |  | Public      |  |
                  |  | Subnet      |  |
                  |  | 10.0.1.0/24 |  |
                  |  |             |  |
                  |  | EC2         |  |
                  |  | 10.0.1.110  |  |
                  |  +-------------+  |
                  +-------------------+

```
## VPC Configuration

The VPC was created using the IPV4 CIDR block:

```text
10.0.0.0/16
```
This  provides the private address space used by the AWS network

configuration details are available in:

```text
config/vpc-configuration.txt
```

## Public Subnet

A public subnet was created within the VPC:

```text
Subnet Name: public-subnet-1
CIDR: 10.0.1.0/24
```

The subnet was configured to automatically assign public IPv4 addresses to resources launched within it.

## Internet Gateway

An Internet Gateway named:

```text
aws-cloud-support-igw
```
was created and attached to the VPC.
The Internet Gateway provides the path between the VPC and the public Internet.

## Route Table

A dedicated route table was created:

```text
aws-cloud-support-public-rt
```
The routing configuration includes:

```text
10.0.0.0/16 → local
0.0.0.0/0    → Internet Gateway
```
The route table was explicitly associated with:

```text
public-subnet-1
```




