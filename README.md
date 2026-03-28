# Sentinel CI 🛡️

**Sentinel CI** is a professional-grade DevSecOps platform (built on the **AI Code Guardian** engine) that uses multi-agent AI to protect your codebase. It does not only find vulnerabilities — it understands your project's architecture and helps every Pull Request meet your standards.

[**View Technical Details & Architecture ➔**](./TECHNICAL_DETAILS.md)

---

## 🚀 Why Sentinel CI?

In the era of AI-generated code, security vulnerabilities and architectural drift are harder to spot than ever. Standard static analysis tools (SAST) often produce too many low-value alerts, leading to "alert fatigue."

**Sentinel CI helps by:**
- **Reducing Noise:** AI filters out false positives by understanding the surrounding code context.
- **Actionable Insights:** It does not just say "Error found"—it explains *why* it is a risk and *how* to fix it.
- **Multi-Agent AI**: Supports OpenAI, Anthropic, and Gemini with auto-failover.
- **Security Guardrails**: Maps findings to OWASP & CWE standards.
- **Architectural Enforcement**: Define your own "Project Laws" in plain English.
- **Clean Code Insights**: Automatically detects code smells and complexity.
- **Enforcing Standards:** Catches violations of your naming conventions and architectural patterns.
- **Gatekeeping:** Acts as a hard-fail gate in your CI/CD pipeline when you configure it to block merges.

---

## 🛠️ Getting Started

You can use the interactive setup wizard or manual configuration.

### 1️⃣ Interactive Setup (Recommended)
Run the installer in your terminal to scaffold everything you need in seconds.

```bash
curl -sL https://raw.githubusercontent.com/abin-g/sentinel-ci-action/master/setup.sh -o setup.sh
chmod +x setup.sh && ./setup.sh
```

### 2️⃣ Manual Integration
If you prefer total control, add the GitHub Action and configuration file yourself.

> See the [Manual Setup Guide](./SETUP.md).

---

## 📖 Explore the Documentation

| Document | Description |
|----------|-------------|
| [**Setup Guide**](./SETUP.md) | How to install and configure Sentinel CI in your project. |
| [**Rule Engine Guide**](./RULE_ENGINE.md) | In-depth `.sentinel-ci.yml` reference, schema, policies, and troubleshooting. |
| [**Feature & AI Guide**](./FEATURES.md) | AI agents and how to test/enable them. |
| [**Error & Analysis Reference**](./ERROR_CODES.md) | Findings, severity levels, and troubleshooting. |
| [**Roadmap & Lifecycle**](./ROADMAP.md) | Direction and upcoming features. |

---

## 🛡️ Governance & Policy

Sentinel CI uses a policy-driven approach. Define what severities block a merge in your `.sentinel-ci.yml` file. By default, many setups block Pull Requests containing **ERROR** level security findings (you can add **WARNING** for strict mode). Legacy `.ai-guardian.yml` is still read if `.sentinel-ci.yml` is missing.

> **Note:** The GitHub Action package may still be published as `abin-g/sentinel-ci-action` for backward compatibility.

---

## 🤝 Contributing & Support

We welcome contributions! If you encounter issues or have questions about scan results, check our [Error Reference](./ERROR_CODES.md) or open an issue in [this repository](https://github.com/abin-g/sentinel-ci-action/issues).

---

## ⚖️ License

This project is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**. See the [LICENSE](./LICENSE) file for details.
