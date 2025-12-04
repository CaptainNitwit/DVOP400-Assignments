# DVOP400-Assignments

This repository contains static HTML workflow guides for DVOP400 assignments.

## Node/Express static server

A minimal Node/Express server serves the site locally.

**Quick start (PowerShell):**

```powershell
cd "g:\DVOP400 Github Stuff\DVOP400-Assignments\DVOP400-Assignments"
npm install
npm start

# open http://localhost:3000 in your browser
```

**Notes:**
- The Express server serves files from the project root so existing HTML and asset paths continue to work.
- `package.json` includes a `dev` script that uses `nodemon` if you want automatic restarts (install nodemon globally or as a devDependency).

## Docker & GitHub Actions

A GitHub Action automatically builds and pushes a **multi-platform Docker image** (Linux amd64, arm64) to Docker Hub whenever you push to the `main` branch.

### Setup

1. Create a Docker Hub account: https://hub.docker.com/
2. Generate a personal access token: https://hub.docker.com/settings/security
3. Add secrets to your GitHub repository:
   - Go to **Settings → Secrets and variables → Actions**
   - Add `DOCKER_USERNAME` (your Docker Hub username)
   - Add `DOCKER_PASSWORD` (your personal access token)

### Run the Docker container

Once the GitHub Action completes, pull and run the image:

```powershell
# Using your Docker Hub username
docker pull YOUR_DOCKER_USERNAME/dvop400-workflows:latest
docker run -p 3000:3000 YOUR_DOCKER_USERNAME/dvop400-workflows:latest

# Open http://localhost:3000 in your browser
```

The image runs on Windows, macOS, and Linux via Docker Desktop.

### Build locally

```powershell
docker build -t dvop400-workflows:local .
docker run -p 3000:3000 dvop400-workflows:local
```

## Files Overview

- `index.html` — Home page with links to all workflow guides
- `*-workflow.html` — Individual workflow guide pages
- `server.js` — Express server that serves static files
- `package.json` — Node.js project config with Express dependency
- `Dockerfile` — Multi-stage Docker build for containerized deployment
- `.dockerignore` — Excludes unnecessary files from Docker image
- `.github/workflows/docker-build-push.yml` — GitHub Action for CI/CD

## Workflow Pages

1. **Centralized Workflow** — Single branch, best for small teams
2. **Feature Branch Workflow** — Feature isolation with develop/main branches
3. **Gitflow Workflow** — Complex branching for releases and hotfixes
4. **Forking Workflow** — Distributed development for open-source
5. **Trunk-Based Development** — Short-lived branches with frequent commits
6. **GitHub Workflow** — Simplified branch model with pull requests
