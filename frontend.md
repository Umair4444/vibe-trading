# Vibe-Trading Frontend: Master Frontend Blueprint

**INSTRUCTIONS TO AGENT:** This is the definitive, unified specification for reconstructing the Vibe-Trading frontend. It merges design standards with implementation requirements. Follow this document in its entirety to reconstruct the frontend.

## 1. Design System (Aesthetics)
- **Themeing:** Based on CSS variables in `:root` (light) and `.dark` (dark mode) defined in `index.css`.
    - **Surface System:** Maintain a 5-point lightness difference between dark surfaces.
    - **Variables:** Background (`--background`), Card (`--card`), Popover (`--popover`), Muted (`--muted`), Border (`--border`).
- **Colors:** Primary (`--primary`), Semantic (`--success`, `--danger`, `--warning`, `--info`), and Chart tokens.
- **Typography:**
    - **Sans:** `Inter`, `system-ui`, `sans-serif` (UI, inputs, tables).
    - **Mono:** `JetBrains Mono`, `ui-monospace`, `monospace` (code, logs, data).
    - **Serif:** `Georgia`, `serif` (**Restricted to Hero Greeting only**).
- **Spacing/Radius:** Tailwind defaults. Border Radius: `lg` (0.5rem), `md` (calc(var(--radius) - 2px)), `sm` (calc(var(--radius) - 4px)).

## 2. Project Scaffolding
- **Stack:** React 19 (TS), Vite, Tailwind, Zustand, ECharts, React-Markdown.
- **Global Config:** Enforce `overflow-anchor: none` on chat containers and custom webkit scrollbar styling in `index.css`.

## 3. Component & Page Catalog

### Pages (Lazy-loaded via `router.tsx`)
| Route | Page Component | Functional Purpose |
| :--- | :--- | :--- |
| `/` or `/agent` | `Agent.tsx` | Core chat interface, swarm interaction. |
| `/runtime` | `Runtime.tsx` | Live agent runtime status/logs. |
| `/scheduled` | `Scheduled.tsx` | Manage scheduled research tasks. |
| `/portfolio` | `Portfolio.tsx` | Portfolio overview/asset management. |
| `/runs/:runId` | `RunDetail.tsx` | Backtest run deep dive. |
| `/compare` | `Compare.tsx` | Strategy/run comparison. |
| `/correlation` | `Correlation.tsx` | Correlation matrix. |
| `/options` | `OptionsLab.tsx` | Options strategy modeling. |
| `/alpha-zoo` | `AlphaZoo.tsx` | Factor research library. |
| `/reports` | `Reports.tsx` | Generated reports. |
| `/settings` | `Settings.tsx` | Configuration. |
| `/about` | `Home.tsx` | Project information. |

### Component Hierarchy (`src/components/`)
- **`layout/`**: `Layout.tsx` (Sidebar + Outlet), `ThemeToggle.tsx`.
- **`chat/`**: `ChatContainer.tsx` (Streaming logic), `MessageList.tsx` (Markdown), `InputArea.tsx`.
- **`charts/`**: `EChartsWrapper.tsx` (Theming logic), `TimeSeriesChart.tsx`.
- **`run/`**: `RunSummary.tsx`, `RunLogs.tsx`.
- **`portfolio/`**: `AssetTable.tsx`, `PerformanceMetrics.tsx`.
- **`settings/`**: `ApiConfigForm.tsx`, `PreferenceToggle.tsx`.

## 4. State & API Patterns
- **State (Zustand):**
    - `useAgentStore`: `{ status: 'idle'|'running'|'error'; task: string|null; setStatus: (s) => void; }`
    - `useChatStore`: `{ messages: Message[]; addMessage: (m) => void; streaming: boolean; setStreaming: (b) => void; }`
- **API (`src/hooks/`):**
    - `useFetch`: Wrapper for `fetch` with `VITE_API_URL` and auth.
    - `useSSE`: Connects to `/v1/events`, receives JSON chunks, updates `useChatStore`.

## 5. Functional Implementation Requirements (Strict)
1.  **Markdown:** `react-markdown` + `rehype-highlight` (code), `rehype-katex` (math), `remark-gfm` (tables). **Prose table styling required**: `.prose tbody tr:nth-child(even)` background + border-collapse.
2.  **Streaming:** `ChatContainer` MUST use `overflow-anchor: none`.
3.  **Charts:** ECharts must be theme-aware; update dynamically when `document.body` toggles `dark` class.
4.  **Routing:** All pages MUST be lazily loaded via `Suspense` with a `<PageLoader />` fallback.

## 6. Development Workflow
1.  **Scaffold:** Vite/TS/Tailwind setup.
2.  **Tokens:** Apply HSL variables from `index.css` to `tailwind.config.ts`.
3.  **Core:** Stores -> Hooks -> Layout.
4.  **Pages/Components:** Reconstruct each page/component using the catalog above.
