# Sentinel CI Setup Guide 🛠️

This guide covers how to integrate **Sentinel CI** (AI Code Guardian engine) into your GitHub repository using the interactive setup wizard or manual configuration.

---

## 🏗️ Method 1: Interactive Setup Wizard (Fastest)

Our interactive setup script walks you through configuration and generates the necessary files in your project.

### Usage

1. Open your terminal and navigate to the root of your target project.
2. Run the following command:
   ```bash
   curl -sL https://raw.githubusercontent.com/abin-g/sentinel-ci-action/master/setup.sh -o setup.sh
   chmod +x setup.sh && ./setup.sh
   ```

### What the Wizard Does:
- **Scaffolds Config:** Creates a `.sentinel-ci.yml` file based on your feature preferences.
- **Sets up Workflow:** Creates `.github/workflows/sentinel-ci.yml` with the correct permissions and triggers.
- **Configures Governance:** Lets you choose strict vs conservative merge blocking.

> **Legacy:** Older installs may use `sentinel-ci.yml` as the workflow filename; both work the same way.

---

## 🛠️ Method 2: Manual Installation

If you prefer to configure the action manually, follow these steps:

### 1. Create the Workflow File
Create a file at `.github/workflows/sentinel-ci.yml` with the following content:

```yaml
name: Sentinel CI

on:
  pull_request:
    types: [opened, synchronize, reopened]
    branches: [main, master, release]

permissions:
  contents: read
  pull-requests: write

jobs:
  sentinel-ci:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Run Sentinel CI
        uses: abin-g/sentinel-ci-action@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          # Optional: scan_path: "."
          # Optional: block_on_findings: "true"
```

### 2. Add the Configuration File
Create a `.sentinel-ci.yml` file in your repository root to control the scanner's behavior (legacy `.ai-guardian.yml` is still supported if the new file is absent):

```yaml
security:
  enabled: true
  # Severities that will cause the CI check to fail
  block_on_severity:
    - ERROR

exclude:
  - "tests/**"
  - "node_modules/**"
  - "dist/**"
```

---

## 🔑 Authentication

Sentinel CI requires a `GITHUB_TOKEN` to post comments on your Pull Requests.

- **GitHub Actions:** The `${{ secrets.GITHUB_TOKEN }}` is automatically provided by GitHub for every workflow run. No manual secret setup is required as long as you have `pull-requests: write` permissions defined in your workflow.

---

## 🚀 Post-Installation

Once the files are added:
1. Commit the changes: `git add . && git commit -m "chore: add Sentinel CI"`
2. Push to your repository: `git push`
3. Open a test Pull Request to see the scan in action!
