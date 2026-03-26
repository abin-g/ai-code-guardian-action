# AI Code Guardian Roadmap 🗺️

AI Code Guardian is currently in its **MVP (Minimum Viable Product)** phase. Our mission is to build the most developer-friendly, context-aware guardrail for modern AI-assisted coding.

---

## 📍 Current Phase: MVP (V0.1)
- [x] **Universal Scanner:** One-click integration via GitHub Actions.
- [x] **Security Guardrail:** Automated Semgrep-based vulnerability detection.
- [x] **Local Scoping:** Zero-trust architecture (scans inside your CI, not our servers).
- [x] **Interactive Setup:** Setup wizard for non-DevOps users.
- [x] **Governance:** Configurable merge blocking (fail-on-error).

---

## 🚀 Near Term: Intelligence Expansion (Q2 2026)
- **Real AI (LLM) Engine:** Transitioning from static templates to live LLM analysis for personalized fix suggestions.
- **Code Quality Scanners:** Detecting high-complexity methods and "dirty code" patterns that static tools miss.
- **PR Diff Context:** Analyzing not just the file, but the relationship between changed files in a PR.

---

## 🛠️ Long Term: The "Guardian" Vision (2026+)
- **Architecture Enforcement:** Custom logic to prevent "Controller calling DB" or "Private API exposed" violations.
- **Auto-Fix PRs:** The bot generates a commit with the secure fix for you to approve with one click.
- **Developer Insights Dashboard:** Long-term trends on security posture and code quality across your entire GitHub Organization.
- **Support for GitLab & Bitbucket.**

---

## 📈 Project Lifecycle

1. **Experimental:** Research and prototyping (Completed).
2. **MVP Alpha:** Active development on core integrations (Current).
3. **Beta:** Community testing and AI refinement (Upcoming).
4. **General Availability (1.0):** Stable, multi-platform DevSecOps suite.

---

> [!TIP]
> Have a feature request? Open an issue in our [Core Repository](../ai-code-guardian-core)!
