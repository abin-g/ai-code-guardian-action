# Technical Details & Architecture

AI Code Guardian is not just another wrapper around an LLM. It is a sophisticated, hybrid-analysis engine designed to provide industrial-grade security and architectural governance.

## 🏗️ How It Works (The Core Engine)

The platform follows a **"Static-Analysis First, AI-Refined"** methodology. This ensures that every finding is grounded in real code patterns before the AI provides context.

### 1. The Scanning Layer (Industrial Standards)
We leverage **Semgrep**, the industry standard for lightweight static analysis. 
- **Standards**: Our rulesets are mapped directly to **OWASP Top 10** and **CWE (Common Weakness Enumeration)**.
- **Rulesets**:
    - `p/security-audit`: Deep security checks for vulnerabilities.
    - `p/secrets`: Detection of hardcoded keys and tokens.
    - `p/ci` & `p/default`: Industry-standard code quality and maintainability rules.

### 2. The AI Intelligence Layer (Multi-Agent)
Finding a bug is only half the battle. Explaining it and fixing it is the other half.
*   **Context Extraction**: Our engine extracts the specific code lines and surrounding context from the scanner output.
*   **Orchestration**: We use a priority-based failover system. If OpenAI is throttled, the agent automatically switches to Anthropic or Gemini.
*   **Data Privacy**: Only the specifically flagged code snippets are sent for analysis, minimizing exposure.

### 3. The Practices Enforcer (Our Core USP) 📐
Unlike Snyk or SonarQube, AI Code Guardian understands **your project's specific laws**.
*   **Structure Analyzer**: We generate a manifest of your repository's file tree and module dependencies.
*   **Architectural Guardrails**: The AI evaluates code against your custom guidelines (e.g., "Services must not call Repositories diretamente").
*   **Contextual Reasoning**: It uses the file path and repo structure to determine if a pattern is a violation (e.g., an unsafe import in a Production file vs. a Test file).

---

## 🆚 Comparison with Other Platforms

| Feature | Snyk / SonarQube | AI Code Guardian |
| :--- | :--- | :--- |
| **Security Coverage** | Excellent (Static) | Excellent (Static + AI Explanations) |
| **Custom Architecture** | Hard to define (Regex only) | **Natural Language Guidelines** |
| **Suggested Fixes** | Templates | **Contextual Code Fixes** |
| **Developer UX** | High noise / Generic | Human-readable & Grouped Findings |
| **Multi-LLM Choice** | Vendor Locked | **Any Provider (OpenAI, Gemini, Anthropic)** |

---

## 🛠️ Technical Methodology

### Security Matrix
We evaluate findings across three core dimensions:
1.  **Severity**: Impact on the system (ERROR vs. WARNING).
2.  **Exploitability**: How easy is it for an attacker to reach this code?
3.  **Remediation Effort**: How complex is the suggested fix?

### AI Agent industrial Standards
Our AI Agents use a **"Expert Chain-of-Thought"** prompt engineering technique. When performing a review:
1.  **Identify**: Pinpoint the exact line of risk.
2.  **Verify**: Cross-reference with the project structure to avoid false positives.
3.  **Correct**: Generate a fix that respects the existing coding style and imports.

## 🔐 Reliability & Failover
Because security never sleeps, our engine includes a **Static Fallback Mode**. If all AI providers are down, the system automatically detects this and serves high-quality, pre-computed security templates. Your PRs will **never** be blocked by provider downtime.
