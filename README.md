# Shantanu Sarode - Cloud Engineering & SRE Portfolio

This repository hosts my professional portfolio and daily "Break-and-Fix" engineering labs. As a Cloud Systems and Site Reliability Engineer, I use this site to document infrastructure escalations, root-cause analysis (RCA), and Day 2 operational resolutions across AWS and Azure environments. 

Live Site: [ssarode1410.github.io](https://ssarode1410.github.io/)

## Operational Approach: The Troubleshooting Triad
All lab documentation and incident resolutions on this site follow my core methodology for minimizing MTTR:
1. **Networking & Connectivity (Path):** VPCs, subnets, routing, and security groups.
2. **IAM & Access (Permissions):** Role-based access, bucket policies, and least-privilege enforcement.
3. **Capacity & Compute (Resources):** Node health, CPU/memory limits, and resource exhaustion.

## Tech Stack
* **Framework:** [Hugo](https://gohugo.io/) (Static Site Generator)
* **Hosting:** GitHub Pages
* **CI/CD:** GitHub Actions (Automated build and deploy)
* **Version Control:** Git

## SOP: Updating Static Assets (Resume, Images, PDFs)
Hugo dynamically generates the `public/` directory during the build process. **Never place files directly into the `public/` folder**, as they will be overwritten by the GitHub Actions CI/CD pipeline. 

To update static files like your resume or lab architecture images, follow this runbook:

1. **Upload to Static:** Place the new file strictly inside the `/static` directory at the root of the repository (e.g., `/static/Shantanu_Sarode_Resumeeee.pdf`).
2. **Update the Configuration:** 
   * If updating the resume button, open the main Hugo configuration file (e.g., `config.yml`, `hugo.toml`, or `hugo.yaml`).
   * Update the `url` parameter to exactly match the new filename. Case sensitivity matters.
   * If updating an image in a blog post, update the markdown image reference (e.g., `![Architecture Diagram](/new-image.png)`).
3. **Commit and Push:** 
   ```bash
   git add .
   git commit -m "Update resume file and config references"
   git push