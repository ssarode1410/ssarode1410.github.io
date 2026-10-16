---
title: "Automated Portfolio Deployment with IaC"
date: 2026-05-12 08:29:17
draft: false
tags: ['Terraform', 'AWS', 'Ansible', 'IaC', 'DevOps', 'Linux', 'Continuous Deployment', 'EC2']
summary: "This project details the automated deployment of a personal portfolio website using an Infrastructure as Code (IaC) pipeline. It leverages Terraform for AWS EC2 provisioning and Ansible for Nginx installation and content deployment across multiple environments."
---

Just wrapped up a fantastic hands-on project: deploying my personal portfolio using a fully automated Infrastructure as Code (IaC) pipeline! I used Terraform to provision AWS EC2 instances across Dev, Stage, and Prod environments, and Ansible to automatically install Nginx and push my website files. Everything is tied together with a single deployment script.

## Learning Through Challenges

But as anyone in IT Infrastructure knows, the real learning happens when things break! Here are a few fun errors I ran into and how I solved them:

### The Windows/Linux Translation Trap

*   **Problem:** My `deploy.sh` script initially refused to run, throwing a "file not found" error.
*   **Fix:** Working in WSL means Windows line endings (CRLF) sometimes sneak into Bash scripts. A quick `dos2unix` command converted the hidden characters to Linux format (LF), and the script fired right up.

### Strict Ansible Security

*   **Problem:** Ansible completely ignored my configuration file and couldn't find my servers. Why? Because my WSL-mounted drive gave the folder "world-writable" (777) permissions, which Ansible flags as a security risk.
*   **Fix:** Instead of fighting Windows/Linux mount permissions, I bypassed the config file entirely by explicitly passing my dynamically generated inventory to the command: `ansible-playbook -i inventory/hosts.ini`

### The Parallel SSH Traffic Jam

*   **Problem:** Ansible failed to connect to my newly spun-up EC2 instances. Because Ansible runs tasks in parallel, it triggered multiple interactive "Are you sure you want to continue connecting?" SSH prompts at the exact same time, crashing the automated pipeline.
*   **Fix:** Infrastructure automation should never wait for a human to type "yes." I set `export ANSIBLE_HOST_KEY_CHECKING=False` in my deployment script to automatically accept the new host keys.

### The Classic Extension Typo

*   **Problem:** My final deployment failed because Ansible couldn't find my profile picture.
*   **Fix:** A great reminder that Linux is strictly case and extension-sensitive! My file was a `.png`, but my code was looking for a `.jpg`. A quick syntax update fixed it.

Building this end-to-end really solidified how these tools fit together under the hood. There is nothing quite like hitting 'enter' and watching a pipeline deploy flawlessly from start to finish!

Thanks to Pravesh Sudha for his tutorial and the link to the updated repo: https://lnkd.in/ddJPmE6B

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7459882377566380032)*
