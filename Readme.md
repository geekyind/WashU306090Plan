# 🎓 Strategic Roadmap: AI & MLOps Integration in IAM

**Role:** Engineering Manager, Identity & Access Management (IAM)  
**Organization:** Washington University in St. Louis  
**Primary Objective:** Modernize the IAM stack with AI/ML capabilities while maintaining current service excellence.
**Flexibility** This is a living document intended to evolve with the needs of the team.  It was created in a vacuum, is non-authoritative, and I can guarantee it will change according to university priorties.

---

## 🛑 Executive Abstract

### "Evolution through Intelligence."

WashU Identity Access Management (IAM) team is a high-performing unit supporting critical university infrastructure like Duende (IdentityServer), federated logins, and SSO for 40+ applications. The next strategic step in todays technology landscape is to transition from static rule-based security to **dynamic, AI-driven adaptive authentication**. This plan outlines a low-risk, incremental approach to layering AI solutions and Ops practices into our .NET ecosystem, ensuring stability while unlocking predictive security capabilities.

---

## 📅 Days 1-30: Discovery, Assessment & Stability

*Focus: "Do no harm." Understand the landscape and identify low-hanging fruit for AI without disrupting the current success.*

### 🔴 Top 3 Priorities

1. **Team Enablement & AI Tooling:** Interview the engineering team to identify skill gaps and introduce **GitHub Copilot** as a pair programmer to accelerate the team's transition from pure .NET to hybrid .NET/Python development.
2. **Deep Dive into Duende .NET Architecture:** Audit the existing identity stack to understand extension points for AI signals (e.g., `ICustomTokenRequestValidator` or event sinks).
3. **Data Quality & MLOps Readiness Assessment:** Evaluate currently logged events (federated login attempts, token requests) to determine if the data is "AI-ready" (clean, structured, labeled).

### 📝 Detailed Summary Days 0-30

The first month is dedicated to listening and learning. Integrating AI into a critical path like Authentication requires precision. We will begin by mapping the data flow of our 40+ dependent applications. Where are the logs stored? Are we capturing IP geolocation, device fingerprinting, and access times in a format a model can use? (structured logs?) We will also establish the **"MLOps Baseline"**—determining where our machine learning models will live in conjuction with the ML team. To support this shift, we will provision **GitHub Copilot/Azure Repos** licenses, allowing the team to use AI-assisted coding to bridge language barriers and generate boilerplate for the new components. By Day 30, we will have selected *one* specific use case for our first pilot (likely **Anomaly Detection**—e.g., detecting *Impossible Travel* events where a user logs in from two distant locations instantly, flagging *Abnormal Access Times* for sensitive admin portals, or identifying *Volume Spikes* in token requests).

---

## 📅 Days 31-60: Strategy, Prototyping & MLOps Foundation

*Focus: "Build the rails before the train." Establish the MLOps pipeline and build a non-blocking Proof of Concept.*

### 🟡 Top 3 Priorities

1. **Architect MLOps & Automated QA:** Implement **GitHub Actions** workflows with rigorous **automated testing** (unit/integration) to enable high **deployment velocity**. This establishes a "Zero Bug" quality gate, ensuring rapid iteration without thrashing in regression testing.
2. **AI-Enhanced Login Risk Score (POC):** Develop a lightweight model (or heuristic algorithm) that assigns a "risk score" to login attempts based on historical patterns.
3. **Shadow Mode Integration:** Deploy the risk scoring engine into production in **"Shadow Mode"** (logging scores only, taking no action) to validate system latency and accuracy.

### 📝 Detailed Summary Days 31-60

In this phase, we move from theory to code. We will introduce the foundations of MLOps by building **GitHub Actions** pipelines that automatically trigger model retraining and **comprehensive test suites** when new data arrives or code changes. By integrating QA directly into the CI/CD pipeline ("Shift Left"), we remove manual bottlenecks, allowing us to increase **deployment velocity** while adhering to a **Zero Bug** methodology. The critical deliverable is integrating this model with the Duende framework *without* affecting user experience. We will use a "Shadow Mode" deployment strategy: the .NET app will call the AI service asynchronously for every login, record the prediction (e.g., "High Risk"), but proceed with the login as normal. This allows us to measure the latency impact (KPI: adds < 50ms) and verify that the AI is accurate without locking out legitimate students or faculty.

---

## 📅 Days 61-90: Execution, Evaluation & Roadmap

*Focus: "Closing the loop." Move from observation to action and formalize the long-term vision.*

### 🟢 Top 3 Priorities

1. **Validate & Tune Shadow Models:** Analyze 30 days of "Shadow Mode" data to minimize False Positives and refine the model's decision boundary.
2. **First Active AI Feature (Step-Up Auth):** Transition the model from "Shadow" to "Active" for a small subset of users/apps. If Risk Score > X, trigger MFA (Step-Up Authentication).
3. **SOC Compliance & Governance Tooling:** Integrate **Microsoft Defender for Cloud** and automated evidence collectors (e.g., **Azure Policy**) to ensure the new AI flows comply with university SOC 2 mandates/controls.

### 📝 Detailed Summary

By Day 90, the foundation is solid. We will analyze the performance of our shadow model against real-world traffic. How many legitimate researchers would have been flagged as suspicious? We tune the model until the False Positive Rate is negligible. Once confident, we enable the **"Active Feedback Loop"**. Instead of just logging the risk, Duende will consume the risk score and dynamically require MFA for high-risk attempts. We will also finalize our compliance posture by enabling **code scanning workflows and immutable audit logs** in GitHub, ensuring that every AI decision path is traceable for auditors. We close the quarter by presenting a retrospective and a forward-looking roadmap to university leadership.

---

## 📊 Measuring Success: KPIs

We will measure progress using a balanced scorecard approach:

| Category | KPI Metric | Target (Day 90) |
| :--- | :--- | :--- |
| **AI/ML Quality** | **False Positive Rate (FPR)** | **< 0.1%** (Critical to avoid locking out faculty/students). |
| **Automation** | **MLops** | **100%** of new ML pipelines defined in Actions/YAML |
| **Automation** | **IAM Deploy** | **50%** of IAM pipelines defined in Actions/YAML |
| **Compliance** | **Audit Readiness** | **100%** of AI deployments have automated SOC evidence trails via GitHub Actions. |
| **MLOps** | **Model Retraining Cycle** | Capability to retrain and deploy a new model in **< 48 hours**. |
| **Operational** | **Authentication Latency** | AI inference adds **< 50ms** to total request time. |
| **Operational** | **Service Availability** | Maintain **99.99%** uptime for SSO/Duende during deployments. |
| **Quality** | **Defect Rate (Zero Bug)** | **0 Critical Bugs** in Prod; **100%** passing automated tests before merge. |
| **Quality** | **Thrashing** | **0 Feature/ProdSupport** tickets reopened; **100%** passing resgression tests before deploy. |
| **Security** | **Vulnerabilities** | **0%** of deployments have no high risk vulnerabilities.  Medium and low risk vulnerabilities are mitigated or documented before next regression.  |
| **Team** | **Skill Adoption** | **100%** of IAM engineers completed [intro to MLOps workshop](https://www.databricks.com/resources/ebook/machine-learning-engineering-in-action). |
| **Team** | **GitHub CoPilot** | **30%** reduction in coding time via Copilot. |
| **Velocity** | **Deployment Frequency** | Increase to **Weekly** or Ad-Hoc releases for ML/IAM components (High Velocity). |