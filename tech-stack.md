# Tech Stack

Vibe-Trading is built on a modular, containerized architecture that separates the intelligence-driven backend (agentic reasoning and finance operations) from a high-performance, interactive frontend dashboard.

## 1. Backend: Python Agent System
The backend powers the research, strategy simulation, and trading execution logic.

| Category | Technology/Package | Purpose |
| :--- | :--- | :--- |
| **Orchestration** | `langchain`, `langgraph` | Handles ReAct agent loops, multi-turn reasoning, and memory-managed workflows. |
| **API & Server** | `fastapi`, `uvicorn` | Provides the REST/SSE API for frontend communication. |
| **Data Analysis** | `pandas`, `numpy`, `scipy` | Core quantitative processing and financial data manipulation. |
| **Database/Storage** | `duckdb` | High-performance analytical database for research data. |
| **Web Search** | `duckduckgo-search` (`ddgs`) | Enables live market research. |
| **Finance Sources** | `yfinance`, `akshare`, `ccxt` | Connectors for various financial markets and assets. |
| **Utilities** | `rich`, `jinja2`, `weasyprint` | Terminal output, reporting, and automated report generation. |
| **MCP** | `fastmcp` | Implements Model Context Protocol for agent tool integration. |

## 2. Frontend: React Dashboard
The frontend provides a real-time, visual interface to interact with the Vibe-Trading agents.

| Technology | Purpose |
| :--- | :--- |
| **Framework** | **React 19** with **Vite** for fast development and build. |
| **Language** | **TypeScript** for type-safe code. |
| **Styling** | **Tailwind CSS** for responsive, modern UI design. |
| **State Management** | **Zustand** for lightweight global state. |
| **Visualization** | **ECharts** for rich financial charts. |
| **UI Components** | **Lucide React** (icons), **Sonner** (notifications). |
| **Markdown/Rendering** | **React-Markdown** with **Remark/Rehype** plugins (LaTeX support via KaTeX). |

## 3. Infrastructure
The application is fully containerized to ensure consistent environment setups.

*   **Docker & Docker Compose:** Used to manage the backend, frontend, and persistent data volumes (e.g., sessions, agent runs, user state).
*   **Persistent Volumes:** Named Docker volumes are used for critical state, ensuring that session history, agent configuration, and memory indexes persist across container recreation.
*   **Hardening:** Security measures include non-root execution (`no-new-privileges`) and constrained resource limits (`mem_limit`, `cpus`).

## Integration Flow

1.  **Orchestration:** The **FastAPI** backend exposes endpoints for the **React** frontend.
2.  **Communication:** Real-time data is streamed between the backend agent (orchestrated by **LangGraph**) and the frontend UI.
3.  **Data Processing:** When a research goal is initiated, the backend agent (via **LangChain**) dynamically selects tools, retrieves data (using **DuckDB** + loaders), performs analysis (**Pandas**), and updates the UI.
4.  **Persistence:** Agent states, session memory, and configurations are persisted across sessions using structured storage in Docker volumes, ensuring continuity for multi-turn research tasks.
