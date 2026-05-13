# github-actions-workflows
Reusable GitHub Actions workflows for CI/CD, security scanning, Terraform validation and Docker builds

# GitHub Actions Workflows

Reusable GitHub Actions workflows for CI/CD automation, 
security scanning, Terraform validation, and multi-environment 
deployments.

## Repository Structure
.github/workflows/          # Production-ready workflows
├── terraform-validate.yml  # Validates Terraform on every push
├── docker-build.yml        # Builds and tests Docker images
├── security-scan.yml       # Scans for secrets and vulnerabilities
└── scheduled-cleanup.yml   # Weekly maintenance automation
examples/                   # Reference workflow examples
├── pr-checks.yml           # Automated pull request checks
└── multi-environment-deploy.yml  # Dev → Staging → Production pipeline

## Workflows

### terraform-validate.yml
Triggers on every push that changes `.tf` files. Runs:
- Terraform format check
- Terraform init
- Terraform validate

Catches syntax errors and misconfigurations before they reach production.

### docker-build.yml
Triggers on every push that changes Dockerfile or application code. Runs:
- Docker image build using Buildx
- Container startup test
- Image summary report

### security-scan.yml
Triggers on push, pull request, and every Monday at 9am. Runs:
- Secret detection using TruffleHog
- Dependency vulnerability scan using Trivy
- Sensitive file pattern detection
- Large file detection

### scheduled-cleanup.yml
Triggers every Sunday at 2am. Runs:
- Repository health check
- File statistics report
- TODO item detection
- Maintenance summary

## Examples

### pr-checks.yml
Automated checks on every Pull Request:
- PR title validation
- Merge conflict marker detection
- YAML file validation

### multi-environment-deploy.yml
Sequential deployment pipeline:
- Deploy to Dev automatically on push to main
- Deploy to Staging after Dev succeeds
- Deploy to Production after Staging succeeds
- Each stage runs smoke and integration tests

## Key concepts demonstrated

| Concept | Where |
|---|---|
| Push triggers | terraform-validate.yml, docker-build.yml |
| PR triggers | security-scan.yml, pr-checks.yml |
| Scheduled triggers (cron) | security-scan.yml, scheduled-cleanup.yml |
| Manual triggers | All workflows via workflow_dispatch |
| Job dependencies (needs:) | multi-environment-deploy.yml |
| Environment gates | multi-environment-deploy.yml |
| Pre-built actions (uses:) | All workflows |
| Shell commands (run:) | All workflows |
| GitHub context variables | All workflows |

## How to use these workflows

Copy any workflow file into your repository's `.github/workflows/` 
folder and push — GitHub will automatically detect and run it.

```bash
mkdir -p .github/workflows
cp terraform-validate.yml .github/workflows/
git add .
git commit -m "Add Terraform validation workflow"
git push
```

## Requirements
- GitHub repository (public or private)
- GitHub Actions enabled (default for all repos)
- Secrets configured in repository settings for deployment workflows

## Author
Navya Kanchisamudram — Azure Administrator (AZ-104)
GitHub: github.com/Navya123489
