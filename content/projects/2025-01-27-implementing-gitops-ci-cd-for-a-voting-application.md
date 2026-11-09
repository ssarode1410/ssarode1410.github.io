---
title: "Implementing GitOps CI/CD for a Voting Application"
date: 2025-01-27 19:16:35
draft: false
tags: ["Docker", "Azure Container Registry", "Azure Repos", "GitOps", "ArgoCD", "CI/CD", "AKS", "Kubernetes", "Azure"]
summary: "This project details the implementation of a robust CI/CD pipeline for a voting application, leveraging GitOps and ArgoCD to automate deployments to an AKS cluster. It covers the process of updating Docker images from Azure Container Registry to Azure Repos and managing Kubernetes deployments."
---

## CI/CD Implementation for a Voting Application

The Continuous Delivery (CD) aspect of the Voting Application has been a significant undertaking, with considerable effort invested in achieving smooth and reliable operations.

This section primarily focuses on the critical process of updating the latest **Docker image** from **Azure Container Registry** to **Azure Repos** whenever a new change is committed. The seamless integration was largely achieved by leveraging the power of **GitOps** and **ArgoCD**.

### CI/CD Workflow Overview

Here's a brief glimpse into the CI/CD workflow followed:

*   **Initiate Changes**: Developers or users initiate changes in the source code within the repository, which triggers the CI pipeline.
*   **Build and Push**: The Build Stage generates a new container image, which is then uploaded to **Azure Container Registry** via the Push Stage.
*   **Deployment with GitOps**: An **AKS Cluster** is used for deployment. **GitOps** and **ArgoCD** are utilized to manage the application, ensuring the deployment of the latest image to **Kubernetes**.
*   **Update Azure Repos**: An Update Stage is introduced in CI to facilitate the update of the new image to **Azure Repos**, requiring deployment and service files for all services.

This CD phase has significantly enhanced my understanding of **Kubernetes**, **GitOps**, and **ArgoCD**, while also refining my command syntax skills.

A special shoutout to Abhishek Veeramalla for his invaluable contribution to Part 15 of the Azure Zero-to-Hero Series, which, albeit time-consuming, was a rewarding implementation experience. I am always ready to troubleshoot and improve, so feel free to point out any errors.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7289722978605420544)*
