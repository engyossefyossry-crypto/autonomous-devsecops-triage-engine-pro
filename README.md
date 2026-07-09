<h1 align="center">🚨 Autonomous DevSecOps Triage Engine PRO</h1>

<h3 align="center">Enterprise-Grade Multi-Agent Incident Commander, Observability Metric Core & Self-Healing Telemetry Pipeline</h3>

<p align="center">
  <img src="https://img.shields.io/badge/Automation-n8n-FF6C37?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/Inference-Groq_API-F54E42?style=for-the-badge&logo=fastapi&logoColor=white" alt="Groq">
  <img src="https://img.shields.io/badge/Model_Mesh-OpenRouter-007ACC?style=for-the-badge&logo=openaccess&logoColor=white" alt="OpenRouter">
  <img src="https://img.shields.io/badge/Observability-Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white" alt="Grafana">
  <img src="https://img.shields.io/badge/Security-DevSecOps_Hardened-38A169?style=for-the-badge&logo=dataguard&logoColor=white" alt="Security">
</p>

---

## 📖 The Evolution: Moving from Basic Automation to LLMOps

The original DevSecOps Triage Engine proved that AI could manage an incident response cycle. However, real production systems do not operate on a happy path. Network APIs fail, rate limits choke models, and independent AI agents can generate conflicting analyses or experience hallucinations.

The **PRO Version** represents a complete paradigm shift in AI orchestration. Instead of blindly executing sequential actions, **Triage Engine PRO** treats LLMs as raw compute resources that must be routed dynamically, audited heavily, and protected by deterministic code boundaries. It utilizes a highly resilient, self-healing **Evaluation Pipeline** featuring parallel agent swarms, confidence-aware QA gatekeeping, granular infrastructure exception handling, and real-time Grafana observability telemetry.

---

## 🏗️ Architectural Topology & Dual-Track Execution

The core runtime separates processing vectors into two distinct, isolated paths: a **Success Track** governed by a high-tier QA Auditor, and an **Error Track** that captures infrastructure faults (like LLM rate limits) to build machine-readable anomaly reports without crashing the pipeline.

```text
                              [ Reactive Incident Webhook ] 
                                             │
                                             ▼
                                  [ Data Preparer Node ]
                                             │
                                             ▼
                                  [ Supervisor Orchestrator ]
                                             │
             ┌───────────────────────────────┴───────────────────────────────┐
             ▼ (SUCCESS TRACK: Parallel Inference Swarm)                     ▼ (FAILURE TRACK: Active Fault Interception)
   ┌───────────────────┼───────────────────┐                        [ Node API Crash / Network Timeout ]
   ▼                   ▼                   ▼                                         │
┌─────────────┐ ┌─────────────┐ ┌─────────────┐                                      ▼
│  Hardcore   │ │    Risk     │ │   PR & Status │                                [ Switch Node ]
│  Developer  │ │  Evaluator  │ │   Manager   │                   ┌──────────────────┼──────────────────┐
└──────┬──────┘ └──────┬──────┘ └──────┬──────┘                   ▼                  ▼                  ▼
       │               │               │                  [429/Timeout]       [400/Bad Input]     [Other Exceptions]
       └───────────────┼───────────────┘                          │                  │                  │
                       ▼                                          └──────────────────┼──────────────────┘
             [ Merge by Position ]                                                   ▼
                       │                                                    [ Set Error Schemas ]
                       ▼                                                             │
             [ Auditing Inspector ]                                                  ▼
                       │                                                    [ Error Informer ]
                       ▼                                                             │
            [ Pass / Fail IF Gate ]                                                  │
             ┌─────────┴─────────┐                                                   │
             ▼ (Pass)            ▼ (Fail/Contradiction)                              │
             │                   └───────────────────┬───────────────────────────────┘
             ▼                                       ▼
  [ Update Grafana Dashboard ]             [ Deterministic Aggregator Layer ]
             │                                       │
             └───────────────────┬───────────────────┘
                                 ▼
                     [ Final Output Formatter ]
                                 │
         ┌───────────────┬───────┴───────┬───────────────┬───────────────┐
         ▼               ▼               ▼               ▼               ▼
  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐
  │ Slack Devs │  │ Gmail HTML │  │ Discord HQ │  │ GitHub     │  │ Telegram & │
  │ Markdown   │  │ Executives │  │ Rich Embed │  │ Bug Ticket │  │ Sheets Log │
  └────────────┘  └────────────┘  └────────────┘  └────────────┘  └────────────┘
```

---

## 🧠 Strategic AI Model Mesh (The Orchestration Rationale)

Relying on a single AI model for complex system architecture leads to context drift and latency bottlenecks. This engine uses a **decoupled multi-model mesh**, routing specific operational tasks to models explicitly optimized for those workloads:

| Agent Role | Assigned Model | Provider | Strategic Rationale |
| :--- | :--- | :--- | :--- |
| **Supervisor & QA Inspector** | `llama-3.3-70b-versatile` | Groq | **The State Machine:** Operates on Groq's ultra-low latency compute layers. Chosen for its strict instruction-following capabilities. It acts purely as a routing and validation gatekeeper, ensuring strict JSON schema compliance and cross-examining worker agents for hallucinations. |
| **Hardcore Developer** | `gemini-2.5-flash-lite` | OpenRouter | **The Forensic Analyst:** Code forensics requires parsing massive, chaotic stack traces. Gemini 2.5 Flash offers a massive context window and rapid processing speed, making it perfect for isolating broken scripts and writing pseudo-code patches. |
| **Risk Evaluator** | `gemma-4-31b-it` | OpenRouter | **The Compliance Auditor:** Strong logical weighting and security guardrails make Gemma ideal for threat modeling, calculating CVE impact, and defining strict network isolation protocols without hallucinating fake vulnerabilities. |
| **PR & Status Manager** | `gpt-oss-20b` | OpenRouter | **The Communicator:** Excellent at synthesizing highly technical jargon into clear, empathetic human prose for public status pages, while keeping internal Slack updates crisp and operational. |
| **Error Informer** | `gpt-oss-120b` | Groq | **The Telemetry Engine:** A heavyweight model deployed strictly on the Error Track to parse complex n8n infrastructure crashes and translate raw pipeline failures into actionable executive summaries. |

---

## 📊 Internal Data Ledger Schemas (n8n Data Tables)

To ensure full historical transparency, individual sub-agents interact directly with native **n8n Data Tables**. This ensures an immutable audit log is generated *during* the execution turn, independent of external API delivery success.

### 1. Forensics Databank (`Store Debugging Attempt`)
* `incident_id`: The trackable unique identifier (e.g., INC-123456).
* `target_file`: Isolated source script context path.
* `line_number`: Exact numerical line allocation within the broken file.
* `patch_snippet`: The emergency code mitigation patch or recommended syntax.

### 2. Compliance Databank (`Store Evaluation Attempt`)
* `incident_id`: Cross-reference token.
* `risk_score`: Evaluated threat level (CRITICAL, HIGH, MEDIUM, LOW).
* `compliance_impact`: Granular diagnostic assessing database exposure or GDPR leaks.
* `containment_protocol`: Step-by-step system isolation or cluster container rules.

### 3. Communications Databank (`Store Current Status`)
* `incident_id`: Cross-reference token.
* `slack_published`: Tracking signature detailing the engineering alert state.
* `status_page_published`: Verification payload detailing external public communications.

---

## 🛠️ Advanced Engineering Pillars

### 1. Parallel Agent Swarm & Confidence Scoring
Instead of running agents sequentially (which multiplies latency), the Developer, Risk Evaluator, and PR Manager execute **simultaneously**. Furthermore, each agent is required to output a **Confidence Score (0.0 to 1.0)**. If an agent is guessing due to poor log quality, it must mathematically declare its uncertainty.

### 2. The QA Inspector (Gatekeeper Node)
Before any data reaches the outside world, the **Inspector** agent catches the merged output of all three workers. It cross-examines the data for structural consistency. If the Developer suggests a patch that violates the Risk Evaluator's containment protocol, or if any agent's Confidence Score drops below 0.4, the Inspector **fails the execution** and routes it to the Error Track to prevent hallucinated data from reaching the production database.

### 3. Self-Healing Error Track & Regex Switching
If the Groq or OpenRouter APIs crash due to Rate Limits (429), Context Limits (400), or Gateway Timeouts (504), the pipeline does not freeze. A **Switch Node** uses strict Regex boundaries to catch the exception type, applies a fallback schema, and triggers the **Error Informer** to alert the engineering team that the *automation pipeline itself* is degraded.

### 4. Real-Time Grafana Telemetry
Every successful triage sequence generates a structured payload pushed directly to a **Grafana Dashboard**. It logs the `classification` type, `risk_score`, and the `confidence_scores` of the AI swarm, giving directors a live quantitative view of both system stability and AI performance.

---

## 🚀 Installation & Deployment

### Prerequisites
* A running instance of **n8n v1.0+** (Self-hosted or Cloud).
* Active API credentials for **Groq** and **OpenRouter**.
* Configured targets: **GitHub PAT**, **Slack/Discord Webhooks**, **Telegram Bot**, **Gmail**, and **Google Sheets Service Accounts**.
* (Optional) **Grafana** instance for dashboard telemetry injection.

### Import Instructions
1. Clone this repository locally.
2. Open your n8n workspace dashboard and click **Create New Workflow**.
3. Click the options menu in the top right corner and select **Import from File**.
4. Upload the `autonomous-devsecops-triage-engine-pro.json` file.
5. Re-link your specific credential profiles to the respective AI and Communication nodes.
6. Verify your n8n Data Tables are created matching the schemas outlined above.
7. Toggle the workflow to **Active** and fire a test payload!

---

## 📜 License

This project is open-source and available under the terms of the **MIT License**. Feel free to fork it, modify the agent prompts, and build your own autonomous infrastructure sentries.
