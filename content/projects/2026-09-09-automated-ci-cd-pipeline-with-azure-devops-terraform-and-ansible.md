---
title: "Automated CI/CD Pipeline with Azure DevOps, Terraform, and Ansible"
date: 2026-09-09 10:51:40
draft: false
tags: ['Azure DevOps', 'Terraform', 'Ansible', 'CI/CD', 'Azure', 'Ubuntu', 'CentOS', 'DevOps', 'Cloud Engineering', 'Infrastructure as Code']
summary: "Engineered a fully automated, end-to-end CI/CD workflow using Azure DevOps, Terraform, and Ansible, enabling zero-touch deployment of Azure infrastructure and server configuration."
---

Just wrapped up a fantastic architectural challenge: engineering a fully automated, end-to-end CI/CD workflow from scratch using Azure DevOps, Terraform, and Ansible.

Moving from monitoring existing pipelines to architecting this zero-touch deployment was incredibly rewarding. Here is a breakdown of what was built and the roadblocks solved along the way.

## The Architecture

*   Configured a self-hosted Ubuntu Agent in Azure DevOps for secure, fast execution inside a private network.
*   Wrote Terraform to provision Azure infrastructure (VNets, Subnets, VMs) using a remote backend for secure state locking.
*   Leveraged Terraform to dynamically generate RSA SSH keys during deployment.
*   Used pipeline scripting and `jq` to parse Terraform’s JSON outputs, generating a dynamic inventory on the fly.
*   Passed the torch to Ansible to seamlessly configure the newly spun-up servers without hardcoding a single IP or credential.

## The Roadblocks (And How They Were Solved)

### The 403 Forbidden State Error

Early on, the pipeline failed to initialize Terraform. This was traced back to the Azure DevOps Service Connection scope. It was restricted exclusively to the target resource group, meaning the Service Principal lacked the **Storage Blob Data Contributor** role on the subscription level to read the remote state file. Adjusting the RBAC IAM roles fixed it instantly.

### The Python OS Clash

A mix of Ubuntu and CentOS instances were deployed. During Ansible’s fact-gathering phase, the pipeline crashed because CentOS 8.5 shipped with an older Python version that modern Ansible rejected. Instead of manually altering the servers, the pipeline script was modified to use `jq` to filter the Terraform output on the fly, building a targeted inventory of only the Ubuntu servers so the configuration could proceed flawlessly.

## The Takeaways

### Identity is Everything

Understanding the nuances of Service Principals and RBAC is just as critical as writing good infrastructure code.

### Pipelines are Glue

The real magic of CI/CD isn't just running scripts; it's dynamically passing state data (like IPs and keys) from one tool to the next.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3Ashare%3A7503404754996465664)*
