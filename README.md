# CI/CD Lab

A simple Node.js application designed for learning and demonstrating Continuous Integration and Continuous Deployment (CI/CD) pipelines. This project uses Express.js for the API, Docker for containerization, and GitHub Actions for automation.

## Features

- **REST API**: Simple Express server with health check.
- **Dockerized**: Multi-stage Dockerfile for optimized production images.
- **CI/CD Pipeline**: Comprehensive GitHub Actions workflow including:
  - Linting and Testing
  - Security Scanning (Trivy, npm audit)
  - Docker Build and Push
  - Staging Deployment simulation

## Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later)
- [Docker](https://www.docker.com/)
- [npm](https://www.npmjs.com/)

## Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd ci-cd-lab
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

## Usage

### Running Locally

To start the server locally:

```bash
node src/app.js
```

The server will start on port `3000` (default).
Access the API at: `http://localhost:3000`

### Running with Docker

1. Build the image:
   ```bash
   docker build -t ci-cd-lab .
   ```

2. Run the container:
   ```bash
   docker run -p 3000:3000 ci-cd-lab
   ```

## API Endpoints

- `GET /`
  - Returns a welcome message and the current server timestamp.
  - Response: `{ "message": "Hello CI/CD World!", "timestamp": "..." }`

- `GET /health`
  - Health check endpoint.
  - Response: `{ "status": "healthy" }`

## Testing

The project uses [Jest](https://jestjs.io/) and [Supertest](https://www.npmjs.com/package/supertest) for testing.

To run tests manually:

```bash
npx jest
```

> **Note**: The default `npm test` script in `package.json` needs to be updated to run jest.

## CI/CD Pipeline

The project includes a GitHub Actions workflow (`.github/workflows/ci-cd.yml`) that triggers on pushes and pull requests to the `main` branch.

### Workflow Steps:
1. **Test & Code Quality**: Runs linting and unit tests.
2. **Security Scan**: Scans the filesystem for vulnerabilities using Trivy and runs `npm audit`.
3. **Build & Push**: Builds the Docker image and pushes it to Docker Hub (requires `DOCKER_USERNAME` and `DOCKER_PASSWORD` repository secrets).
4. **Deploy**: Simulates a deployment to a staging environment.

## Configuration

- **Port**: The server listens on port `3000` by default. Set the `PORT` environment variable to override execution port.
