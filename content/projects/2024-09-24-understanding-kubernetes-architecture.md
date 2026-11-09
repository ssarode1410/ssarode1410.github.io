---
title: "Understanding Kubernetes Architecture"
date: 2024-09-24 08:23:34
draft: false
tags: ["Kubernetes", "Architecture", "Cloud Native", "Container Orchestration"]
summary: "This post provides a foundational overview of Kubernetes architecture, detailing the key components of both the Master and Worker planes and their respective functions."
---

This post outlines the basic architecture of Kubernetes.

Kubernetes architecture consists of two main parts:
*   The **Master Plane**
*   The **Worker/Data Plane**

### Master Plane Components

The Master Plane consists of 5 key components:
1.  **API Server**: The heart of Kubernetes, controlling everything and connecting core Kubernetes to requests.
2.  **Scheduler**: Looks for free pods and assigns pods to nodes based on requests from the API server.
3.  **etcd**: A distributed key-value store that stores all cluster data.
4.  **Controller Manager**: Manages the in-built controllers.
5.  **Cloud Controller Manager**: Integrates Kubernetes with underlying cloud provider APIs.

### Data Plane Components

The Data Plane has 3 essential components:
1.  **Kubelet**: Ensures that pods and their containers are running on the nodes.
2.  **Kube Proxy**: Handles network proxying for Kubernetes services.
3.  **Container Runtime**: Responsible for running containers (e.g., Docker, containerd).

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3Ashare%3A7244260160695631874)*
