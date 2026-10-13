---
title: "Building a GitOps Microservices Architecture on AWS"
date: 2026-06-27 08:09:49
draft: false
tags: ['AWS', 'EKS', 'Docker', 'Terraform', 'GitHub Actions', 'ArgoCD', 'Prometheus', 'Grafana', 'Kubernetes', 'DevOps', 'GitOps', 'Microservices']
summary: "This project details the implementation of an end-to-end DevOps Microservices architecture on AWS, leveraging a GitOps workflow with Terraform, AWS EKS, GitHub Actions, and ArgoCD. It highlights key challenges encountered during deployment and their practical solutions."
---

I recently deployed a complete, end-to-end DevOps Microservices architecture on AWS. The journey wasn't without its challenges, and it was through troubleshooting that the most significant learning occurred.

As a firm believer in "learning by building," I implemented a full GitOps workflow from a completely blank slate.

## Tech Stack Implemented

*   **Infrastructure as Code:** Terraform
*   **Cloud & Containerization:** AWS EKS & Docker
*   **CI/CD & GitOps:** GitHub Actions & ArgoCD
*   **Observability Stack:** Prometheus & Grafana

While the architecture looked robust on paper, Kubernetes quickly presented several hurdles. Below are the three biggest roadblocks encountered and their respective solutions.

## Key Roadblocks and Solutions

### Roadblock 1: Pipeline Passed, GitOps Failed

My GitHub Actions CI pipeline reported success, indicating "Everything up-to-date," yet ArgoCD on the cluster threw an `InvalidImageName` error.

**The Fix:** The issue stemmed from an `<AWS_ACCOUNT_ID>` placeholder left in my YAML manifests. The `sed` command in the pipeline failed to match the regex required to update the image tag.
**Lesson Learned:** Always meticulously verify the targets and patterns your automation scripts are scanning against.

### Roadblock 2: The Dreaded CrashLoopBackOff

My authentication microservice repeatedly crashed immediately after startup.

**The Fix:** Investigation revealed that while the PostgreSQL pod was running, its database was entirely empty. The microservices couldn't initialize without their required database schemas. A manual Kubernetes restore job was executed to initialize the DB tables, which subsequently stabilized the entire cluster.

### Roadblock 3: Pods Stuck in "Pending" (Insufficient Capacity)

Attempting to run the database restore job, Kubernetes refused to schedule it, reporting a "Too many pods" error.

**The Fix:** AWS EC2 instances have strict hard limits on the number of pods they can host, determined by attached Network Interfaces. Between the observability stack and system pods, my single node had reached its capacity. The solution involved temporarily scaling down the frontend deployment to 0, running the restore job in the newly freed slot, and then scaling the frontend back up.
**Lesson Learned:** Continuous monitoring of node capacity is crucial.

A massive shoutout to Vishakha Sadhwani for providing the phenomenal baseline architecture and tutorial that inspired this project. The contributions of creators like her are invaluable to the DevOps community.

I have thoroughly documented this journey, rectified the manifest bugs, and pushed the updated, working configuration to GitHub. Feel free to explore, fork, and experiment with the repository: https://lnkd.in/d-CsejtP

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7476547320860385280)*
