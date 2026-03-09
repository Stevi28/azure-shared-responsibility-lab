# Terraform Azure Windows VM Deployment

This repository provides a complete, production-ready Infrastructure as Code (IaC) setup for deploying a **Windows Virtual Machine** on Azure. It is designed with security and automation as a priority.

## Architecture Overview

The deployment includes the following Azure resources:

* **Resource Group**: Centralized management for all lab components.
* **Networking**: A secure VNet with isolated subnets for workloads and the management layer.
* **Security**: 
    * **Network Security Groups (NSGs)**: Dynamic rules for controlled inbound/outbound traffic.
    * **Azure Key Vault**: Stores VM credentials securely (Usernames/Passwords).
* **Compute**: Windows Server 2022 VM (Standard_B2s, Premium SSD).
* **Access**: **Azure Bastion** host for secure, browser-based RDP access to the VM.
* **Optimization**: Automated daily shutdown schedule at 20:00 (GTB time).

##  Repository Structure

├── bootstrap/          # Initial setup for remote state storage
│   └── main.tf         # Creates the Storage Account & Container
└── main/               # Core infrastructure deployment
    └── main.tf         # VNet, Bastion, Key Vault, VM, and NSGs


## Deployment Guide

### 1. Bootstrap Remote State
Ensure your Terraform state is stored securely in Azure:
1. Navigate to `/bootstrap`.
2. Run `terraform init` and `terraform apply`.

### 2. Deploy Core Infrastructure
1. Navigate to `/main`.
2. Ensure your backend configuration points to the storage created in the bootstrap step.
3. The GitHub Actions pipeline will automatically handle the deployment upon every `git push`.

## Security & Secrets
Sensitive data such as VM admin credentials are managed via **Azure Key Vault**. This setup ensures that secrets are not exposed in plaintext and are handled securely by the Service Principal during deployment.

## Contribution Policy
This repository is protected. All changes must be submitted via **Pull Requests**. 
Direct pushes to the `main` branch are blocked. Please create a feature branch, submit your changes, and request a review before merging.
