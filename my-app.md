# Vibe-Trading

Vibe-Trading is an open-source, agent-based research and trading workspace designed to transform high-level finance questions into executable research, simulation, and automated trading workflows. It operates as a modular, self-improving agent system that bridges the gap between natural-language reasoning and rigorous quantitative analysis.

## Core Purpose

Vibe-Trading aims to democratize access to institutional-grade trading research and automation. It allows users to:
*   **Research:** Perform natural-language market analysis using agents, web search, and data tools.
*   **Simulate:** Build, test, and backtest sophisticated trading strategies across various asset classes.
*   **Audit:** Compare live trading performance against extracted rule-based strategies using a Shadow Account system.
*   **Automate:** When authorized, automate trading through bounded, mandate-gated broker connectors.

## How It Works

The architecture is built around a modular agent-based design, separating the intelligence layer from the execution and data layers.

### 1. Backend: The Trading Agent
The core is a Python-based backend that manages the agent's "thought" process, tool orchestration, and memory.
*   **Orchestration:** Uses a ReAct agent loop for multi-turn reasoning, tool calls, and evidence collection.
*   **Swarm Architecture:** Supports complex, collaborative agent teams (e.g., investment, quant, crypto, risk teams) for multi-faceted analysis.
*   **Memory:** Implements persistent cross-session memory and FTS5 session search for context-aware research.
*   **Governance:** Tracks methodology and versioning through a hash-manifest and a hash-chained audit ledger, ensuring transparency in how research or trading decisions were reached.

### 2. Frontend: Dashboard & Interface
A web-based dashboard, built with React, Vite, and Tailwind, provides a visually rich environment for:
*   Interactive agent chats.
*   Real-time monitoring of agent swarms.
*   Visualizing backtest results, tearsheets, and correlation matrices.
*   Managing configurations and connector credentials.

### 3. Data & Backtesting Engine
The backtesting engine is designed for rigor, supporting:
*   **Cross-Market Capabilities:** A composite backtest engine allows for portfolio management across diverse asset classes (equities, crypto, futures, forex) with unified capital handling.
*   **Intelligent Loaders:** A source-agnostic data-loader registry supports 20+ sources with automatic, IP-ban-resilient fallback chains.
*   **Factored Research:** Includes a library of 400+ pre-built quantitative factors (Alpha Zoo) for fast strategy testing and benchmarking.
*   **Risk & Validation:** Built-in tools for Monte Carlo simulation, Bootstrap CI, and Walk-Forward validation to guard against overfitting.

### 4. Operational Workflow
1.  **Research Goal:** The user defines a goal. The agent breaks this down into sub-tasks (evidence gathering, strategy discovery, backtesting).
2.  **Tool Orchestration:** The agent utilizes the tool registry to fetch data, perform quantitative math (via `quantlib`), or generate and validate strategy code.
3.  **Shadow & Audit:** Trading records can be ingested to analyze behavioral biases and extract explicit trading rules, which are then audited against counterfactual shadow-backtests.
4.  **Live Mandate (Optional):** If configured, the agent acts within a strict, user-defined mandate (symbols, size/exposure limits, daily caps) for live trading, with human oversight via audit ledgers and immediate kill switches.

---
*For more information, see the official [Wiki](https://vibetrading.wiki/) and [Documentation](https://vibetrading.wiki/docs/).*
