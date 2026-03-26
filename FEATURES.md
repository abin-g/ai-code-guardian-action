# AI Code Guardian: Features & AI Capabilities 🚀

AI Code Guardian is more than just a static scanner. It combines the speed of local security tools with the intelligence of modern Large Language Models (LLMs).

---

## 🌟 Core Features

### 1. Multi-Agent AI Analysis (New!)
The engine now supports three of the most advanced AI models in the world. When enabled, the tool extracts the actual code context and sends it to your choice of AI for a expert-level security review.

- **Anthropic Claude 3.5 Sonnet**: Our recommended model for high-precision security fixes.
- **OpenAI GPT-4o**: Excellent for general-purpose security and context-aware explanations.
- **Google Gemini 1.5 Pro**: Great for analysis of large codebases and complex patterns.

### 2. Intelligent Auto-Failover
If you configure multiple AI providers, the system will automatically handle failovers. If one service is down or you hit a rate limit, AI Code Guardian will instantly try the next available agent.

### 3. Local-First Security Scanning
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
