---
title: "Building an End-to-End AWS CI/CD Pipeline"
date: 2026-07-27 15:12:58
draft: false
tags: ['AWS', 'DevOps', 'CI/CD', 'GitHub', 'CodePipeline', 'CodeBuild', 'S3', 'CloudFront', 'IAM']
summary: "This project details the creation of a zero-touch, end-to-end CI/CD pipeline on AWS, integrating GitHub, CodePipeline, CodeBuild, S3, and CloudFront for automated deployments. It highlights a common IAM troubleshooting scenario encountered during the build."
---

# Building an End-to-End AWS CI/CD Pipeline

Just wrapped up building an end-to-end AWS CI/CD pipeline! There is something incredibly satisfying about zero-touch automation. I wanted to build a workflow where deployments happen completely behind the scenes—no manual uploads, no manual cache clearing. Just write code, push, and let the cloud handle the rest.

## The Architecture & Workflow

I integrated GitHub, AWS CodePipeline, CodeBuild, Amazon S3, and CloudFront to create a seamless delivery loop:

1.  **Source**: A simple git push to the main branch on GitHub acts as the trigger.
2.  **Build & Sync**: AWS CodePipeline instantly detects the change and kicks off AWS CodeBuild, which securely syncs the updated assets to an S3 website bucket.
3.  **Global Delivery**: Finally, the pipeline automatically invalidates the Amazon CloudFront cache, instantly distributing the fresh content to edge locations worldwide.

## The Challenge: An IAM Puzzle

Because no cloud project is complete without an IAM puzzle, the best way to understand AWS is when things break. Initially, my pipeline stalled out during the `DOWNLOAD_SOURCE` phase in CodeBuild.

After digging into the logs and IAM roles, I spotted the missing link. CodePipeline uses a separate, auto-generated S3 artifact bucket to store the zipped GitHub source. My CodeBuild service role had permissions to write to my final website bucket, but it didn't have permission to read from this intermediary pipeline bucket.

Adding an inline IAM policy granting `s3:GetObject` and `s3:PutObject` for that specific artifact bucket ARN was the exact fix needed. I triggered a fresh release, and the pipeline went perfectly green!

Testing it live—editing a single line of HTML, hitting push, and watching the live CloudFront URL update seconds later—was a fantastic reminder of the power of CI/CD and the importance of deeply understanding how underlying services interact.

You can check out the repo here: https://lnkd.in/dVnE4c_J

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3AugcPost%3A7487525447380037632)*
