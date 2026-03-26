# AI Code Guardian: Features & AI Capabilities 🚀

AI Code Guardian is more than just a static scanner. It combines the speed of local security tools with the intelligence of modern Large Language Models (LLMs).

---

## 🚀 Principal Features

### 1. Multi-Agent AI (Orchestrator)
Currently supports **OpenAI (GPT-4o)**, **Anthropic (Claude 3.5 Sonnet)**, and **Google Gemini (1.5 Pro)**. The orchestrator automatically handles priority and failover, ensuring your PRs are never blocked by a single provider's downtime.

### 2. Repo-Wide Context Awareness (Requirement 45) 🧠
Unlike basic scanners, AI Code Guardian understands your entire project. It detects your tech stack (e.g., FastAPI, Django, React) and key dependencies to provide fixes that respect your existing libraries and coding style.

### 3. Project-Specific Practices Enforcer (Requirement 2C) 📐
Define your own "Project Laws." Want to forbid direct DB calls from Controllers? Or enforce a specific naming convention? Just add it to your guidelines, and the AI will enforce it during every PR.

### 4. Smart Code Quality & Maintenance (Requirement 2B) ✨
Automatically detects "Code Smells," high cyclomatic complexity, and maintainability risks, grouping them separately from security vulnerabilities for a cleaner developer experience.

### 5. Intelligent Auto-Failover
If you configure multiple AI providers, the system will automatically handle failovers. If one service is down or you hit a rate limit, AI Code Guardian will instantly try the next available agent.

### 6. Local-First Security Scanning
We use **Semgrep** to perform initial scans directly on your CI/CD runner. This means your raw source code is never uploaded to our servers—only the specific flagged snippets are sent to your chosen AI provider for analysis.

---

## 🧪 How to Enable & Test AI Feedback

By default, the tool uses static templates. To enable real-time AI analysis, follow these steps:

### Step 1: Get an API Key
You can use any of the following providers:
- **OpenAI**: [Get API Key here](https://platform.openai.com/api-keys)
- **Anthropic**: [Get API Key here](https://console.anthropic.com/settings/keys)
- **Google Gemini**: [Get API Key here](https://aistudio.google.com/app/apikey)

### Step 2: Add Secrets to your Repository
1. Go to your GitHub Repository -> **Settings** -> **Secrets and variables** -> **Actions**.
2. Click **New repository secret**.
3. Add your key as:
   - `OPENAI_API_KEY`
   - `ANTHROPIC_API_KEY`
   - `GEMINI_API_KEY`
   *(Note: You only need one, but you can add multiple for failover support).*

### Step 3: Update your Workflow
Update your `.github/workflows/ai-code-guardian.yml` to pass the secret:

```yaml
      - name: Run AI Code Guardian
        uses: abin-g/ai-code-guardian-action@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
        env:
          # Add any or all of these to enable AI analysis
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
          GEMINI_API_KEY: ${{ secrets.GEMINI_API_KEY }}
```

### Step 4: Verify
Open a Pull Request. If the AI is configured correctly, your PR report will now contain a "🤖 Using AI Provider" message and detailed, code-specific fix suggestions!

---

## 🛠️ Feature Matrix

| Feature | Static Mode (Default) | AI Enhanced Mode |
|---------|-----------------------|------------------|
| Security Scan | ✅ Yes | ✅ Yes |
| Risk Score | ✅ Yes | ✅ Yes (More Accurate) |
| Fix Suggestions | 💠 Generic | 🧠 Context-Aware |
| Explanation | 💠 Rule-based | 🧠 Expert Analysis |
| Merge Blocking | ✅ Yes | ✅ Yes |
