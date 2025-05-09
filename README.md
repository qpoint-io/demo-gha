# Qpoint GitHub Actions Demo

This repository demonstrates how to integrate Qpoint with GitHub Actions for seamless traffic monitoring and security in CI/CD pipelines.

## Overview

This demo shows how to:

1. Deploy Qpoint in a GitHub Actions workflow
2. Wait for Qpoint to become ready
3. Generate sample traffic using a traffic generator
4. Monitor traffic patterns through Qpoint

## Workflow Setup

The main workflow file [`.github/workflows/qpoint-demo.yml`](.github/workflows/qpoint-demo.yml) contains the following steps:

1. **Checkout Code**: Clones the repository code
2. **Install Qpoint**: Deploys Qpoint using Docker with the necessary privileges
3. **Wait for Qpoint**: Ensures Qpoint is fully initialized and ready
4. **Run Traffic Generator**: Starts a traffic generator to simulate network traffic
5. **Wait for Demo**: Allows time for the demo to run and collect data

## Local Testing

You can test this workflow locally using [act](https://github.com/nektos/act):

```bash
# Install act (if not already installed)
brew install act

# Run the workflow
act -j setup-qpoint --container-architecture linux/amd64
```

Note: When running locally with act, you may need to provide additional environment variables or settings depending on your specific environment.

## Requirements

- Docker
- GitHub Actions
- For local testing: [act](https://github.com/nektos/act)

## Configuration

The workflow uses the following configuration:

- Qpoint container: `us-docker.pkg.dev/qpoint-edge/public/qtap:v0`
- Traffic generator: `jonfriesen/traffic-generator-go:amd64_1.22`
- Traffic generation rate: 1 request per second with 3 workers

## Notes

- The Qpoint container requires privileged mode and specific capabilities to function correctly
- The workflow checks Qpoint's readiness by polling the `/readyz` endpoint
- A GitHub secret named `TOKEN` can be used to pass the registration token securely