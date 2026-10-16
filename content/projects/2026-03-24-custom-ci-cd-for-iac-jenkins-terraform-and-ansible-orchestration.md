---
title: "Custom CI/CD for IaC: Jenkins, Terraform, and Ansible Orchestration"
date: 2026-03-24 09:39:24
draft: false
tags: ['Jenkins', 'Terraform', 'Ansible', 'AWS', 'CI/CD', 'IaC', 'Automation', 'Shell Scripting', 'jq']
summary: "This project details the creation of a custom CI/CD pipeline using Jenkins to orchestrate Terraform for AWS EC2 provisioning and Ansible for configuration management. It highlights a clever solution for dynamic inventory generation and a key learning about remote state management."
---

# Infrastructure Orchestration in Jenkins

Inspired by a tutorial on orchestrating Terraform and Ansible with Spacelift, I took on the challenge to build the same orchestrator from scratch using Jenkins.

With a background in IT infrastructure, I enjoy understanding the underlying mechanisms of technology. This led me to develop a custom CI/CD pipeline in an Ubuntu WSL environment, designed to seamlessly integrate infrastructure provisioning and configuration management.

## Mimicking an IaC Platform with Jenkins

Here is how I made Jenkins mimic a dedicated IaC platform:

*   **The Provisioning**: Jenkins initiates Terraform to provision an immutable fleet of AWS EC2 instances.
*   **The Hook (Dynamic Inventory)**: A key challenge was passing dynamic IP addresses from Terraform to Ansible. I solved this by writing a custom shell script that uses `jq` to parse Terraform's JSON output and generate a live `inventory.ini` file on the fly.
*   **The Configuration**: Jenkins securely injects ed25519 SSH keys and passes the dynamic inventory directly to Ansible for instant server configuration.
*   **Idempotency**: For scaling, the pipeline intelligently reads the state to ensure only newly added instances are configured.

## Real-World Learning Moment: Remote State Management

I also developed a "Destroy" pipeline to clean up the AWS environment, which initially failed. This was due to using local state files, meaning the new Jenkins workspace lacked knowledge of the previous build. This experience served as a crucial reminder of the necessity of remote backends (such as AWS S3) for robust, team-based state management.

The updated repository can be found [here](https://lnkd.in/dJKgxH-V).

Special thanks to Abhishek Veeramalla for the inspiring original tutorial and repository.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7442143018180321280)*
