---
title: "CI/CD Pipeline for Static Website"
date: 2025-12-08T12:19:18+05:30
summary: "Automated the deployment of a Hugo-based portfolio using GitHub Actions and Pages."
tags: ["CI/CD", "GitHub Actions", "DevOps", "Hugo"]
weight: 1
---

## 🚀 Project Overview
To showcase my transition into DevOps, I moved away from drag-and-drop website builders and built a static site using **Infrastructure-as-Code** principles. The goal was to create a zero-maintenance, high-performance portfolio that deploys automatically.

## 🔧 Tech Stack
* **Engine:** Hugo (Static Site Generator)
* **Version Control:** Git & GitHub
* **CI/CD:** GitHub Actions (YAML workflows)
* **Hosting:** GitHub Pages
* **Editor:** VS Code

## 🏆 The Challenge
Manually uploading HTML files via FTP is error-prone and slow. I needed a way to ensure that any change to the source code (Markdown/Config) would automatically trigger a build and deployment process without human intervention.

## 💡 The Solution
I implemented a **Continuous Deployment** pipeline.
1.  **Source Control:** I maintain the code in a public GitHub repository.
2.  **Automation:** I wrote a `.github/workflows/hugo.yaml` file.
3.  **Trigger:** Upon a `git push` to the `main` branch, the pipeline activates.
4.  **Build:** It spins up an Ubuntu container, installs the specific Hugo version (0.146.0), and builds the static assets.
5.  **Deploy:** It securely uploads the artifacts to GitHub Pages.

## 📈 Key Learnings
* Configuring **YAML workflows** for GitHub Actions.
* Troubleshooting **dependency version mismatches** (Hugo Extended vs Standard).
* Managing **Git submodules** for theme management.

---
*Check out the code for this very website here: [Link to your Repo](https://github.com/ssarode1410/ssarode1410.github.io)*