# AI Code Guardian Setup Guide 🛠️

This guide covers how to integrate AI Code Guardian into your GitHub repository using the interactive setup wizard or manual configuration.

---

## 🏗️ Method 1: Interactive Setup Wizard (Fastest)

Our interactive setup script will walk you through the configuration and automatically generate the necessary files in your project.

### Usage

1. Open your terminal and navigate to the root of your target project.
2. Run the following command:
   ```bash
   curl -sO https://raw.githubusercontent.com/abin-g/ai-code-guardian-action/master/setup.sh
   chmod +x setup.sh && ./setup.sh
   ```

### What the Wizard Does:
- **Scaffolds Config:** Creates a `.ai-guardian.yml` file based on your feature preferences.
- **Sets up Workflow:** Creates `.github/workflows/ai-code-guardian.yml` with the correct permissions and triggers.
- **Configures Governance:** Allows you to decide if critical security issues should block PR merges.

---

## 🛠️ Method 2: Manual Installation

If you prefer to configure the action manually, follow these steps:

### 1. Create the Workflow File
Create a file at `.github/workflows/ai-code-guardian.yml` with the following content:

```yaml
name: AI Code Guardian

on:
  pull_request:
    types: [opened, synchronize, reopened]
    branches: [main, master, release]

permissions:
  contents: read
  pull-requests: write

jobs:
  code-guardian:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Run AI Code Guardian
        uses: abin-g/ai-code-guardian-action@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          # Optional: scan_path: "."
          # Optional: block_on_findings: "true"
```

### 2. Add the Configuration File
Create a `.ai-guardian.yml` file in your repository root to control the scanner's behavior:

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

AI Code Guardian requires a `GITHUB_TOKEN` to post comments on your Pull Requests. 

- **GitHub Actions:** The `${{ secrets.GITHUB_TOKEN }}` is automatically provided by GitHub for every workflow run. No manual secret setup is required as long as you have `pull-requests: write` permissions defined in your workflow.

---

## 🚀 Post-Installation

Once the files are added:
1. Commit the changes: `git add . && git commit -m "chore: add AI Code Guardian"`
2. Push to your repository: `git push`
3. Open a test Pull Request to see the bot in action!
