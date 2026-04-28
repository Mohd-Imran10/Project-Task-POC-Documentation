# 📘 Bastion Host (Jump Server) – Detailed Guide

## What is a Bastion Host?

A **bastion host** (also called a **jump server / jump box**) is a secure server placed in a public network that acts as a **single entry point** to access systems in a private network.

It is the **only machine exposed to the internet**, while all other servers remain private.


## Simple Definition

A bastion host is a hardened server used to securely access private infrastructure without exposing those systems directly to the internet.


## Where is it Used?

### 1. Cloud Environments

* AWS, Azure, GCP
* Public Subnet → Bastion Host
* Private Subnet → App & DB servers

### 2. Corporate Networks

* Used to access internal company servers securely

### 3. Production Systems

* Banking applications
* Healthcare systems
* Enterprise-grade applications

### 4. DevOps & Infrastructure Management

* SSH into servers (EC2, VMs, Kubernetes nodes)
* Manage infrastructure securely


## How It Works

### Step 1: Connect to Bastion

```bash
ssh user@bastion-public-ip
```

### Step 2: Connect to Private Server

```bash
ssh user@private-ip
```

### Flow:

```
Your Laptop → Bastion → Private Server
```

## Importance of Bastion Host

### 1. Security

* Private servers are not exposed to the internet
* Reduces attack surface

### 2. Controlled Access

* Single entry point
* IP-based and key-based access control

### 3. Centralized Monitoring

* Track login activity
* Useful for auditing

### 4. Compliance

* Required in industries like finance & healthcare

### 5. Simplified Network Design

* No need to expose multiple servers
* Easier to manage access

## Key Characteristics

* Hardened system (minimal software)
* Publicly accessible (controlled access)
* Acts as a gateway/proxy
* Uses SSH or RDP

## Advantages

* Strong security
* Centralized access
* Easy auditing
* Protects private systems

## Disadvantages

* Single point of failure
* Requires maintenance
* Can become a bottleneck

## Modern Alternatives

### AWS Systems Manager (SSM)

* No SSH required
* No open ports

### VPN

* Secure direct access to private network

### Zero Trust Security

* Access based on identity instead of network

## Real-Life Analogy

Think of a bastion host like a **security gate in an office building**:

* You cannot directly access internal offices
* You must pass through security
* Entry is verified and logged

## Summary

* Bastion = Secure entry point
* Used in cloud and enterprise networks
* Protects private servers
* Improves security and control

