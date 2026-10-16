---
title: "AWS EKS 3-Tier Microservices Application Deployment"
date: 2025-07-26 08:18:32
draft: false
tags: ['AWS', 'EKS', 'Kubernetes', 'Microservices', 'DevOps', 'Helm', 'Instana', 'MongoDB', 'MySQL', 'Node.js', 'Java', 'Python', 'Go', 'PHP', 'RabbitMQ', 'Redis', 'Angular', 'IAM', 'EC2', 'Load Balancer', 'EBS']
summary: "Successfully deployed a complex 3-tier e-commerce microservices application, Stan's Robot Shop, on AWS EKS. This project involved orchestrating 12 microservices, integrating multiple databases, and setting up comprehensive monitoring with Instana, demonstrating advanced cloud-native and DevOps practices."
---

## Successfully Deployed a 3-Tier Microservices Application on AWS EKS

Over the last few days, I challenged myself to deploy a complete e-commerce application on Amazon EKS (Elastic Kubernetes Service), and I'm thrilled to share that I completed it!

This wasn’t just any app—it was the popular **Stan’s Robot Shop**, a cloud-native demo with:
*   12 Microservices
*   2 Databases (MongoDB & MySQL)
*   Integrated Monitoring via Instana
*   Built using a mix of: Node.js, Java, Python, Go, PHP, RabbitMQ, Redis, Angular

### Implementation Steps
Here's what I implemented step-by-step:
1.  **IAM User Setup**: Configured with full permissions to manage EKS and related services.
2.  **EC2-based Bastion Host**: Configured with kubectl, eksctl, Helm & AWS CLI.
3.  **EKS Cluster Creation**: Created a highly available EKS cluster using eksctl.
4.  **OIDC Integration**: Set up IAM OIDC provider for fine-grained IAM roles for service accounts.
5.  **AWS Load Balancer Controller**: Installed via Helm and associated IAM policies to enable Ingress support.
6.  **EBS CSI Driver**: Provisioned dynamic volumes for persistent storage of databases like MongoDB/MySQL.
7.  **Namespace + Helm Deployment**: Deployed Robot Shop in a dedicated namespace with all services running smoothly.
8.  **Ingress + DNS**: Integrated ALB with Ingress, exposing the frontend to the internet.
9.  **Validation + Cleanup**: Accessed the fully running e-commerce site via public DNS and later cleaned up all resources using eksctl delete cluster.

### Key Learnings
*   Gained hands-on experience with real-world Kubernetes concepts like Ingress, ServiceAccounts, OIDC, Helm Charts, StatefulSets & CSI volumes.
*   Understood how to orchestrate 12 microservices across different tech stacks inside EKS.
*   Integrated observability with Instana, allowing full request tracing and monitoring.
*   Realized how crucial IAM fine-tuning and automation are for a production-ready Kubernetes setup on AWS.

This project deepened my understanding of cloud-native architectures and DevOps practices. If you're someone learning Kubernetes, AWS, or DevOps, this is a goldmine to practice end-to-end deployments.

I highly recommend checking out the original walkthrough by Abhishek Veeramalla—it’s beginner-friendly yet powerful.

### Resources
If you're planning to try this out, below are the repo links:
*   **GitHub repo**: https://lnkd.in/dm_bsfKf

Screenshots of the working setup and the Robot Shop in action (Ingress, Helm charts, ALB DNS, etc.) are attached.

Let's connect if you're also learning EKS, DevOps, or preparing for interviews!

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7354787191106998272)*
