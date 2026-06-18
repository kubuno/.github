<div align="center">

# ☁️ Kubuno

**A safe home for all your data — your cloud, your rules.**

Self-hosted, libre (AGPLv3) cloud platform with a modular architecture — a sovereign,
community-driven alternative to **Google Workspace** and **Microsoft 365**.

One platform, **20+ apps**: office suite, drive, mail, calendar, chat, a creative suite,
a no-code app builder, automation, an AI assistant… all running on **your** server.

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://github.com/kubuno/core/blob/main/LICENSE)
![Rust](https://img.shields.io/badge/Rust-edition_2021-orange.svg)
![React](https://img.shields.io/badge/React-19-61dafb.svg)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791.svg)
![Apps](https://img.shields.io/badge/apps-20%2B-4D38DB.svg)
![Self-hosted](https://img.shields.io/badge/self--hosted-100%25-1e8e3e.svg)

</div>

---

## 🤔 What is Kubuno?

Kubuno is a **complete cloud platform you run yourself**. Instead of renting your email,
documents, photos and files from a Big Tech vendor, you host them — on a home server, a
VPS, or a company rack — and keep full ownership and control.

It is built as a small **core** (the platform's "operating system") plus a constellation of
**independent apps**. The core handles auth, storage, real-time events and proxying; each app
is its **own process** and its **own repository**, so you install only what you need and the
platform grows without ever becoming a monolith.

## ✨ Why you'll like it

- 🧩 **Truly modular** — every app (drive, calendar, mail, office…) is an **independent process** that registers with the core at startup. Add or remove apps freely; nothing is hard-wired.
- 🏠 **Your data, your rules** — 100% self-hosted, no third-party service required, no telemetry.
- 🔐 **Secure by default** — JWT + HttpOnly refresh tokens, Argon2id password hashing, AES-256-GCM, anti-DDoS hardening, and a **seccomp sandbox** that forbids process execution inside modules.
- ⚡ **Fast & lean** — Rust + Axum + PostgreSQL backend. PostgreSQL pulls triple duty: database, **event bus** (`LISTEN/NOTIFY`) and **job queue** (`SKIP LOCKED`) — no Redis, no extra broker.
- 🖥️ **Runtime-loaded frontend** — a single React 19 host loads every app **at runtime** via ESM import maps and shared singletons (`@kubuno/sdk`, `@kubuno/ui`), so apps share one consistent shell.
- 📦 **Distributed as `.deb`** — each app ships a Debian package; install what you want with `apt`.
- 📱 **Offline-first clients** — a Rust sync engine and a cross-platform desktop app keep your files available everywhere.
- 🌍 **Truly international** — 13 languages out of the box, RTL included.

## 🧭 The apps

Twenty apps and counting — grouped by what they're for:

### 📁 Productivity & office
| App | Repo | What it does |
|---|---|---|
| 📝 **Office** | [office](https://github.com/kubuno/office) | Full suite — **8 editors**: Documents, Spreadsheets, Presentations, Diagrams, Data (BI), Maths (LaTeX), Script, Whiteboard |
| 🗄️ **Drive** | [drive](https://github.com/kubuno/drive) | File storage, sharing, search, remote mounts |
| 📅 **Calendar** | [calendar](https://github.com/kubuno/calendar) | Calendars, events, CalDAV |
| ✅ **Tasks** | [tasks](https://github.com/kubuno/tasks) | Tasks & Kanban boards (CalDAV VTODO) |
| 🗒️ **Notes** | [notes](https://github.com/kubuno/notes) | Rich notes |
| 👥 **Contacts** | [contacts](https://github.com/kubuno/contacts) | Address book (CardDAV) |
| 📋 **Forms** | [forms](https://github.com/kubuno/forms) | Forms & surveys |

### 💬 Communication
| App | Repo | What it does |
|---|---|---|
| ✉️ **Mail** | [mail](https://github.com/kubuno/mail) | Email client (IMAP/SMTP), Bayesian spam filter |
| 💬 **Chat** | [chat](https://github.com/kubuno/chat) | Messaging, voice/video calls & meetings |
| 🗣️ **Forum** | [forum](https://github.com/kubuno/forum) | Discussion boards (categories, topics, moderation) |

### 🎨 Creative & media
| App | Repo | What it does |
|---|---|---|
| 🎨 **PaintSharp** | [paintsharp](https://github.com/kubuno/paintsharp) | Creative suite — **6 editors**: Layer (raster), Apex (vector), Vertex (3D), Motion (video), Keyframe (2D animation), PdfWriter |
| 🖼️ **Photos** | [photos](https://github.com/kubuno/photos) | Photo gallery |
| 🎵 **Media** | [media](https://github.com/kubuno/media) | Media library |

### 🛠️ Build & automate
| App | Repo | What it does |
|---|---|---|
| 📚 **Wiki** | [wiki](https://github.com/kubuno/wiki) | Collaborative wiki, MediaWiki-inspired (wikitext, templates, categories) |
| 🧱 **App** | [app](https://github.com/kubuno/app) | Visual **no-code** app builder (Bubble-style) |
| 🔀 **Flow** | [flow](https://github.com/kubuno/flow) | Workflow automation (n8n / Make-style) |
| 💻 **Code** | [code](https://github.com/kubuno/code) | Code editor |

### 🔧 Utilities & AI
| App | Repo | What it does |
|---|---|---|
| 🔑 **KeeStore** | [keestore](https://github.com/kubuno/keestore) | Password manager (KDBX) |
| 🗺️ **Maps** | [maps](https://github.com/kubuno/maps) | Maps |
| 🤖 **Jarvis** | [jarvis](https://github.com/kubuno/jarvis) | AI assistant |

## 🏗️ Architecture

```
Frontend host (React 19) ── import map ──► apps loaded at runtime (/modules/<id>/entry.js)
        │
Core (Rust / Axum)  ── reverse proxy + events + auth + storage ──►  apps (separate processes)
        │
PostgreSQL 16 (schema per app · LISTEN/NOTIFY · jobs)
```

The **[core](https://github.com/kubuno/core)** is the platform's operating system. Each app lives in
its **own repository** and ships its own Debian package, depending on Kubuno's shared Rust crates
(tagged git deps) and frontend libraries (`@kubuno/*` on npm). Apps never link the core directly —
they talk to it over HTTP and well-defined extension points, so they stay genuinely independent.

## 🖥️ Native & offline

- **[desktop](https://github.com/kubuno/desktop)** — a Nextcloud-style **file sync engine** (`kubuno-sync`, Rust): bidirectional pull + push, offline outbox, conflict handling, real-time `watch` mode — usable as a library, a CLI daemon, or wrapped in a **cross-platform desktop app** (Tauri).
- **[api-spec](https://github.com/kubuno/api-spec)** — generated OpenAPI clients (Swift, Kotlin) for building native mobile apps.

## 🚀 Get Kubuno

Start with the **[core](https://github.com/kubuno/core)**, then add the apps you want — each ships a `.deb` package.

**Requirements:** Rust ≥ 1.82, Node.js ≥ 24, PostgreSQL 16.

```bash
git clone https://github.com/kubuno/core && cd core
cargo build --release && (cd frontend && npm ci && npm run build)
bash build_deb.sh --install        # build & install the .deb locally
```

Prefer prebuilt packages? Every repository publishes **`.deb` artifacts** on its
[GitHub Releases](https://github.com/kubuno/core/releases) page (built automatically by CI on each tagged version).

## 🤝 Get involved

Contributions are welcome — **code, translations, design, testing, docs**. Open an issue on the
relevant repository to discuss any significant change before submitting a pull request. New to the
project? The [core](https://github.com/kubuno/core) is the best place to start reading.

## 📄 License

Everything is [AGPL-3.0-or-later](https://github.com/kubuno/core/blob/main/LICENSE) © Kubuno contributors.
