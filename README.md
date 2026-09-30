```markdown
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
* **Version Control:** Git

## Local Development & Deployment Workflow

To run this site locally or deploy new changes, follow these steps:

1. **Local Server:** Run `hugo server` to preview changes locally at `http://localhost:1313/`.
2. **Build:** Run `hugo` to compile the final static site into the `/public` directory.
3. **Deploy:** Commit and push the generated files to the remote repository.

```

### Future Workflow: How to handle all future changes

Whenever you add a new "Break-and-Fix" lab, update your resume, or change a configuration, you must follow this exact four-step cycle to ensure your live GitHub Pages site updates correctly:

1. **Edit the Source Files:**
Make your changes in the appropriate source folders (e.g., place new images or PDFs in `/static`, write new blog posts in `/content`, or edit configurations). *Never edit files directly inside the `/public` folder, as they will be overwritten.*
2. **Test Locally (Optional but Recommended):**
Run `hugo server -D` in your terminal to preview your changes in your browser and ensure nothing is broken.
3. **Build the Site:**
Stop the local server (Ctrl+C) and run the command `hugo`. This compiles your source files and generates the fresh HTML/CSS directly into your `/public` folder.
4. **Push to GitHub:**
Run your standard Git commands to push the updated files to your repository:
* `git add .`
* `git commit -m "Added new troubleshooting lab" `
* `git push`