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

### Installation & Setup


### System Architecture

This project utilizes a **Multi-Agent** approach or "Separation of Duties":  
- **Agent A** (Privacy Auditor): Uses a deterministic **Regex Tool** to scan for some **hard rules** (PII) such as IBANs
- **Agent B** (Security Expert): Uses LLM reasoning to detect **subjective **, malicious intent and prompt injection for instance.

### Tech Stack


