---
title: "Mastering Infrastructure Orchestration: Debugging Spacelift, Terraform, and Ansible"
date: 2026-03-24 05:50:12
draft: false
tags: ['Spacelift', 'Terraform', 'Ansible', 'AWS', 'DevOps', 'CI/CD', 'Infrastructure as Code', 'Debugging', 'GitOps']
summary: "This project details a deep dive into infrastructure orchestration using Spacelift, Terraform, and Ansible, focusing on overcoming significant debugging challenges in a live CI/CD environment. The author successfully provisioned and configured four automated AWS EC2 instances, demonstrating robust problem-solving skills."
---

I spent the day deep-diving into Infrastructure Orchestration with Spacelift, blending Terraform (provisioning) with Ansible (configuration). It was supposed to be a straightforward tutorial, but the real learning happened when things broke! This wasn't just copy-pasting code; it turned into a debugging masterclass that gave me amazing hands-on experience with how these tools interact in a live CI/CD runner environment.

## Technical Hurdles Overcome

Here is how the day went, including the four big technical hurdles I faced and overcame:

1.  **The Case of the Missing `jq`**: My Spacelift hook was trying to use `jq` to parse Terraform output, but the Spacelift runner didn't have it installed. Instead of messing with container images, I refactored the script to use standard Linux text manipulation tools (`tr`) that are guaranteed to be present. Problem solved!
2.  **Infrastructure Code "Rot"**: The tutorial code (recorded 10 months ago) was looking for Ubuntu 20.04, but AWS deprecated those free public images. AWS was returning "0 results" errors. I modernized the Terraform data blocks to grab Ubuntu 24.04 LTS (Noble) instead, navigated dynamic naming convention changes, and even fixed a sneaky `nobel`/`noble` typo along the way!
3.  **Strict SSH Security**: The Ansible run was failing with a cryptic SSH connection error. SSH was refusing to use the private key because the file permissions were too open (0777). I realized Spacelift resets the runner environment between the 'Plan' and 'Apply' phases. I added a fresh hook to the Before Apply phase to force a `chmod 600` right before the run, and SSH finally let Ansible in.
4.  **Dynamic Inventory Orchestration**: Once Terraform built the instances, I successfully orchestrated the state transfer so that the fresh IP addresses were dynamically passed to Ansible's inventory right before the run.

## The End Result

Four freshly provisioned, automated EC2 instances with a perfectly running `htop` dashboard! (See the screenshots below)

A huge thanks to Abhishek Veeramalla for the original tutorial and repository that gave me this great foundation. You can check out my fully debugged and updated forked repo below, where I modernized the Terraform code for Ubuntu 24.04 and added the fixed Spacelift hooks:

[https://lnkd.in/dJKgxH-V](https://lnkd.in/dJKgxH-V)

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7442085338300182528)*
