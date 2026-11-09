---
title: "Deploying a NodeJS App on AWS EC2"
date: 2025-02-20 19:17:14
draft: false
tags: ["AWS", "EC2", "NodeJS", "Git", "Ubuntu"]
summary: "This project details the step-by-step process of deploying a NodeJS application on an AWS EC2 instance, covering setup, dependency installation, and security group configuration for public access."
---

Today, we took the exciting step of deploying our first application on AWS using the EC2 service.

### Technologies Used
The core technologies involved in this deployment were **AWS**, **Git**, and **NodeJS**.

### Deployment Process Overview
Here's a brief overview of the process we followed:

1.  **EC2 Instance Initialization**: We initiated an EC2 instance on AWS, opting for **Ubuntu** as the operating system and utilizing the free tier eligible `t2.micro` instance type.
2.  **Software Installation**: **Git** and **NodeJS** were installed on the server to support our application.
3.  **Code Deployment**: We set the foundation for our project by cloning a Git repository from a public source.
4.  **Application Launch**: Since our project relies on NodeJS, we executed the commands `npm install` to acquire necessary dependencies, followed by `npm run start` to launch the application.
5.  **Accessing the Application**: To view the content, simply input the public IP of the EC2 instance in a new browser window with port 3000 (e.g., `http://ec2_public_ip:3000`).

### Important: Exposing Port 3000
Before accessing the content, it is crucial to expose port 3000 to the world to facilitate incoming requests; failing to do so will result in errors.

To achieve this:
*   Navigate to the security settings of the created EC2 instance.
*   Edit the inbound rules.
*   Append a new rule permitting any incoming request from anywhere (`0.0.0.0/0`) at port 3000.

Once this configuration is complete, the content will be readily accessible.

---
*Thanks to Abhishek Veeramalla for the insights.*

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3Ashare%3A7298420454833217536)*
