---
title: "Custom Jenkins Orchestrator for Terraform and Ansible"
date: 2026-03-24 09:39:24
draft: false
tags: ["Jenkins", "Terraform", "Ansible", "AWS", "CI/CD", "Infrastructure as Code", "Shell Scripting", "jq"]
summary: "This project details building a custom CI/CD pipeline using Jenkins to orchestrate Terraform for AWS EC2 provisioning and Ansible for configuration management. It includes a unique solution for dynamically passing Terraform outputs to Ansible via a custom shell script and jq."
---

# Custom Jenkins Orchestrator for Terraform and Ansible

This project details building a custom CI/CD pipeline using Jenkins to orchestrate Terraform for AWS EC2 provisioning and Ansible for configuration management. It includes a unique solution for dynamically passing Terraform outputs to Ansible via a custom shell script and jq.

## The Challenge

Inspired by a tutorial on orchestrating Terraform and Ansible using Spacelift, I decided to build the exact same orchestrator from absolute scratch using Jenkins. Coming from an IT infrastructure background, I love diving deep into how things actually work under the hood.

I rolled up my sleeves, spun up an Ubuntu WSL environment, and engineered a custom CI/CD pipeline that perfectly bridges the gap between infrastructure provisioning and configuration management.

## How Jenkins Mimics a Dedicated IaC Platform

Here's a breakdown of the pipeline's key stages:

*   **The Provisioning**: Jenkins triggers Terraform to spin up an immutable fleet of AWS EC2 instances.
*   **The "Hook" (My favorite part!)**: A critical challenge was passing dynamic, ever-changing IP addresses from Terraform to Ansible. I wrote a custom shell script utilizing `jq` to parse Terraform's JSON output and generate a live `inventory.ini` file on the fly.
*   **The Configuration**: Jenkins securely injects my `ed25519` SSH keys, passing the dynamic inventory straight to Ansible to configure the new servers instantly.
*   **The Idempotency Test**: For scaling scenarios, the pipeline intelligently reads the state and only configures the newly added instances, ensuring idempotency.

## Real-World Learning Moment

I also built a "Destroy" pipeline to clean up my AWS environment. It immediately failed. Why? Because I was using local state files, and the new Jenkins workspace had no idea what the first workspace had built! This was a perfect, hands-on reminder of why remote backends (like AWS S3) are an absolute must for team-based state management.

## Resources

*   Screenshots of the pipeline are attached to the original post.
*   **Link to the Updated Repo**: [https://lnkd.in/dJKgxH-V](https://lnkd.in/dJKgxH-V)

## Acknowledgements

A big thanks to Abhishek Veeramalla for the original tutorial and his repository that inspired this project.

## Open to Work & Community Question

I’m currently exploring new opportunities in DevOps and Cloud Engineering. If your team is looking for someone who loves connecting the dots between legacy infrastructure and modern cloud automation, let's connect!

**Question for the community**: When you are gluing Terraform and Ansible together, what is your go-to orchestrator? Jenkins, GitHub Actions, GitLab CI, or a specialized tool? Let me know below!

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7442143018180321280)*
