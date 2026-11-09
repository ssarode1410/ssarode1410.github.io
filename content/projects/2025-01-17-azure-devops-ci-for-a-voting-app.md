---
title: "Azure DevOps CI for a Voting App"
date: 2025-01-17 07:53:19
draft: false
tags: ["Azure DevOps", "Docker", "Containerization", "CI/CD", "Azure Virtual Machines", "YAML"]
summary: "This project involved implementing the Continuous Integration (CI) pipeline for a multi-service Voting App using Azure DevOps. It leveraged Docker for containerization and Azure Virtual Machines as self-hosted agents."
---

# Azure DevOps CI for a Voting App Project

I successfully completed the Day 14 project from the Azure Zero to Hero Series, focusing on the Continuous Integration (CI) part of a Voting App. This implementation utilized Azure DevOps.

## Implementation Details

*   **Pipelines:** Built three separate pipelines for the `result`, `vote`, and `worker` services.
*   **Pre-pipeline Checks:** Emphasized the importance of studying Dockerfiles to understand container contents and YAML files for correctness before running pipelines.
*   **Agent Pools:** Utilized Azure Virtual Machines as self-hosted Linux agents for the build process.

## Key Learnings

This project provided deep knowledge and practical experience in:

*   **Docker and Dockerfile:** Understanding containerization principles and writing effective Dockerfiles.
*   **Containerization:** The process of packaging applications and their dependencies into containers.
*   **Azure DevOps Platform:** Hands-on experience with setting up and managing CI pipelines.
*   **Multi-Stage Build Method:** Learned the importance and benefits of this technique for optimizing Docker images.

I made many mistakes while running the pipelines, but each one was a valuable learning opportunity.

**Note:** The CD (Continuous Delivery/Deployment) part of this project is coming soon.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3Ashare%3A7285927151285981184)*
