# Development Workstation Setup

## 1. Project Overview
This project documents the setup and practice of a development workstation using macOS, OrbStack, Docker, and Git.

## 2. Environment
- OS: macOS
- Computer: MacBook Air (Apple Silicon)
- Terminal: zsh
- Container Runtime: OrbStack
- Container Tool: Docker
- Version Control: Git
- Remote Repository: GitHub

## 3. Completed Tasks

### Terminal Practice
- [x] Check current directory (`pwd`)
- [x] List files (`ls`)
- [x] Create files and directories
- [x] Copy, move, rename, and delete files
- [x] View file contents (`cat`)
- [x] Change file permissions (`chmod`)

### Docker Practice
- [x] Install and run OrbStack
- [x] Run hello-world container
- [x] Run Ubuntu container
- [x] Check Docker images and containers
- [x] Build a custom Docker image
- [x] Run an NGINX web server
- [x] Map host port 8080 to container port 80
- [x] Check container logs and resource usage
- [x] Practice Bind Mount
- [x] Practice Docker Volume

### Git Practice
- [x] Configure Git username and email
- [x] Initialize a Git repository
- [x] Commit project files
- [x] Connect GitHub repository
- [x] Push files to GitHub

## 4. Docker Web Server
- Docker Image: `my-web-image`
- Container: `my-web`
- Host Port: `8080`
- Access URL: http://localhost:8080

## 5. Bind Mount and Volume
Bind Mount was used to connect the local HTML folder to the NGINX container. Changes made to the local HTML file were reflected in the browser.

Docker Volume was used to verify that stored data remains available even after a temporary container is removed.

## 6. Screenshots
Screenshots of the installation, terminal commands, Docker containers, and web server are stored in the `screenshots` directory.

## 7. Troubleshooting
Troubleshooting records will be added after documenting the errors and their solutions.

## 8. Conclusion
This project provided practical experience with terminal commands, file permissions, Docker image and container management, web server deployment, persistent storage, and Git-based version control.
## 8. Troubleshooting

### Case 1. GitHub Repository Not Found

**Problem:**

When executing `git push -u origin main`, the following error occurred:

`remote: Repository not found.`

**Cause:**

The remote repository URL contained an incorrect repository address.

**Solution:**

The remote URL was updated using the correct GitHub repository address.

```bash
git remote set-url origin https://github.com/juju1105/dev_workstation.git
git remote -v
git push -u origin main
```

**Result:**

The repository address was corrected, and the project could be uploaded to GitHub.
### Case 2. Docker Image Build Failure

**Problem:**

An error occurred while building a custom Docker image using the `docker build` command.

**Possible Causes:**

- Incorrect Dockerfile instructions
- Incorrect file paths
- Missing source files
- Docker build context errors

**Troubleshooting:**

1. Checked the Dockerfile instructions.
2. Verified the location of the HTML file.
3. Checked that the Dockerfile was located in the project directory.
4. Executed the build command again.

```bash
docker build -t my-web-image .
```

**Result:**

The Docker image was successfully built and the NGINX web server was started.
