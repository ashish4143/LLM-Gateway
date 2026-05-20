# LLM Gateway: Unified Multi-Provider Routing, Security Guardrails & Observability

A production-ready middleware architecture for managing, routing, securing, and observing interactions with multiple Large Language Model (LLM) providers (OpenAI, Groq, Anthropic, Gemini, and xAI/Grok) using **LiteLLM** and **LangChain**.

---

## 💡 The Core Problem This Solves

When building enterprise LLM applications, developers face several critical production challenges:
1. **SDK Fragmentation:** Managing separate codebases, payloads, and client SDKs for every model provider.
2. **Reliability & Outages:** System-wide downtime if a single provider (like OpenAI or Anthropic) goes down.
3. **Security & Privacy:** Risk of leaking Personally Identifiable Information (PII) or falling victim to prompt injection/jailbreak attempts.
4. **Cost & Latency Control:** Inability to dynamically route simple tasks to fast/cheap models and complex tasks to heavy models.
5. **Observability deficit:** Lack of real-time monitoring for call latency and precise execution costs.

This project implements an **LLM Gateway** that serves as a smart middleware layer to solve all five challenges.

---

## 🛠️ Core Capabilities

### 1. Unified Model Interface
Abstracts multiple proprietary and open-source models under a single, unified completion standard. Switch from `gpt-4o-mini` to `groq/llama-3.3-70b-versatile` or `xai/grok-beta` with a single string change.

### 2. Automatic Resilient Fallbacks
Implements automated error recovery. If a primary model experiences an outage, rate limit, or network failure, the gateway instantly falls back to alternative providers (e.g., failing over from Gemini to Groq) to guarantee 99.9% uptime.

### 3. Intelligent Semantic Routing
Analyses user queries at runtime to classify them into distinct categories (e.g., *code*, *summary*, *general*). It dynamically routes each query to the optimal model list, ensuring high-accuracy models are used for coding, while fast, lightweight models handle basic requests.

### 4. Enterprise-Grade Security Guardrails
Applies real-time pre-call filtering middleware to protect resources:
* **PII Redaction:** Instantly detects and redacts emails, phone numbers, SSNs, Aadhaar, PAN, and credit cards before they reach the model.
* **Injection Blockers:** Screens queries against common prompt-injection and jailbreak vectors.
* **Topic Enforcement:** Refuses queries that touch upon unsafe or blacklisted topics.

### 5. Latency & Cost Tracking
Captures call execution metrics (duration in seconds, input/output tokens) and calculates the exact USD cost per transaction, feeding structured metrics directly into downstream telemetry.

---

## 🧰 Tech Stack
* **Language:** Python 3.11+
* **Gateway Orchestrator:** `LiteLLM`
* **Workflow Framework:** `LangChain` / `langchain-community`
* **Configuration Management:** `python-dotenv`
* **Interactive Development:** Jupyter Notebooks (`.ipynb`)

---

## 🚀 Getting Started

### 1. Prerequisites
Clone the repository and ensure you have Python installed. It is recommended to run inside a virtual environment.

```bash
# Create and activate virtual environment
python -m venv .venv
.\.venv\Scripts\activate  # On Windows
source .venv/bin/activate  # On macOS/Linux

# Install dependencies
pip install -r requirements.txt
```

### 2. Environment Configuration
Create a `.env` file in the root directory and add your API keys:

```env
OPENAI_API_KEY=your_openai_key
GROQ_API_KEY=your_groq_key
ANTHROPIC_API_KEY=your_anthropic_key
GEMINI_API_KEY=your_gemini_key
XAI_API_KEY=your_xai_key
```

### 3. Execute the Walkthrough
Open the interactive Jupyter Notebook to step through the entire gateway implementation:

```bash
jupyter notebook llmGateway.ipynb
```

---

## 🔍 Why This Project Stands Out (For Reviewers & HRs)

This project avoids generic "Hello World" chatbot templates in favour of **real-world production design patterns**:

* **Resilience First:** Demonstrates a deep understanding of cloud service failures and high-availability design via simple-shuffle load balancing and automated routing failover.
* **Security Conscious:** Integrates active input sanitization, showing how compliance and privacy standards (like GDPR, HIPAA, or local data privacy laws) are practically enforced in LLM architectures.
* **FinOps and Cost Control:** Features structured telemetry (latency, token calculation, exact USD billing) to address the primary financial concerns of running AI at scale.
* **Modular Integration:** Designed with clean abstraction boundaries, making the gateway easy to plug into any existing LangChain or native Python application.
