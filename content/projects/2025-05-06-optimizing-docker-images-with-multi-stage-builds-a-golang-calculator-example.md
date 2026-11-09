---
title: "Optimizing Docker Images with Multi-Stage Builds: A Golang Calculator Example"
date: 2025-05-06 15:28:58
draft: false
tags: ["Docker", "Multi-Stage Builds", "Golang", "Containerization", "DevOps", "CI/CD", "Image Optimization", "Scratch"]
summary: "This project demonstrates the power of multi-stage Docker builds to significantly reduce image size and improve efficiency. By containerizing a Golang calculator app, a 600x reduction in image size was achieved, highlighting best practices for lean and secure containerization."
---

## Mastering Multi-Stage Docker Builds – Build Smarter, Not Bigger!

When building Docker images for production, bloated containers filled with compilers, test tools, and unnecessary files are undesirable. That's where Multi-Stage Builds come in — a game-changer for clean, efficient containerization.

### What is a Multi-Stage Docker Build?

A multi-stage Docker build allows you to use multiple `FROM` statements in a single Dockerfile. Each `FROM` starts a new build stage, and you can copy artifacts from one stage to another — ensuring your final image only contains what it needs to run.

**Goal:** Build and test in earlier stages, exporting only the minimal runtime to the final image.

### Example Dockerfile

```dockerfile
# Stage 1: Build
FROM golang:1.21 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# Stage 2: Runtime
FROM scratch
WORKDIR /app
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

*   **Stage 1** compiles the Go application.
*   **Stage 2** is an ultra-light `scratch` image, containing only the compiled binary.

### Real-World Example: Golang Calculator App

I containerized a simple calculator app written in Golang.
*   Initially, using a regular Docker build, the image size was a massive ~640 MB.
*   After implementing a multi-stage Dockerfile, the image was reduced to just ~2 MB!

That’s a ~600x size reduction for the same app, demonstrating incredible optimization.

*Big thanks to Abhishek Veeramalla for the original app idea!*

### Why Use Multi-Stage Builds?

*   **Smaller Image Size:** No compilers or development tools in your final image means faster downloads and better security.
*   **Better Separation of Concerns:** Build logic stays in build stages; runtime is clean and production-ready.
*   **Improved Security & Attack Surface:** A minimal base image results in fewer vulnerabilities.
*   **Faster CI/CD Pipelines:** Smaller images lead to quicker deployments.

### Best Practices:

*   Use `AS builder` to name your stages for clarity.
*   Use `COPY --from=builder` to selectively grab only necessary artifacts.
*   Keep base images minimal for runtime (e.g., Alpine or Scratch).
*   Add a `.dockerignore` file to exclude unnecessary files from the build context.
*   Always scan final images for vulnerabilities.

Multi-stage builds aren’t just a best practice — they’re essential in modern containerization.

*[Original LinkedIn Post](https://www.linkedin.com/feed/update/urn%3Ali%3Ashare%3A7325542098810626048)*
