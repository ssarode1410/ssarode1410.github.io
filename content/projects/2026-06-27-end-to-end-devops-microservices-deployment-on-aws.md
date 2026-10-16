---
title: "End-to-End DevOps Microservices Deployment on AWS"
date: 2026-06-27 08:09:49
draft: false
tags: ['AWS', 'DevOps', 'Microservices', 'Terraform', 'EKS', 'Docker', 'GitHub Actions', 'ArgoCD', 'Prometheus', 'Grafana', 'Kubernetes', 'GitOps', 'CI/CD']
summary: "This project details the deployment of a complete, end-to-end DevOps Microservices architecture on AWS, leveraging a full GitOps workflow. It highlights the challenges encountered with Kubernetes, CI/CD, and infrastructure provisioning, along with their practical solutions."
---

Just deployed a complete, end-to-end DevOps Microservices architecture on AWS! But here’s the real story: it didn't work on the first try. And that’s exactly where the actual learning happened.

I’m a firm believer in "learning by building," so I rolled up my sleeves to implement a full GitOps workflow. Here is the tech stack I provisioned from a completely blank slate:

## Project Overview: End-to-End DevOps Microservices on AWS

I embarked on a journey to implement a full GitOps workflow, provisioning a complete end-to-end DevOps Microservices architecture on AWS from a blank slate.

### Tech Stack

*   **Infrastructure as Code:** Terraform
*   **Cloud & Containerization:** AWS EKS & Docker
*   **CI/CD & GitOps:** GitHub Actions & ArgoCD
*   **Observability Stack:** Prometheus & Grafana

Everything looked great on paper, but Kubernetes humbled me quickly. Here are the 3 biggest roadblocks I hit and exactly how I fixed them:

### Roadblocks and Solutions

#### Error 1: The Pipeline Passed, but GitOps Failed

My GitHub Actions CI pipeline succeeded and said "Everything up-to-date," but ArgoCD threw an `InvalidImageName` error on the cluster.

**The Fix:** I left an `<AWS_ACCOUNT_ID>` placeholder in my YAML manifests. The `sed` command in my pipeline couldn't match the regex to update the image tag! Lesson learned: Always verify what your automation scripts are actually scanning against.

#### Error 2: The Dreaded CrashLoopBackOff

My auth microservice kept crashing immediately after starting up.

**The Fix:** My PostgreSQL pod was running, but it was completely empty! The microservices couldn't start because their database schemas didn't exist yet. Running a manual Kubernetes restore job to initialize the DB tables stabilized the entire cluster.

#### Error 3: Pods stuck in "Pending" (Insufficient Capacity)

When I tried to run that restore job, Kubernetes refused to schedule it, throwing a "Too many pods" error.

**The Fix:** AWS EC2 instances have strict hard limits on the number of pods they can run based on attached Network Interfaces. Between my observability stack and system pods, my single node was full! I temporarily scaled my frontend deployment down to 0, ran the restore job in the freed-up slot, and brought the frontend back up. Always monitor your node capacity!

A massive shoutout to Vishakha Sadhwani for providing the phenomenal baseline architecture and tutorial for this project. It’s creators like her that make the DevOps community so incredibly strong.

I’ve documented this whole journey, fixed the manifest bugs, and pushed my updated, working configuration to GitHub. Feel free to check it out, fork it, and break it yourself! [GitHub Repository](https://lnkd.in/d-CsejtP)

What was the toughest Kubernetes or CI/CD bug you had to squash recently? Let me know in the comments!

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7476547320860385280)*
