# Docker Build Automation

This project demonstrates Docker build automation using GitHub Actions for a simple Python Flask application.

## Programming Language and Application

- **Language**: Python
- **Framework**: Flask
- **Application**: A simple "Hello World" web application

## Dockerfile Structure

The Dockerfile uses a multi-stage build approach:

### Build Stage
- Base image: `python:3.9-slim`
- Installs Python dependencies from `requirements.txt`
- Uses `--user` flag to install packages in user directory

### Runtime Stage
- Base image: `python:3.9-slim`
- Copies installed packages from build stage
- Copies application code
- Sets environment variables
- Exposes port 5000
- Runs the Flask application

## Build Process

1. **Local Build**:
   ```bash
   docker build -t my-flask-app .
   docker run -p 5000:5000 my-flask-app
   ```

2. **Using Docker Compose**:
   ```bash
   docker-compose up --build
   ```

3. **GitHub Actions**:
   - Triggers on push/PR to main branch
   - Builds multi-stage Docker image
   - Pushes to GitHub Container Registry and Docker Hub
   - Sends Slack notifications on success/failure

## Advantages of Multi-Stage Builds

1. **Reduced Image Size**: Only runtime dependencies are included in the final image
2. **Security**: Build tools and source code are not present in the runtime image
3. **Efficiency**: Faster deployments and reduced attack surface
4. **Layer Caching**: Better use of Docker layer caching for faster builds

## Required Secrets for GitHub Actions

- `DOCKERHUB_USERNAME`: Docker Hub username
- `DOCKERHUB_TOKEN`: Docker Hub access token
- `SLACK_WEBHOOK_URL`: Slack webhook URL for notifications

## Running the Application

```bash
# Using Docker
docker build -t flask-app .
docker run -p 5000:5000 flask-app

# Using Docker Compose
docker-compose up --build
```

Visit `http://localhost:5000` to see "Hello World"