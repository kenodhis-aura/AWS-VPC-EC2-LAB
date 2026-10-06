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

## Security Group

A security group named:

```text
aws-cloud-support-sg
```
was created for the EC2 instance.

SSH access was restricted to the administrator's public IP address using:

```text
TCP/22
Source: <administrator IP>/32
```
Outbound connectivity was permitted for the instance.

## EC2 Deployment

An Amazon Linux 2023 EC2 instance was deployed using:

```text
Instance Name: aws-cloud-support-server
Instance Type: t3.micro
Private IP: 10.0.1.110
Public IP: 51.20.84.127
```
The instance was successfully launched and passed its AWS status checks.

## SSH Connectivity

SSH access was established successfully using the configured EC2 key pair.

The instance reported:

```text
Amazon Linux 2023
```
Hostname:

```text
ip-10-0-1-110.eu-north-1.compute.internal
```

# Connectivity Testing

## Internet Connectivity

The instance successfully reached Google's public DNS server:

```text
ping -c 4 8.8.8.8
```
Result:
```text
4 packets transmitted, 4 received
0% packet loss
```

## DNS Resolution

DNS Resolution was validated using:

```text
ping -c 4 www.google.com
```

Result:

```text
4 packets transmitted, 4 received
0% packet loss
```

## HTTPS Connectivity

HTTPS connectivity to AWS was tested with:

```text
curl -I https://aws.amazon.com
```

Result:

```text
HTTP/2 200
```
Google HTTPS connectivity was also tested:

```text
curl -I https://google.com
```

Result:

```text
HTTP/2 301
```

The response redirected to:

```text
https://www.google.com/
```

## AWS Instance Metadata

The EC2 Instance Metadata Service was queried using IMDSv2
Verified information included:

```text
Instance ID: i-04f0cc7a881fd4054
Private IPv4: 10.0.1.110
Public IPv4: 51.20.84.127
Region: eu-north-1
```

## Validation Results

The following components were successfully validated:
- VPC creation
- IPv4 CIDR addressing
- Public subnet creation
- Internet Gateway attachment
- Default Internet route
- Subnet-to-route-table association
- Security group configuration
- EC2 deployment
- SSH connectivity
- Internet connectivity
- DNS resolution
- HTTPS connectivity
- EC2 instance metadata access
Detailed test output is available in:

```text
test-results.txt
```

## Screenshots

Evidence Captured during the implementation is stored under:

```text
screenshots/
```
The screenshots demonstrate:
- VPC creation
- Subnet configuration
- Internet Gateway attachment
- Route table configuration
- Security group configuration
- EC2 deployment
- EC2 connectivity testing


  ## Skill Demonstrated
  
AWS VPC networking
IPv4 addressing and CIDR
Subnetting
Route tables
Internet Gateway configuration
AWS security groups
EC2 deployment
Linux administration
SSH
DNS troubleshooting
Network connectivity testing
AWS Instance Metadata Service
Layered network troubleshooting

## Key Outcomes

Successfully designed, deployed, and validated a functional AWS VPC environment with a public subnet and EC2 workload.
The project demonstrates practical understanding of how AWS networking components work together to provide connectivity from an EC2 instance to the Internet.

## Conclusion

This lab provided hands-on experience building an AWS network environment from the VPC layer through to an operational EC2 instance.
The deployment was validated using Linux networking tools and real connectivity tests, providing practical evidence of AWS networking, troubleshooting, and cloud infrastructure fundamentals.





