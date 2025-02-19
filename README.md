# Dependency Check 🔍

### Overview 🛡️
This repository contains a GitHub Actions workflow that scans dependency updates for security vulnerabilities whenever a pull request modifies dependency lock files. It ensures that new vulnerabilities are not introduced into the codebase.

### How It Works ⚙️
**The workflow triggers only when a PR modifies any of the following files:**
- Gemfile.lock (Ruby)
- package-lock.json (npm)
- yarn.lock (Yarn)
- pnpm-lock.yaml (pnpm)

NOTE: This can be customized to add additional dependency files as needed (see [supported languages](https://trivy.dev/v0.47/docs/coverage/language/#:~:text=Licenses-,Supported%20languages,-The%20files%20analyzed))

**The workflow runs Trivy, a reputable security scanner, and compares the scan results between:**
- Main branch (baseline security state)
- PR branch (newly introduced changes)

**If new vulnerabilities are found, the PR will be flagged.**

### Workflow Steps 🔄

- Install Trivy Scanner – Downloads and verifies the latest Trivy version.
- Checkout Repository – Fetches both the main branch and PR branch.
- Scan Main Branch – Runs Trivy on the default branch and saves results.
- Scan PR Branch – Runs Trivy on the PR branch and saves results.
- Analyze Results – Compares scan outputs and determines if new vulnerabilities were introduced.

### Requirements 📋
- GitHub Actions enabled on the repository.
- PRs modifying dependency lock files trigger the workflow.
- The repository should contain the `.github/scripts/dependency_check.rb` script to analyze scan results.

### Why Use This? 🚀
- ✅ Prevents security vulnerabilities from being merged.
- ✅ Automates security checks for dependency updates.
- ✅ Works across multiple package managers (Bundler, npm, Yarn, pnpm).
- ✅ Only flags new issues, reducing false positives.
- ✅ Lightweight and integrates into CI/CD workflows.

### How to Enable ⚡
Ensure this workflow is placed in `.github/workflows/dependency-check.yml` within your repository. GitHub will automatically run the check when relevant files are updated. Ensure `.github/scripts/dependency_check.rb` is also present. This file can be customized to display results based on specific requirements.

### Severity Threshold 🎛️
Modify the ALERT_ON environment variable in dependency-check.yml to adjust severity levels:
```
env:
  ALERT_ON: "LOW,MEDIUM,HIGH,CRITICAL"
```

<img width="1134" alt="Screenshot 2025-02-19 at 10 20 48 AM" src="https://github.com/user-attachments/assets/27f039cb-c66d-46d8-a658-6654d515f83d" />
