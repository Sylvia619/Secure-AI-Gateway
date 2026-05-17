## 🛡️ Secure-AI Gateway: Multi-Agent Banking Compliance Guardrail

**Secure-AI Gateway** is a Proof of Concept (PoC) designed to solve 
the "Banking Secrecy vs. AI Innovation" dilemma. It implements 
a multi-agent "Guardrail" between bank employees and Large Language Models (LLMs) 
to ensure that sensitive data leaks and strategic vulnerabilities are caught 
before they reach public AI platforms.


### 🎯 The Proposal

As bank adopt AI, employees may accidentally paste sensitive
data, such like IBANs, CC numbers, or, may attempt "Jailbreaks"
to bypass safety rules, to trick with AI aiming to get
Admin password for instance.
  
This project acts as a **Middleware Firewall** to intercept 
and audit prompts before they leave the bank's secure network.


### ⚙️ Technical Setup
#### Prerequisites

- Python >= 3.13.2
- pip >= 25.1.1
- Groq API Key: Get it at [groq.com](https://groq.com)
- Virtual Environment (Recommended): Best to run this in a `.venv` to avoid package conflicts. 

#### Getting Started

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

Executing the script initiates a multi-layered security workflow: 
the system loads the latest corporate policy, audits the user prompt for 
both sensitive data and safety risks using specialized AI agents, 
and **pauses for a mandatory human sign-off**. Finally, the entire 
reasoning journey is recorded in a structured **Audit Trail (CSV)** and 
a final `ALLOW` / `DENY` verdict is issued.

#### Security Policy File
This external text file serves as the Governance Engine for 
the gateway. It contains the specific rules and risk boundaries 
that the AI agents must enforce during an audit. 
By keeping these rules in an external file rather than hard-coding 
them, the system allows Compliance Managers to update 
security protocols in real-time without modifying the underlying 
Python code. 

#### Audit Log File (.csv)
The **Audit Log** serves as the system's "Black Box" recorder, providing 
a comprehensive and time-stamped record of every security event. 
It is designed to ensure **Explainability** and **Accountability**—two critical 
requirements for AI in a regulated banking environment. 

### 🤖 System Architecture

- Multi-Agent Orchestration (The "Crew" Concept)
- Defense-in-Depth (Deterministic + Heuristic Layers)
- Policy-Driven Security (Dynamic Governance)
- Human-in-the-Loop (Accountability & Control)
- Auditability & Transparency (The Audit Trail)

### 🛠️ Tech Stack

| Category            | Technology | Application in Project |
|:--------------------| :--- | :--- |
| **Framework**       | CrewAI | Multi-agent framework for specialized security roles |
| **LLM**             | Llama 3.3-70B | Large Language Model providing heuristic reasoning via Groq |
| **Language**        | Python 3.11+ | Core programming for tool development and system logic |
| **Security Tools**  | Regex (re) | Deterministic scanning for 100% IBAN/PII detection accuracy |
| **Governance**      | Local .txt Integration | Dynamic reading of external corporate security policies |
| **Data Management** | CSV & Datetime | Structured logging for transparency and regulatory compliance |

### 🗺️ Library

| Library | Role |
|---|---|
| [CrewAI](https://www.crewai.com) | Multi-agent orchestration |
| [Groq](https://console.groq.com) | LLM inference (LLaMA 3.3 70B) |
| [LiteLLM](https://github.com/BerriAI/litellm) | Unified LLM API layer |
| python-dotenv | Environment variable management |


### 🚀 Security Coverage

| Threat | Agent | Method |
|---|---|---|
| IBAN / Account Numbers | Privacy Auditor | Regex (`pii_scanner` tool) |
| Prompt Injection | Security Expert | LLM reasoning |
| Jailbreak Attempts | Security Expert | LLM reasoning |
| Unprofessional Language | Security Expert | LLM reasoning |

### 💡 Example Output

```
user_prompt: Transfer funds from IBAN DE89370400440532013000

--- FINAL SECURITY AUDIT---
Danger: Potential IBAN detected! ['DE89370400440532013000']
Verdict: DENY — sensitive banking data found in prompt.
```
