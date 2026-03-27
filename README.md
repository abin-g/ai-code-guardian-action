# AI Code Guardian 🛡️

**AI Code Guardian is a professional-grade DevSecOps platform that uses Multi-Agent AI to protect your codebase. It doesn't just find vulnerabilities — it understands your project's specific architecture and ensures every Pull Request meets industrial standards.

[**View Technical Details & Architecture ➔**](./TECHNICAL_DETAILS.md)

---

## 🚀 Why AI Code Guardian?

In the era of AI-generated code, security vulnerabilities and architectural drift are harder to spot than ever. Standard static analysis tools (SAST) often produce too many low-value alerts, leading to "alert fatigue."

**AI Code Guardian solves this by:**
- **Reducing Noise:** AI filters out false positives by understanding the surrounding code context.
- **Actionable Insights:** It doesn't just say "Error found"—it explains *why* it's a risk and *how* to fix it.
- **Multi-Agent AI**: Supports OpenAI, Anthropic, and Gemini with auto-failover.
- **Security Guardrails**: Maps findings to OWASP & CWE standards.
- **Architectural Enforcement**: Define your own "Project Laws" in plain English.
- **Clean Code Insights**: Automatically detects code smells and complexity.
- **Enforcing Standards:** Automatically catches violations of your project's specific naming conventions and architectural patterns.
- **Gatekeeping:** Acts as a hard-fail gate in your CI/CD pipeline to prevent critical vulnerabilities from being merged.

---

## 🛠️ Getting Started

We've made setup as simple as possible. You can choose between our interactive setup wizard or manual configuration.

### 1️⃣ Interactive Setup (Recommended)
Run our smart installer directly in your terminal to scaffold everything you need in seconds.
```bash
curl -sL https://raw.githubusercontent.com/abin-g/ai-code-guardian-action/master/setup.sh -o setup.sh
chmod +x setup.sh && ./setup.sh
```

### 2️⃣ Manual Integration
If you prefer total control, you can manually add the GitHub Action and configuration file.
> See the [Manual Setup Guide](./SETUP.md#manual-installation).

---

## 📖 Explore the Documentation

| Document | Description |
|----------|-------------|
| [**Setup Guide**](./SETUP.md) | How to install and configure AI Code Guardian in your project. |
| [**Rule Engine Guide**](./RULE_ENGINE.md) | In-depth `.ai-guardian.yml` reference, schema, policies, and troubleshooting. |
| [**Feature & AI Guide**](./FEATURES.md) | Exploration of AI agents and how to test/enable them. |
| [**Error & Analysis Reference**](./ERROR_CODES.md) | Detailed breakdown of findings, severity levels, and troubleshooting. |
| [**Roadmap & Lifecycle**](./ROADMAP.md) | Where the project is headed and upcoming AI features. |

---

## 🛡️ Governance & Policy

AI Code Guardian uses a policy-driven approach. You can define what severities block a merge in your `.ai-guardian.yml` file. By default, it blocks any Pull Request containing **CRITICAL (ERROR)** level security findings.

---

## 🤝 Contributing & Support

We welcome contributions! If you encounter issues or have questions about specific scan results, check our [Error Reference](./ERROR_CODES.md) or open an issue in [this repository](https://github.com/abin-g/ai-code-guardian-action/issues).

---

## ⚖️ License

This project is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**. See the [LICENSE](./LICENSE) file for details.
