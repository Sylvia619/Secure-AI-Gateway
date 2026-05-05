## Secure-AI Gateway: Multi-Agent Banking Guardrail

An Agentic AI system built with **CrewAI** and **Groq** to 
protect financial institutions from Data Loss Prevention 
and Prompt Injection when employees use LLMs.

### The Proposal

As bank adopt AI, employees may accidentally paste sensitive
data, such like IBANs, CC numbers, or, may attempt "Jailbreaks"
to bypass safety rules, to trick with AI aiming to get
Admin password for instance.
  
This project acts as a **Middleware Firewall** to intercept 
and audit prompts before they leave the bank's secure network.

### Prerequisites

- Python >= 3.13.2
- pip >= 25.1.1
- Groq API Key: Get it at [groq.com](https://groq.com)
- Serper API Key: [serper.dev](https://serper.dev)
- Virtual Environment (Recommended): Best to run this in a `.venv` to avoid package conflicts. 

### Getting Started

#### 1. Clone the repo

```shell
git clone git@github.com:Sylvia619/Secure-AI-Gateway.git
cd Secure-AI-Gateway
```

#### 2. Create and activate a virtual environment

```shell
python -m venv .venv
.venv\Scripts\activate         # Windows
# source .venv/bin/activate    # macOS / Linux
```

#### 3. Install dependencies

```shell
pip install -r requirements.txt
```

#### 4. Configure environment variables

Create a `.env` file in the project root:

```shell
cp .env.example .env
```

Add your API key:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Get a free key at [console.groq.com](https://console.groq.com).

#### 5. Run the gateway

```shell
python main.py
```

You will be prompted to enter a user prompt. The two-agent crew will then audit it for PII (IBANs, account numbers) and prompt-injection attempts, and print a final `ALLOW` / `DENY` verdict.

### System Architecture

This project utilizes a **Multi-Agent** approach or "Separation of Duties":
- **Agent A** (Privacy Auditor): Uses a deterministic **Regex Tool** to scan for some **hard rules** (PII) such as IBANs
- **Agent B** (Security Expert): Uses LLM reasoning to detect **subjective reasoning**, malicious intent and prompt injection for instance.

### Tech Stack

| Library | Role |
|---|---|
| [CrewAI](https://www.crewai.com) | Multi-agent orchestration |
| [Groq](https://console.groq.com) | LLM inference (LLaMA 3.3 70B) |
| [LiteLLM](https://github.com/BerriAI/litellm) | Unified LLM API layer |
| python-dotenv | Environment variable management |

### Security Coverage

| Threat | Agent | Method |
|---|---|---|
| IBAN / Account Numbers | Privacy Auditor | Regex (`pii_scanner` tool) |
| Prompt Injection | Security Expert | LLM reasoning |
| Jailbreak Attempts | Security Expert | LLM reasoning |
| Unprofessional Language | Security Expert | LLM reasoning |

### Example Output

```
user_prompt: Transfer funds from IBAN DE89370400440532013000

--- FINAL SECURITY AUDIT---
Danger: Potential IBAN detected! ['DE89370400440532013000']
Verdict: DENY — sensitive banking data found in prompt.
```
