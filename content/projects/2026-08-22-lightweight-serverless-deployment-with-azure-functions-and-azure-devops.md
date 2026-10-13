---
title: "Lightweight Serverless Deployment with Azure Functions and Azure DevOps"
date: 2026-08-22 07:25:19
draft: false
tags: ['Azure', 'Azure Functions', 'Azure DevOps', 'CI/CD', 'Serverless', 'Zero-Trust', '.NET 8', 'Managed Identity', 'Key Vault']
summary: "This project details the architecture and implementation of a lightweight, non-containerized PaaS deployment for a .NET 8 Azure Function. It features a zero-trust CI/CD pipeline built with Azure DevOps, leveraging Azure's Flex Consumption plan and Managed Identities for secure, efficient serverless operations."
---

Not every cloud deployment requires the heavy lifting of a Kubernetes cluster!

Lately, I’ve been diving deep into container orchestration and GitOps, but today I took a step back to architect a native, non-containerized PaaS deployment. The goal? Maximum speed, zero-trust security, and zero container overhead.

I built a complete CI/CD pipeline for a .NET 8 Azure Function targeting the new Flex Consumption plan, and the results were incredibly lightweight and efficient.

## Architecture Breakdown

Here is a breakdown of the architecture:

### The Compute

Deployed to **Azure's Flex Consumption plan** to keep the pay-as-you-go serverless model while unlocking enterprise features like VNet integration and cold-start mitigation.

### Zero-Trust Security

Completely eliminated hardcoded pipeline secrets. I provisioned the Function App with a **System-Assigned Managed Identity**, granted it strict **RBAC** access to **Azure Key Vault**, and utilized native `@Microsoft.KeyVault` environment variable references.

### The CI/CD Engine

Built a multi-stage **Azure DevOps YAML pipeline** running on a **self-hosted Linux agent**.
*   The **CI stage** uses the **.NET CLI** to compile and package a `.zip` artifact.
*   The **CD stage** pushes it directly to the App Service plan via an **Azure Resource Manager connection**.

## The Takeaway

While Docker and AKS are fantastic tools, sometimes a native ZIP deployment over a secure Service Connection is exactly what an enterprise needs for event-driven APIs. It drastically reduces pipeline execution time and shrinks the operational attack surface.

## Discussion

What is your go-to deployment strategy for lightweight background jobs and APIs? Are you team Serverless or team Containers? Let me know below!

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7496829844270243840)*
