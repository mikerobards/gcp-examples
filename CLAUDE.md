# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository contains GCP (Google Cloud Platform) examples demonstrating specific use cases and features. Currently, examples are organized as self-contained directories, each with its own Terraform configuration.

## Terraform Workflow

Each example directory is an independent Terraform root module. Commands must be run from within the specific example directory (e.g., `quotas/`).

```bash
# Initialize (downloads providers)
terraform init

# Preview changes
terraform plan

# Apply changes
terraform apply

# Destroy resources
terraform destroy
```

## Authentication

Each module authenticates via a service account key file (`terraform-key.json`) referenced directly in the provider block. This file is gitignored and must be placed in the module directory before running Terraform. The `project_id` is passed via `terraform.tfvars` (also gitignored).

## Repository Structure

- Each top-level subdirectory is a standalone GCP example with its own provider config, variables, and tfvars.
- `terraform-key.json` and `*.tfvars` are gitignored — these must be supplied locally per example.
- The `hashicorp/google` provider is pinned (currently `7.21.0` in the `quotas` example via `.terraform.lock.hcl`).

## Adding a New Example

Create a new subdirectory with at minimum:
- `main.tf` — provider config + resources
- `variables.tf` — input variable declarations
- `terraform.tfvars` — variable values (gitignored, not committed)
