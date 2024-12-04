# Development Environment Setup

This guide explains how to set up a development environment to host private software repositories, essential software packages, and a package management system.

---

## Overview

In a network (LAN/WAN without internet access), you can enable software development by hosting the following components:

1. **Version Control System**: Git hosting (e.g., GitLab or Gitea).
2. **Package Management**: Nexus Repository for managing Python, JavaScript, and other packages.
3. **Software Distribution**: Hosting essential software tools (e.g., PyCharm, VSCode, Git).
4. **Optional**: Local Docker registry for containerized development.

---

## Components

### 1. **Git Hosting**
- Use **GitLab CE** or **Gitea** to host private Git repositories.
- **GitLab Installation**: [GitLab CE Installation Guide](https://about.gitlab.com/install/)
- **Gitea Installation**: [Gitea Installation Guide](https://docs.gitea.io/en-us/installation/)

---

### 2. **Package Management System**
Use **Sonatype Nexus Repository Manager** to manage programming language packages:

#### Python (PyPI)
1. Create a PyPI repository in Nexus.
2. Mirror public PyPI repositories for required packages before disconnecting the internet.
3. Upload custom Python packages if needed.

#### JavaScript (npm)
1. Create an npm repository in Nexus.
2. Mirror public npm packages.
3. Host private JavaScript packages.

**Nexus Documentation**: [Nexus Repository OSS](https://help.sonatype.com/repomanager3)

---

### 3. **Software Distribution**
- Use **Nexus** or an HTTP file server (e.g., Nginx, Apache, MinIO) to distribute tools:
  - IDEs: PyCharm, VSCode.
  - Tools: Git, Docker CLI, etc.
- Create a raw repository in Nexus to host binary files (e.g., `.exe`, `.deb`, `.tar.gz`).

---

### 4. **Local Docker Registry (Optional)**
- Deploy **Harbor** or Nexus Docker Repository to:
  - Host container images for tools and services.
  - Store Docker images for development or CI/CD pipelines.

**Docker Registry Setup**: [Nexus Docker Registry Guide](https://help.sonatype.com/repomanager3/nexus-repository-administration/formats/docker-registry)

---

### 5. **Local Package Cache**
To cache dependencies:
1. Use Nexus as a caching proxy for repositories like PyPI, npm, and Maven.
2. Synchronize dependencies when temporarily connected to the internet.

---

### 6. **Network Design**
Ensure all services are accessible in the air-gapped environment:
- Use a **reverse proxy** (e.g., Nginx) for central access to hosted services.
- Optionally, set up DNS entries for internal service URLs.

---

### 7. **Offline Synchronization**
- Use scripts to mirror external repositories (PyPI, npm, etc.).
- Periodically update hosted tools and dependencies.

---

## Summary
This setup enables efficient offline development by hosting all necessary resources in an environment.
