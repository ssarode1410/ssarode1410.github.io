---
title: "GitHub Actions with Self-Hosted AWS EC2 Runner"
date: 2025-04-21 06:15:03
draft: false
tags: ["GitHub Actions", "AWS EC2", "Self-Hosted Runner", "DevOps", "Automation", "Ubuntu"]
summary: "Implemented a GitHub Actions workflow using a self-hosted runner provisioned on an AWS EC2 instance running Ubuntu, demonstrating custom CI/CD execution."
---

## Project Overview

This project involved exploring GitHub Actions with a self-hosted runner for the first time. A big thanks to Abhishek Veeramalla for the clear explanation and hands-on demo that inspired this implementation.

## Implementation Steps

Here’s a quick breakdown of the steps taken:

*   **Provisioned an EC2 Instance on AWS** running **Ubuntu OS** to act as a self-hosted runner.
*   **Installed the GitHub runner** on the Instance by following the setup guide available in the repository’s runner settings.
*   **Updated the GitHub Actions workflow** by modifying the `runs-on` field to `self-hosted`. This ensures the workflow executes on our EC2 instance instead of GitHub-hosted runners.
*   **Pushed the code changes**, monitored the status on the GitHub Actions dashboard (observing pending and success states), and validated execution directly on the EC2 instance.

## Conclusion

Excited to explore more automation possibilities with self-hosted runners!

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7319966881346420736)*
