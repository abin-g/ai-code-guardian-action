# AI Code Guardian (Public Hub)

Welcome to the public setup repository for AI Code Guardian!

## How to Install (Interactive)

The easiest way to integrate AI Code Guardian into your GitHub projects is to use our interactive setup wizard. 

1. Download the setup script:
   ```bash
   curl -sO https://raw.githubusercontent.com/abin-g/ai-code-guardian-action/main/setup.sh
   chmod +x setup.sh
   ```
2. Run it locally and follow the prompts:
   ```bash
   ./setup.sh
   ```

*The wizard will automatically generate the required GitHub Action `.github/workflows/ai-code-guardian.yml` and the standard configuration `.ai-guardian.yml` right inside your target repository.*

## Manual Installation

If you prefer to set it up manually without the setup wizard, add this block to your `.github/workflows/main.yml`:

```yaml
jobs:
  code-guardian-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run AI Code Guardian
        uses: abin-g/ai-code-guardian-action@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          # block_on_findings: "true"
```
