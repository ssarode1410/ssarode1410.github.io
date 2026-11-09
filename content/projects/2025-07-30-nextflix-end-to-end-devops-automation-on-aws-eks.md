---
title: "Nextflix: End-to-End DevOps Automation on AWS EKS"
date: 2025-07-30 20:52:47
draft: false
tags: ["AWS EKS", "Terraform", "Jenkins", "ArgoCD", "Prometheus", "Grafana", "GitOps", "Kubernetes", "CI/CD", "Cloud-Native", "Infrastructure as Code"]
summary: "This project involved building and deploying a Netflix-like streaming application, Nextflix, on AWS EKS. It showcased end-to-end DevOps automation, leveraging tools like Terraform, Jenkins, ArgoCD, Prometheus, and Grafana for infrastructure, CI/CD, and monitoring."
---

# Nextflix: End-to-End DevOps Automation on AWS EKS

This project wasn’t just about building a Netflix clone; it was about understanding how real-world DevOps works at scale. From designing infrastructure to debugging tricky deployment issues, this project delivered deep hands-on learning.

## Project Highlights

*   Built and deployed Nextflix, a Netflix-like streaming app.
*   Infrastructure provisioned using **Terraform** on **AWS EKS**.
*   **GitOps**-based deployment using **ArgoCD**.
*   **CI/CD** pipeline with **Jenkins**.
*   Monitoring integrated via **Prometheus** + **Grafana**.

## Challenges We Faced & Lessons Learned

*   **Issue:** Encountered "Too many pods" error on t3.medium nodes.
    *   **Solution:** Solved by increasing instance size in the managed node group for higher pod capacity.
*   **Issue:** Terraform "Unsupported argument" errors due to version mismatch.
    *   **Solution:** Learned to match `terraform-aws-eks` module v21+ with AWS provider ≥ v5.0.0.
*   **Issue:** ArgoCD and monitoring tools failed to deploy due to pod capacity limits.
    *   **Solution:** Identified the role of CNI, ENI IP limits, and how instance sizing impacts it (resized the instance to t3.xlarge).

Still, the Nextflix application is not showing static images; suggestions to correct them are always welcome.

## Key Takeaways

*   Cloud-native projects demand deep attention to infrastructure limits.
*   Scaling isn’t just about replicas — it’s also about networking & node design.
*   Real DevOps is all about observing, debugging, and iterating.

## Stack Used

*   **Infrastructure as Code:** Terraform
*   **Container Orchestration:** AWS EKS (Kubernetes)
*   **CI/CD:** Jenkins
*   **GitOps:** ArgoCD
*   **Monitoring:** Prometheus, Grafana
*   **Application:** Nextflix (custom streaming app)

Every tool and every error taught something new. If you're exploring DevOps or cloud-native deployments, let's connect and learn together.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7356426556967108609)*
