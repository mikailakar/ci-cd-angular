# CI/CD Angular Project

This project demonstrates Continuous Integration and Continuous Deployment (CI/CD) for an Angular application. It includes GitHub Actions for automated testing and deployment to Vercel.

## Overview

- **Branch `new-feature`**: Add new features to the Angular application.
- **GitHub Workflow**: Set up for automated testing and deployment.
- **Deployment**: The application is deployed to Vercel.

## Features

- **New Feature**: Implemented and tested in the `new-feature` branch.
- **GitHub Actions**: Automated CI/CD pipeline for building, testing, and deploying the application.
- **Deployment**: Continuous deployment to Vercel.

## GitHub Workflows

### Preview Deployment

The workflow defined in `.github/workflows/preview.yaml` handles preview deployments for non-main branches. It includes:

1. **Test**:
   - Runs on: `ubuntu-latest`
   - **Checkout**: Uses `actions/checkout@v3` to fetch the repository.
   - **Setup Node.js**: Uses `actions/setup-node@v3` with Node.js version 18.
   - **Install Dependencies**: Runs `npm ci`.
   - **Run Tests**: Executes `npm run test:prod`.

2. **Deploy-Preview**:
   - Depends on: `Test`
   - Runs on: `ubuntu-latest`
   - **Checkout**: Uses `actions/checkout@v3` to fetch the repository.
   - **Install Vercel CLI**: Installs Vercel CLI globally.
   - **Pull Vercel Environment Information**: Uses `vercel pull` with the preview environment.
   - **Build Project Artifacts**: Uses `vercel build` to build the project.
   - **Deploy Project Artifacts**: Uses `vercel deploy` to deploy the built project.

### Production Deployment

The workflow defined in `.github/workflows/production.yaml` handles production deployments for the `main` branch. It includes:

1. **Deploy-Production**:
   - Runs on: `ubuntu-latest`
   - **Checkout**: Uses `actions/checkout@v3` to fetch the repository.
   - **Install Vercel CLI**: Installs Vercel CLI globally.
   - **Pull Vercel Environment Information**: Uses `vercel pull` with the production environment.
   - **Build Project Artifacts**: Uses `vercel build` with the `--prod` flag.
   - **Deploy Project Artifacts**: Uses `vercel deploy` with the `--prod` flag to deploy the project.

## Deployment

The application is automatically deployed to Vercel:

- **Preview Deployments**: Triggered for branches other than `main`.
- **Production Deployments**: Triggered for the `main` branch.

You can view the live application [here](https://ci-cd-angular.vercel.app).

## Branches

- **`main`**: The main branch with the latest stable code.
- **`new-feature`**: Contains the new feature implementation. Merged into the `main` branch after successful testing.

## Testing

Tests are automatically run as part of the CI/CD pipeline. Ensure all tests pass before merging changes to the `main` branch.
