SupplyChainCopilot

Building an Intelligent Supply Chain Assistant with Fine-Tuning, Reinforcement Learning, and MLOps

Introduction

Supply chains are critical yet fragile components of modern economies. Despite digitalization, they still suffer from shipment delays, cost overruns, vendor unreliability, and compliance risks.

The explosion of supply chain data—purchase orders, invoices, shipment logs, vendor reports—creates an opportunity to apply AI-driven anomaly detection and explanation. However, generic LLMs are too costly, slow, and domain-agnostic.

SupplyChainCopilot is an intelligent supply chain assistant built with:

Small Language Models (SLMs) fine-tuned on domain datasets

Reinforcement Learning from Human Feedback (RLHF) for alignment

MLOps pipelines for scalable deployment and continuous improvement

This project demonstrates how AI can move beyond passive analytics to become an agentic assistant: reasoning, explaining, and collaborating with humans and other AI agents.

Why Small Language Models?

Instead of deploying massive LLMs, this project uses SLMs (~1B–7B parameters) because they:

Lower inference cost and latency

Are easier to fine-tune with domain data (via QLoRA/LoRA)

Are simpler to govern, monitor, and deploy in enterprise settings

Naturally fit multi-agent architectures (specialized, cooperative models)

This approach is influenced by Small Language Models are the Future of Agentic AI (Belcák et al., 2025).

Problem Definition

Supply chains face anomalies such as:

Delayed shipments

Unexpected logistics cost overruns

Vendor SLA breaches

Incomplete or inconsistent records

But detecting anomalies is not enough—explainability is essential:

“The shipment was delayed due to customs clearance hold and carrier breakdown.”

“Vendor X breached SLA 12% more than peers.”

Dataset and Preparation

Dataset: DataCo Smart Supply Chain

Pipeline:

Data Cleaning – normalize dates, currencies, remove duplicates

Anonymization – pseudonymize vendor identifiers

Feature Engineering – e.g.,

lead_time_days = delivery_date - ship_date

delay_flag = lead_time_days > expected_lead_time

cost_overrun = actual_cost - expected_cost

SFT Dataset – instruction–response JSONL

RLHF Data – preference pairs for DPO/PPO

Model Development

Supervised Fine-Tuning (SFT)

Base: Mistral-7B or Llama-2-7B

Method: QLoRA

Tasks: extraction, summarization, anomaly classification

Reinforcement Learning Alignment (RLHF)

DPO – direct preference optimization (no reward model needed)

PPO – policy optimization via trained reward model

Goal: responses that are accurate and business-friendly

Multi-Agent Integration

Agent-to-Agent (A2A) protocol for agent communication

Model Context Protocol (MCP) for structured interoperability with ERP/BI tools

Evaluation

Model Metrics: Precision, Recall, F1, Accuracy, Preference win-rate

Business Metrics: SLA compliance, anomaly triage time, vendor insights

Analytic Metrics: Delay distributions, cost overrun patterns

Deployment with MLOps

Data ingestion: Kaggle prototype, later ERP exports

Preprocessing and feature engineering: automated pipelines (AWS Glue/SageMaker)

Training: HuggingFace + TRL (SFT + DPO/PPO loops)

Deployment: HuggingFace → Amazon Bedrock (Custom Model Import)

Monitoring: latency, drift, preference win-rates

Retraining loop: triggered on drift or domain shift

Goals vs Non-Goals

Goals:

Fine-tune domain SLMs for structured and natural language tasks

Align with RLHF (DPO/PPO)

Deploy via scalable MLOps

Enable interoperability (A2A, MCP)

Non-Goals:

Real-time route optimization

Full ERP/TMS integration

Multimodal inputs (e.g., invoices as images)

Perfect accuracy (focus is on explainability and alignment)

References

Belcák et al., 2025 – Small Language Models are the Future of Agentic AI

Anthropic – Model Context Protocol

Agent2Agent Project (GitHub)

DataCo Smart Supply Chain (Kaggle)

Conclusion

SupplyChainCopilot is a blueprint for building trustworthy, cost-effective, and explainable AI assistants for supply chain operations. By blending fine-tuned SLMs, RLHF, and enterprise-grade MLOps, it demonstrates how AI can move from raw anomaly detection to actionable, human-aligned recommendations—a practical step toward agentic AI in enterprise supply chains.
