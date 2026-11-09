---
title: "Debugging Infrastructure Orchestration with Spacelift, Terraform, and Ansible"
date: 2026-03-24 05:50:12
draft: false
tags: ["Spacelift", "Terraform", "Ansible", "AWS", "DevOps", "CI/CD", "Infrastructure as Code", "Debugging", "GitOps"]
summary: "Successfully orchestrated infrastructure provisioning and configuration using Spacelift, Terraform, and Ansible, debugging complex issues related to runner environments, deprecated AMIs, and SSH security to deploy automated EC2 instances."
---

I spent the day deep-diving into Infrastructure Orchestration with Spacelift, blending Terraform (provisioning) with Ansible (configuration).

What started as a straightforward tutorial quickly evolved into a debugging masterclass. This hands-on experience provided invaluable insights into how these tools interact within a live CI/CD runner environment, especially when things don't go as planned.

### Technical Hurdles Overcome

Here are the four significant technical challenges I faced and successfully navigated:

*   **The Case of the Missing `jq`**: My Spacelift hook attempted to use `jq` for parsing Terraform output, but the Spacelift runner lacked its installation. Instead of modifying container images, I refactored the script to leverage standard Linux text manipulation tools like `tr`, which are guaranteed to be present.
*   **Infrastructure Code "Rot"**: The tutorial's code, recorded ten months prior, specified Ubuntu 20.04. However, AWS had deprecated these free public images, leading to "0 results" errors. I modernized the Terraform data blocks to target Ubuntu 24.04 LTS (Noble), adapting to dynamic naming convention changes and correcting a subtle "nobel/noble" typo.
*   **Strict SSH Security**: The Ansible run encountered a cryptic SSH connection error. SSH was refusing to use the private key due to overly permissive file permissions (0777). I identified that Spacelift resets the runner environment between the 'Plan' and 'Apply' phases. To resolve this, I introduced a new hook in the 'Before Apply' phase to enforce `chmod 600` just before the Ansible run, allowing SSH to proceed.
*   **Dynamic Inventory Orchestration**: After Terraform successfully provisioned the instances, I orchestrated the state transfer to dynamically pass the newly acquired IP addresses to Ansible's inventory immediately before its execution.

### The End Result

The project culminated in four freshly provisioned, automated EC2 instances, each running a perfectly configured `htop` dashboard.

A huge thanks to Abhishek Veeramalla for the original tutorial and repository that provided an excellent foundation. You can explore my fully debugged and updated forked repository, which includes modernized Terraform code for Ubuntu 24.04 and the fixed Spacelift hooks, here: [https://lnkd.in/dJKgxH-V](https://lnkd.in/dJKgxH-V)

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7442085338300182528)*
