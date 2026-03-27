# AI Code Guardian Rule Engine Guide

This document explains how to configure `.ai-guardian.yml` for security gates, quality scanning, deterministic standards, and AI practice review.

---

## What `.ai-guardian.yml` Controls

AI Code Guardian supports four policy layers:

1. `security`  
   Controls merge-blocking behavior by severity (`ERROR`, `WARNING`, `INFO`).

2. `quality`  
   Enables additional Semgrep quality rulesets (`p/ci`, `p/default`) on top of baseline scanning.

3. `standards`  
   Deterministic (non-AI) checks for imports, naming patterns, and required structure.

4. `practices`  
   AI-driven review using your plain-English engineering guidelines.

---

## Full Configuration Template

Use this as a starting point:

```yaml
security:
  enabled: true
  block_on_severity:
    - ERROR

quality:
  enabled: true
  block_on_severity: []

practices:
  enabled: true
  block_on_severity:
    - ERROR
  guidelines:
    - "Avoid direct use of eval or Function constructor."
    - "Use parameterized DB access; do not build raw SQL with user input."
    - "Keep route/controller files thin and move business logic to services."

standards:
  imports:
    - rule: "forbid_pickle"
      pattern: "import\\s+pickle|from\\s+pickle\\s+import"
      in_dirs:
        - "app/"
      message: "Do not use pickle in runtime code."
  naming:
    - rule: "python_service_naming"
      pattern: "^[a-z_]+\\.py$"
      in_dirs:
        - "app/services/"
      message: "Service modules must use snake_case file naming."
  structure:
    - rule: "require_readme"
      path: "README.md"
      required: true
      message: "Repository must include README.md."
    - rule: "require_security_doc"
      path: "docs/SECURITY.md"
      required: true
      message: "Security policy must be documented in docs/SECURITY.md."

exclude:
  - "tests/"
  - "node_modules/"
  - ".git/"
  - ".next/"
  - "dist/"
```

---

## Section-by-Section Reference

### `security`

```yaml
security:
  enabled: true
  block_on_severity:
    - ERROR
    - WARNING
```

- `enabled`: turn security gate on/off.
- `block_on_severity`: list of severities that fail CI.
- Common policy:
  - strict: `ERROR + WARNING`
  - balanced: `ERROR` only

---

### `quality`

```yaml
quality:
  enabled: true
  block_on_severity: []
```

- `enabled: true` adds quality-focused Semgrep packs.
- `block_on_severity` is currently informational in many setups; primary CI gate is driven by `security.block_on_severity`.

---

### `practices`

```yaml
practices:
  enabled: true
  block_on_severity:
    - ERROR
  guidelines:
    - "Do not keep business logic in controller files."
```

- `guidelines` must contain items, otherwise practice review has little/no effect.
- For AI-backed guidance, provide at least one API key in workflow env:
  - `OPENAI_API_KEY`
  - `ANTHROPIC_API_KEY`
  - `GEMINI_API_KEY`

---

### `standards` (Deterministic Rules)

These checks are regex/path based and do not require AI.

#### `standards.imports`
- List of rules with:
  - `pattern`: regex to detect disallowed imports/usage
  - `in_dirs`: optional directory scope
  - `message`: human-readable policy message

#### `standards.naming`
- List of rules with:
  - `pattern`: regex for file name format
  - `in_dirs`: directory scope
  - `message`: violation message

#### `standards.structure`
- List of rules with:
  - `path`: required path in repository
  - `required`: true/false
  - `message`: violation message

---

## Real-World Policy Profiles

### 1) Strict Security Gate (Recommended for production)

```yaml
security:
  enabled: true
  block_on_severity: [ERROR, WARNING]
```

### 2) Report-Only Pilot (Adoption phase)

```yaml
security:
  enabled: true
  block_on_severity: [ERROR]
```

Combine with action input:

```yaml
block_on_findings: "false"
```

### 3) Architecture Governance Mode

```yaml
standards:
  structure:
    - rule: "require_domain_layer"
      path: "app/domain"
      required: true
      message: "Domain layer folder must exist."
```

---

## Troubleshooting

### Only static findings appear

Check:
1. `practices.guidelines` is non-empty.
2. AI keys are present in workflow env if AI review is expected.
3. `standards` uses list-based rules (not custom object shapes).

### PR comment not posted

Check:
1. Workflow permissions include:
   - `contents: read`
   - `pull-requests: write`
2. Token is valid (`github_token` input or `${{ secrets.GITHUB_TOKEN }}`).
3. Repository/fork secret restrictions.

### Config appears ignored

Check:
1. File path is exactly `.ai-guardian.yml` at repository root.
2. YAML indentation is valid.
3. Exclude paths are correct for your project layout.

---

## Minimal Valid Config

```yaml
security:
  enabled: true
  block_on_severity:
    - ERROR
```

This is the smallest valid policy for CI gatekeeping.
