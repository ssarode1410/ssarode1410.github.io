---
title: "End-to-End GitOps Project with AWS EKS + ArgoCD"
date: 2025-07-17 23:08:40
draft: false
tags: ["GitOps", "AWS EKS", "ArgoCD", "Golang", "Docker", "Kubernetes", "eksctl", "Nginx Ingress Controller", "Helm", "GitHub Actions", "CI/CD", "Cloud-Native"]
summary: "This project details the implementation of an end-to-end GitOps pipeline for a Golang web application, leveraging AWS EKS for Kubernetes orchestration and ArgoCD for continuous deployment. It covers the full CI/CD spectrum from Dockerization and Kubernetes manifests to Helm charts and GitHub Actions."
---

# End-to-End GitOps Project with AWS EKS + ArgoCD

Just completed a real-world GitOps pipeline for a Golang web app using AWS EKS and ArgoCD—and I’m sharing everything you need to get it running smoothly (plus a few hiccups I hit along the way).

This hands-on DevOps project covers:

*   **Multi-stage Dockerfile** for Golang app
*   **Kubernetes Manifests**: Deployment, Service, Ingress
*   **EKS Cluster Setup** using eksctl
*   **Nginx Ingress Controller** for custom domains
*   **Helm Charts** for multi-environment GitOps
*   **CI via GitHub Actions** (Build → Test → Push to DockerHub)
*   **CD via ArgoCD** to auto-deploy on EKS

## Mistakes I Made (and Lessons Learned):

*   Tried to git push for 15 mins before realizing I hadn't set a remote repo.
*   Static code analysis still shows red — if you know how to fix it, I’m all ears!
*   When testing manually on Kubernetes without CI/CD, I changed Service type to NodePort but still couldn’t access the app — suggestions welcome!

## Ideal for:

*   DevOps learners & job seekers
*   CI/CD + GitOps practice
*   Cloud-native app deployment experience

## Resources:

*   **GitHub Repo**: [https://lnkd.in/dWjTW6mE](https://lnkd.in/dWjTW6mE)
*   **Full Walkthrough**: [https://lnkd.in/dPv32wAJ](https://lnkd.in/dPv32wAJ)

Big thanks to Abhishek Veeramalla for this excellent base project!

Let’s learn, fail, fix, and grow together.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7351749711881547776)*
