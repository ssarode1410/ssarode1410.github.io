---
title: "End-to-End CI/CD Pipeline with GitHub Actions, Terraform, and AWS EKS"
date: 2026-05-31 06:24:02
draft: false
tags: ['GitHub Actions', 'Terraform', 'AWS EKS', 'CI/CD', 'DevOps', 'Docker', 'SonarQube', 'Trivy', 'GitLeaks', 'Maven', 'AWS']
summary: "This project details the engineering and deployment of a robust, end-to-end CI/CD pipeline from scratch, leveraging GitHub Actions, Terraform, and AWS EKS for infrastructure automation, security scanning, containerization, and orchestration."
---

Just engineered and deployed an end-to-end CI/CD pipeline from scratch using GitHub Actions, Terraform, and AWS EKS!

Transitioning to DevOps means moving beyond tutorials—it’s about hands-on architecture and troubleshooting. I built a robust deployment pipeline encompassing infrastructure automation, security scanning, containerization, and orchestration.

## The Architecture
To prevent resource contention (like OOM crashes), I provisioned a distributed EC2 setup:
- **EKS Management Server**: Terraform & AWS CLI for cluster build.
- **SonarQube Server**: Dockerized static code analysis.
- **GitHub Runner**: A persistent, self-hosted runner.

## The Workflow
- **Compile & Test**: Maven lifecycle phases.
- **Security**: Native Trivy & GitLeaks execution.
- **Code Quality**: SonarQube quality gates.
- **Containerization**: Docker build/push.
- **Deployment**: Dynamic EKS deployment via AWS CLI.

## The "Gotchas" I Fixed
- **apt-key Deprecation**: Updated Trivy install to modern `gpg --dearmor` keyring to prevent pipeline crashes.
- **Runner Quirks**: Added `--update` flags for AWS CLI installs on the persistent runner.
- **Artifact Handoffs**: Implemented explicit upload/download actions to pass `.jar` files between isolated jobs.

I’ve documented the setup, modernized configs, and fixed dependencies here: [Project Documentation](https://lnkd.in/d3QusDEw)

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7466736225249419265)*
