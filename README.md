# zIntent Guard: Intent-Aware Behavioral Guardrails for Autonomous Agents

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Framework: PyTorch](https://img.shields.io/badge/Framework-PyTorch-EE4C2C.svg)](https://pytorch.org/)
[![Classifier: XGBoost](https://img.shields.io/badge/Model-XGBoost-blue.svg)](https://xgboost.readthedocs.io/)
[![Mainframe: IBM Z](https://img.shields.io/badge/Platform-IBM%20Z%20%2F%20LinuxONE-052FAD.svg)](https://www.ibm.com/it-infrastructure/z)

An intent-aware, microsecond-scale security layer designed to intercept autonomous agent actions, extract semantic intent, run behavioral risk models, and enforce stateful deterministic constraints on high-performance enterprise transaction systems.

---

## 📖 Table of Contents
1. [Project Overview](#-project-overview)
2. [System Architecture](#-system-architecture)
3. [Mainframe Threat Vectors (T1–T10)](#-mainframe-threat-vectors-t1t10)
4. [Dataset Ingestion Details](#-dataset-ingestion-details)
5. [Multi-Stage Guard Pipeline](#-multi-stage-guard-pipeline)
6. [IBM Enterprise Infrastructure Deployment Map](#-ibm-enterprise-infrastructure-deployment-map)
7. [Evaluation & Baseline Performance](#-evaluation--baseline-performance)
8. [How to Use the Notebook](#-how-to-use-the-notebook)

---

## 🌟 Project Overview

As autonomous AI agents are increasingly granted execution tools over enterprise resources, they introduce critical vulnerabilities. High-performance transaction mainframes require protection from malicious instruction bypasses, privilege escalations, and Time-of-Check to Time-of-Use (TOCTOU) concurrency manipulation.

**zIntent Guard** addresses this by establishing an independent outer guardrail system. It intercepts agent actions *before* execution, verifies underlying semantic goals, runs continuous ML risk models, and executes atomic policy constraints safely within mainframe parameters.

---

## 🏗️ System Architecture

```
                      Autonomous AI Agents
                                │
       [LLM agents, Enterprise Copilots, Automated APIs]
                                │
                                ▼
             ┌─────────────────────────────────────┐
             │        zIntent Guard Runtime        │
             ├─────────────────────────────────────┤
             │  1. Intent Extraction (MiniLM)      │
             │  2. Tabular Risk Analysis (XGBoost) │
             │  3. Deterministic Policy DSL Engine │
             │  4. Centralized Audit Log Engine    │
             └──────────────────┬──────────────────┘
                                │
         ┌──────────────────────┼──────────────────────┐
         ▼                      ▼                      ▼
     [ ALLOW ]              [ REVIEW ]             [ BLOCK ]
         │                      │                      │
         ▼                      ▼                      ▼
   Execute Action         MFA/Human Step        Prevent Execution
         │                      │                      │
         └──────────────┬───────┴──────────────────────┘
                        ▼
          Protected Enterprise Systems (IBM Z / LinuxONE)
     [Banking Apps · Databases · Core Transaction Systems]
```

---

## 🛡️ Mainframe Threat Vectors (T1–T10)

zIntent Guard successfully identifies and neutralizes all ten core threat vectors defined in modern AI safety frameworks:
* **T1: Prompt Injection / Instruction Override**: Attempts to hijack instructions (e.g. "*Ignore previous security rules and...*").
* **T2: Privilege Abuse**: Unauthorized escalation commands targeting system privileges.
* **T3: Loop Drain Attack**: Continuous iterations designed to exhaust computational/financial balances.
* **T4: Semantic Intent Drift**: Subtle rewording masking harmful actions behind benign context.
* **T5: TOCTOU Concurrency Exploits**: Attempting race conditions before execution locks are established.
* **T6: Limit Ceilings Bypass**: Transactions requesting amounts exceeding maximum transaction thresholds.
* **T7: Forbidden Resource Allocation**: Requests targeting unverified external APIs or foreign bank routing keys.
* **T8: Automated API Spoofing**: Scripts masquerading as verified system orchestrators.
* **T9: Credential Hijacking**: Bypassing MFA protocols under false pre-conditions.
* **T10: Account Takeover Anomaly**: Requests mimicking administrative command channels.

---

## 📊 Dataset Ingestion Details

The guard engine supports loading structured threat and benign data profiles from production-ready schemas:
* `tools.json`: API parameter definition schemas for deterministic policy checking.
* `user_cases.jsonl`: Clean benign queries mapping standard operational requests.
* `attacker_cases_ds.jsonl` / `attacker_cases_dh.jsonl`: Advanced attacks mimicking complex data security and dependency-hijack intrusions.
* `test_cases_*_base.json` / `test_cases_*_enhanced.json`: Structured benchmark templates mapped to expected execution decisions.

---

## ⚙️ Multi-Stage Guard Pipeline

1. **Semantic Intent Extractor**: Evaluates natural language inputs using a lightweight HuggingFace encoder (`all-MiniLM-L6-v2`) mapped to a custom trainable 2-layer PyTorch MLP classifier. Low confidence scores trigger an immediate safe fallback mode.
2. **Deterministic Policy DSL Engine**: Applies strict boundaries on parameters (e.g., maximum transaction limits, blacklisted keywords, state versioning checks to prevent TOCTOU anomalies).
3. **Continuous XGBoost Risk Regressor**: Extracts a 5-dimensional feature array (semantic drift, behavioral deviation, transaction/balance ratio, resource consequence severity, boundary limit proximity) to score transaction risk.
4. **Multi-Tier Decision Bounds**: Routes transactions to `ALLOW`, `REVIEW` (MFA escalation), or `BLOCK` states.

---

## 💻 IBM Enterprise Infrastructure Deployment Map

| Prototype Component | IBM Z / LinuxONE Deployment Implementation |
| --- | --- |
| **Intent Model** | Exported to ONNX and deployed inside FastAPI container running on IBM LinuxONE. |
| **Risk & Policy Engine** | Containerized Python microservice orchestrated via **Red Hat OpenShift**. |
| **Inference Acceleration** | Accelerated using the **IBM Telum II** integrated AI accelerator chip for ultra-low latency. |
| **Mainframe Systems** | Integrated directly into banking/transaction databases through enterprise API interfaces. |
| **Logging** | Cryptographically signed, immutable audit logs integrated with IBM security logging pipelines. |

---

## 📈 Evaluation & Baseline Performance

zIntent Guard is evaluated against classic access control models (**RBAC** and **ABAC**), demonstrating superior security boundaries and resilient detection:

* **Recall / Threat Detection**: **90.3%** vs. RBAC's **24.2%**
* **F1-Score**: **0.836** (zIntent Guard) vs. **0.316** (ABAC Baseline)
* **Latency**: Highly optimized performance yielding sub-millisecond execution times on real architectures, significantly outperforming LLM-In-The-Loop methods.

---

## 🚀 How to Use the Notebook

1. Run **Cell 1** to initialize directory architecture and load core dependencies.
2. Run **Cells 2-6** to generate datasets, train models, and stand up the guard pipeline.
3. Run **Cell 8** to generate comparison metrics, statistical Wilcoxon validation, and latency CDF curves.
4. Use **Cell 10 / 11** to interactively test benign and suspicious prompt flows in the playground sandbox!
