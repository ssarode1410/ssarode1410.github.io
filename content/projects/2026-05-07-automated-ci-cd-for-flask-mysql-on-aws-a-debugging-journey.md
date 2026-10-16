---
title: "Automated CI/CD for Flask & MySQL on AWS: A Debugging Journey"
date: 2026-05-07 13:45:42
draft: false
tags: ['DevOps', 'CI/CD', 'AWS', 'Jenkins', 'Docker', 'Flask', 'MySQL', 'Linux', 'Python', 'System Engineering']
summary: "This project involved building an automated CI/CD pipeline using Jenkins to deploy a containerized Flask and MySQL web application onto an AWS EC2 instance. The process highlighted critical debugging experiences with Jenkins, Docker caching, and Linux dependencies."
---

Green pipelines are the best pipelines! I just wrapped up a fantastic hands-on project deploying a 2-Tier web application, and the debugging process was an incredible learning experience.

## Project Overview
I recently built an automated CI/CD pipeline to deploy a **Flask** and **MySQL** application onto an **AWS EC2** instance. The infrastructure was containerized using **Docker** and **Docker Compose**, and fully automated through **Jenkins**.

But as any systems engineer knows, the real learning happens when things break. Here are a few hurdles I had to troubleshoot along the way:

## Troubleshooting Challenges

### 1. The "Missing" Runtime
Setting up Jenkins on a fresh **Ubuntu EC2** instance from scratch meant dealing with broken GPG keys from outdated repositories and sudden service crashes, which ultimately boiled down to missing **Java JRE** dependencies on the host.

### 2. The Offline Node Mystery
My Jenkins pipeline got permanently stuck waiting for an executor. Digging into the logs, I discovered Jenkins' Node Monitoring feature was taking the server offline. Because I was using an **AWS** instance with limited RAM, the `tmpfs` partition fell below Jenkins' default 1GB safety threshold. Tweaking the node configuration fixed it instantly.

### 3. Docker Caching vs. Flask Routing
The pipeline was completely green, but the UI was broken. I had to navigate Flask's strict security rules for serving media out of dedicated static folders, and force Docker to bypass its aggressive build cache (`--no-cache`) so it would actually pull my updated HTML and image files into the live container.

## Key Learnings
Transitioning from traditional service delivery and system administration into dedicated **DevOps** roles means getting comfortable with these "under the hood" mechanics. It's not just about writing the code; it's about understanding how **Linux**, **Docker**, and the network all interact to serve the final product.

## Resources
Thanks to Vishakha Sadhwani for her YouTube video Projects: [https://lnkd.in/d4kPrNiP](https://lnkd.in/d4kPrNiP)

Check out my GitHub for the source code and Jenkinsfile: [https://lnkd.in/diKMKXFd](https://lnkd.in/diKMKXFd)

## Call to Action
I'm currently an immediate joiner actively looking for my next opportunity as a Cloud or DevOps Engineer. If your team is looking for someone who loves to troubleshoot and automate, let's connect!

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7458150071344218112)*
