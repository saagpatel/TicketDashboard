# TicketDash

[![TypeScript](https://img.shields.io/badge/TypeScript-3178c6?style=flat-square&logo=typescript)](#) [![Rust](https://img.shields.io/badge/Rust-dea584?style=flat-square&logo=rust)](#) [![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](#)

> Your assigned Jira tickets in a native app — instant search, real SLA metrics, and background sync without the browser tab.

TicketDash is a native desktop dashboard for Jira built with Tauri, React, and TypeScript. It pulls your assigned tickets locally, calculates business-hours resolution metrics, visualizes trends with interactive charts, and keeps data fresh in the background — so you have immediate insight into your workload without opening the Jira web app.

## Features

- **Local-first sync** — tickets stored locally for instant search and filtering, even offline
- **Business-hours SLA metrics** — resolution times calculated against a 9–5 working day schedule, not wall-clock hours
- **Visual dashboards** — ticket distribution by status, priority, and category; creation vs. resolution trends over time
- **Background sync** — configurable auto-refresh keeps your data current without manual refreshes
- **Auto-categorization** — define rules to group tickets into meaningful categories
- **Resolution time breakdown** — average and median resolution by priority level
- **Quick search** — find tickets by key, summary, or description instantly
- **Focused view** — only your assigned tickets; no project backlog noise

## Quick Start

### Prerequisites

- Node.js 18+
- Rust stable toolchain (`rustup`)
- Tauri system dependencies: [tauri.app/start/prerequisites](https://tauri.app/start/prerequisites/)
- Jira API token

### Installation

```bash
git clone https://github.com/saagpatel/TicketDashboard
cd TicketDashboard
npm install
```

### Usage

```bash
# Start in development mode
npm run tauri dev
```

Configure your Jira URL and API token in **Settings** on first launch.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Desktop shell | Tauri 2 |
| Frontend | React, TypeScript, Tailwind CSS |
| Charts | Recharts |
| Backend | Rust — Jira sync, business-hours calculation, categorization |
| Storage | SQLite (local app data dir) |

## Architecture

Jira data is pulled via the REST API from the Rust backend and stored locally in SQLite. Business-hours metric calculations happen in Rust where they can be tested deterministically. The frontend reads from the local cache exclusively — network calls only happen during sync, not during navigation or search. Sync runs on a configurable background timer using Tauri's task system.

## License

MIT
