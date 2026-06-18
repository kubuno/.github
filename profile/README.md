<div align="center">

# ☁️ Kubuno

**A safe home for all your data — your cloud, your rules.**

Self-hosted, libre (AGPLv3) cloud platform with a modular architecture — a sovereign,
community-driven alternative to Google Workspace and Microsoft 365.

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://github.com/kubuno/core/blob/main/LICENSE)
![Rust](https://img.shields.io/badge/Rust-edition_2021-orange.svg)
![React](https://img.shields.io/badge/React-19-61dafb.svg)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791.svg)

</div>

---

## ✨ Why is this awesome?

- 🧩 **Truly modular** — every app (drive, calendar, mail, office…) is an **independent process** that connects to the core at startup. Install only what you need.
- 🏠 **Your data, your rules** — fully self-hosted, no third-party service required.
- 🔐 **Secure by default** — JWT + HttpOnly refresh tokens, Argon2id, AES-256-GCM, anti-DDoS hardening, and a seccomp sandbox for modules.
- ⚡ **Fast & lean** — Rust + Axum + PostgreSQL backend; PostgreSQL doubles as the event bus (`LISTEN/NOTIFY`) and job queue (`SKIP LOCKED`).
- 🖥️ **Runtime-loaded frontend** — a React 19 host loads modules **at runtime** via ESM import maps and shared singletons (`@kubuno/sdk`, `@ui`).
- 🌍 **i18n** — 13 languages, RTL included.

## 🏗️ Architecture

```
Frontend host (React 19) ── import map ──► modules loaded at runtime (/modules/<id>/entry.js)
        │
Core (Rust / Axum)  ── reverse proxy + events + auth + storage ──►  modules (separate processes)
        │
PostgreSQL 16 (schema per module · LISTEN/NOTIFY · jobs)
```

The **[core](https://github.com/kubuno/core)** is the platform's operating system. Each app lives in its **own repository** and ships its own Debian package, depending on Kubuno's shared Rust crates (tagged git deps) and frontend libraries (`@kubuno/*` on npm).

## 📦 The apps

| App | Repo | What it does |
|---|---|---|
| 🗄️ **Drive** | [kubuno/drive](https://github.com/kubuno/drive) | File storage, sharing, remote mounts |
| 📅 **Calendar** | [kubuno/calendar](https://github.com/kubuno/calendar) | Calendars, events, CalDAV |
| ✉️ **Mail** | [kubuno/mail](https://github.com/kubuno/mail) | Email client (IMAP/SMTP) |
| 🖼️ **Photos** | [kubuno/photos](https://github.com/kubuno/photos) | Photo gallery |
| 📝 **Office** | [kubuno/office](https://github.com/kubuno/office) | Documents, spreadsheets, slides, diagrams… |
| 🎨 **PaintSharp** | [kubuno/paintsharp](https://github.com/kubuno/paintsharp) | Creative suite (raster, vector, 3D, video) |
| 💬 **Chat** | [kubuno/chat](https://github.com/kubuno/chat) | Messaging |
| 👥 **Contacts** | [kubuno/contacts](https://github.com/kubuno/contacts) | Address book (CardDAV) |
| 🗣️ **Forum** | [kubuno/forum](https://github.com/kubuno/forum) | Discussion boards (categories, forums, topics, posts) |
| ✅ **Tasks** | [kubuno/tasks](https://github.com/kubuno/tasks) | Tasks & Kanban boards |
| 🗒️ **Notes** | [kubuno/notes](https://github.com/kubuno/notes) | Notes |
| 🗺️ **Maps** | [kubuno/maps](https://github.com/kubuno/maps) | Maps |
| 🎵 **Media** | [kubuno/media](https://github.com/kubuno/media) | Media library |
| 📋 **Forms** | [kubuno/forms](https://github.com/kubuno/forms) | Forms & surveys |
| 🔀 **Flow** | [kubuno/flow](https://github.com/kubuno/flow) | Workflow automation (n8n/Make-style) |
| 💻 **Code** | [kubuno/code](https://github.com/kubuno/code) | Code editor |
| 🔑 **KeeStore** | [kubuno/keestore](https://github.com/kubuno/keestore) | Password manager (KDBX) |
| 🤖 **Jarvis** | [kubuno/jarvis](https://github.com/kubuno/jarvis) | AI assistant |

## 🚀 Get Kubuno

Start with the **[core](https://github.com/kubuno/core)** (requirements: Rust ≥ 1.82, Node.js ≥ 24, PostgreSQL 16), then add the apps you want — each ships a `.deb` package.

```bash
git clone https://github.com/kubuno/core && cd core
cargo build --release && (cd frontend && npm ci && npm run build)
bash build_deb.sh
```

## 🤝 Get involved

Contributions are welcome — code, translations, design, testing, docs. Open an issue on the relevant repository to discuss any significant change before submitting a pull request.

## 📄 License

Everything is [AGPL-3.0-or-later](https://github.com/kubuno/core/blob/main/LICENSE) © Kubuno contributors.
