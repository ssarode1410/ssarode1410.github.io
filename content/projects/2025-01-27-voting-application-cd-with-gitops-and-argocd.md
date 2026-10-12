---
title: "Voting Application CD with GitOps and ArgoCD"
date: 2025-01-27 19:16:35
draft: false
tags: ['CI/CD', 'Docker', 'Azure Container Registry', 'Azure Repos', 'GitOps', 'ArgoCD', 'AKS', 'Kubernetes']
summary: "Implemented a continuous deployment pipeline for a Voting Application, leveraging GitOps and ArgoCD to deploy Docker images from Azure Container Registry to an Azure Kubernetes Service (AKS) cluster."
---

The Continuous Deployment (CD) phase of the Voting Application has been a significant undertaking, focusing on achieving smooth and efficient operations. This involved establishing a crucial process for updating the latest Docker image from Azure Container Registry to Azure Repos whenever new changes are committed. The seamless integration was largely achieved by leveraging **GitOps** and **ArgoCD**.

### CI/CD Workflow

Here's a brief overview of the CI/CD workflow implemented:

*   **Initiate Changes**: Developers or users initiate changes in the source code within the repository, which triggers the Continuous Integration (CI) pipeline.
*   **Build and Push**: The Build Stage generates a new container image, which is then uploaded to **Azure Container Registry** via the Push Stage.
*   **Deployment with GitOps**: An **Azure Kubernetes Service (AKS) Cluster** is used for application deployment. **GitOps** and **ArgoCD** manage the application, with GitOps ensuring the deployment of the latest image to **Kubernetes (K8s)**.
*   **Image Update**: To streamline the process, an Update Stage is introduced in CI. This stage facilitates the update of the new image reference within **Azure Repos**, requiring updates to deployment and service files for all services.

This CD implementation has significantly enhanced my understanding of **Kubernetes**, **GitOps**, and **ArgoCD**, while also refining my command syntax skills.

Special thanks to Abhishek Veeramalla for his invaluable contribution to Part 15 of the Azure Zero-to-Hero Series, which provided a rewarding implementation experience. I am always open to feedback and ready to troubleshoot and improve.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7289722978605420544)*
