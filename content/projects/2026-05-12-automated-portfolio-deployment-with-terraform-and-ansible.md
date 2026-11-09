---
title: "Automated Portfolio Deployment with Terraform and Ansible"
date: 2026-05-12 08:29:17
draft: false
tags: ["Terraform", "Ansible", "AWS", "EC2", "Nginx", "Infrastructure as Code", "DevOps", "Linux", "Continuous Deployment"]
summary: "This project details the creation of a fully automated Infrastructure as Code (IaC) pipeline to deploy a personal portfolio website. It leverages Terraform for provisioning AWS EC2 instances across multiple environments and Ansible for configuration management and application deployment."
---

# Automated Portfolio Deployment with Terraform and Ansible

I recently completed a hands-on project focused on deploying my personal portfolio using a fully automated Infrastructure as Code (IaC) pipeline. This setup leverages Terraform to provision AWS EC2 instances across Development, Staging, and Production environments. Ansible is then used to automatically install Nginx and deploy my website files, with the entire process orchestrated by a single deployment script.

As is often the case in IT Infrastructure, the most significant learning experiences come from troubleshooting issues. Here are a few challenges I encountered and their solutions:

## Troubleshooting Common IaC Pipeline Errors

### The Windows/Linux Translation Trap

*   **Problem**: My `deploy.sh` script initially failed to run, throwing a "file not found" error.
*   **Fix**: When working in WSL, Windows line endings (CRLF) can sometimes inadvertently sneak into Bash scripts. A quick `dos2unix` command converted these hidden characters to the Linux format (LF), allowing the script to execute successfully.

### Strict Ansible Security

*   **Problem**: Ansible completely ignored my configuration file and couldn't locate my servers. The root cause was that my WSL-mounted drive assigned "world-writable" (777) permissions to the folder, which Ansible flags as a security risk.
*   **Fix**: Instead of attempting to modify Windows/Linux mount permissions, I bypassed the config file entirely. I explicitly passed my dynamically generated inventory to the command: `ansible-playbook -i inventory/hosts.ini`.

### The Parallel SSH Traffic Jam

*   **Problem**: Ansible failed to connect to my newly provisioned EC2 instances. Because Ansible runs tasks in parallel, it triggered multiple interactive "Are you sure you want to continue connecting?" SSH prompts simultaneously, which crashed the automated pipeline.
*   **Fix**: Infrastructure automation should never require human intervention for prompts like "yes." I resolved this by setting `export ANSIBLE_HOST_KEY_CHECKING=False` in my deployment script to automatically accept new host keys.

### The Classic Extension Typo

*   **Problem**: My final deployment failed because Ansible couldn't find my profile picture.
*   **Fix**: This was a great reminder that Linux is strictly case and extension-sensitive! My file was a `.png`, but my code was looking for a `.jpg`. A quick syntax update resolved the issue.

Building this end-to-end pipeline truly solidified my understanding of how these tools integrate. There's immense satisfaction in hitting 'enter' and watching a pipeline deploy flawlessly from start to finish!

Special thanks to Pravesh Sudha for his tutorial and the link to the updated repository: https://lnkd.in/ddJPmE6B

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7459882377566380032)*
