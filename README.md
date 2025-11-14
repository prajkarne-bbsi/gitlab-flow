# GitLab-Flow 

## Overview
GitLab Flow strikes a balance between Git Flow and GitHub Flow. It adopts GitHub Flow's simplicity while introducing additional branches representing staging environments before production. The main branch serves as the integration point, with environment-specific branches for controlled deployments.

**Best suited for**: Teams needing multiple environments, versioned releases, or staged deployments while maintaining simplicity.

## Core Principles

- **Main branch as integration hub** - Central point for all feature merges
- **Environment branches** - Separate branches for staging, pre-production, and production
- **Upstream first policy** - Changes flow from main → staging → production
- **Feature branches for development** - All work happens in feature branches
- **Version branches for releases** - Support multiple release versions when needed
- **Merge requests drive quality** - Code review and testing before promotion

## Branching Strategy

### Main Branch (`main`)
- **Purpose**: Integration branch, latest development code
- **Protection**: Protected, requires MR reviews
- **Deployment**: Can deploy to development environment
- **Rules**: 
  - No direct commits allowed
  - All changes via Merge Requests only
  - Must pass automated tests
  - Source for all feature branches

### Environment Branches

#### Pre-Production Branch (`pre-production`)
- **Purpose**: Testing and QA environment
- **Created from**: `main`
- **Receives merges from**: `main` only
- **Deployment**: Auto-deployed to staging/QA environment
- **Rules**: 
  - Only accepts merges from `main`
  - Cherry-pick urgent fixes if needed
  - Must pass all integration tests

#### Production Branch (`production`)
- **Purpose**: Live production environment
- **Created from**: `pre-production`
- **Receives merges from**: `pre-production` only
- **Deployment**: Auto-deployed to production
- **Rules**: 
  - Only accepts merges from `pre-production`
  - Tagged with version numbers
  - Highly protected, requires approvals
  - Represents stable releases

### Feature Branches (`feature/*`)
- **Purpose**: New features and bug fixes
- **Naming Convention**: `feature/descriptive-name` or `feature/TICKET-123-description`
- **Lifespan**: Short-lived (ideally 1-5 days)
- **Created from**: `main`
- **Merged into**: `main`
- **Rule**: Delete immediately after merge

### Release Branches (`release/*`) - Optional
- **Purpose**: Support specific release versions
- **Naming Convention**: `release/v1.2.x` or `release/2024-11`
- **Created from**: `main` or specific commit
- **Lifespan**: Long-lived, maintained for version support
- **Use case**: When supporting multiple versions in production
