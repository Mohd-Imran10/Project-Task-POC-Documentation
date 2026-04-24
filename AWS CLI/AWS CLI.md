### AWS CLI

### What is AWS CLI?

The AWS Command Line Interface is a tool that lets you interact with AWS services directly from your terminal instead of using the AWS Management Console.

In simple terms:

It converts your commands → AWS API calls

Lets you automate infrastructure

Widely used in DevOps, scripting, CI/CD

### Why AWS CLI is Important

No need to click in UI (faster)

Can automate full infrastructure

Works well with shell scripts, pipelines


# AWS VPC Setup Using AWS CLI

## Overview

This document describes the step-by-step process of creating and configuring AWS networking components using AWS CLI.

### How to Configure AWS CLI
Install (AWS CLI v2)

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

## 1. VPC Creation

VPC_ID=$(aws ec2 create-vpc \
  --cidr-block 10.0.0.0/16 \
  --query 'Vpc.VpcId' \
  --output text)

  VPC: 10.0.0.0/16

![preview](./vpc2.PNG)


## 2. Internet Gateway (IGW)

IGW_ID=$(aws ec2 create-internet-gateway \
  --query 'InternetGateway.InternetGatewayId' \
  --output text)

aws ec2 attach-internet-gateway \
  --vpc-id vpc-09c47e07a1b5ecb32 \
  --internet-gateway-id $IGW_ID

  ![preview](./igw2.PNG)

## 3. Subnets

### Public Subnet

PUB_SUBNET=$(aws ec2 create-subnet \
  --vpc-id vpc-09c47e07a1b5ecb32 \
  --cidr-block 10.0.1.0/24 \
  --availability-zone us-east-1b \
  --query 'Subnet.SubnetId' \
  --output text)

![preview](./subnet3.PNG)

### Private Subnet

PRIV_SUBNET=$(aws ec2 create-subnet \
  --vpc-id vpc-09c47e07a1b5ecb32 \
  --cidr-block 10.0.2.0/24 \
  --availability-zone us-east-1b \
  --query 'Subnet.SubnetId' \
  --output text)

![preview](./subnet3.PNG)


## 4. Route Tables

### Public Route Table


PUB_RT=$(aws ec2 create-route-table \
  --vpc-id vpc-09c47e07a1b5ecb32 \
  --query 'RouteTable.RouteTableId' \
  --output text)

aws ec2 create-route \
  --route-table-id $PUB_RT \
  --destination-cidr-block 0.0.0.0/0 \
  --gateway-id igw-06233162c01407607

aws ec2 associate-route-table \
  --subnet-id subnet-082a5864d9bf4f4d7 \
  --route-table-id $PUB_RT

![preview](./rt2.PNG)
![preview](./rtpubsub.PNG)

### Private Route Table

PRIV_RT=$(aws ec2 create-route-table \
  --vpc-id $VPC_ID \
  --query 'RouteTable.RouteTableId' \
  --output text)

aws ec2 associate-route-table \
  --subnet-id subnet-09cb76c2122b8e3e5 \
  --route-table-id $PRIV_RT

![preview](./rtpvt2.PNG)
![preview](./rtpvtsub.PNG)


## 5. Security Groups

### SSH Security Group


SG_SSH=$(aws ec2 create-security-group \
  --group-name ssh-sg \
  --description "SSH access" \
  --vpc-id vpc-09c47e07a1b5ecb32 \
  --query 'GroupId' \
  --output text)

aws ec2 authorize-security-group-ingress \
  --group-id $SG_SSH \
  --protocol tcp \
  --port 22 \
  --cidr 0.0.0.0/0

### HTTP Security Group


SG_HTTP=$(aws ec2 create-security-group \
  --group-name http-sg \
  --description "HTTP access" \
  --vpc-id vpc-09c47e07a1b5ecb32 \
  --query 'GroupId' \
  --output text)

aws ec2 authorize-security-group-ingress \
  --group-id $SG_HTTP \
  --protocol tcp \
  --port 80 \
  --cidr 0.0.0.0/0

![preview](./SG2.PNG)


## 6. Network ACL (NACL)


NACL_ID=$(aws ec2 create-network-acl \
  --vpc-id vpc-09c47e07a1b5ecb32 \
  --query 'NetworkAcl.NetworkAclId' \
  --output text)

### Inbound Rules

aws ec2 create-network-acl-entry \
--network-acl-id acl-0f3ae9c8a29f961a3 \
--rule-number 100 \
--protocol tcp \
--port-range From=80,To=80 \
--cidr-block 0.0.0.0/0 \
--rule-action allow \
--ingres

aws ec2 create-network-acl-entry \
--network-acl-id acl-0f3ae9c8a29f961a3 \
--rule-number 110 \
--protocol tcp \
--port-range From=22,To=22 \
--cidr-block 0.0.0.0/0 \
--rule-action allow \
--ingres

![preview](./nacl.PNG)

### Outbound Rules

aws ec2 create-network-acl-entry \
--network-acl-id acl-0f3ae9c8a29f961a3 \
--rule-number 100 \
--protocol -1 \
--cidr-block 0.0.0.0/0 \
--rule-action allow \
--egress

![preview](./nacl1.PNG)


## 7. NACL Association

Aaws ec2 replace-network-acl-association \
  --association-id aclassoc-03eb0d6d0c40fd9d4 \
  --network-acl-id acl-0f3ae9c8a29f961a3

    "NewAssociationId": "aclassoc-000326f7edc5a9bc0"

![preview](./nacl2.PNG)


## Key Learnings

* Security Groups are stateful
* NACLs are stateless
* Public subnet requires IGW route
* CLI automation reduces manual errors


## Conclusion

A complete AWS network infrastructure was successfully created using AWS CLI. This setup is ready for EC2 deployment and real-world applications.
