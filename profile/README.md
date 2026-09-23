<div align="center">

<img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/kubuno.svg" width="120" height="120" alt="Kubuno logo">

# Kubuno

**A safe home for all your data — your cloud, your rules.**

Self-hosted, libre (AGPLv3) cloud platform with a modular architecture — a sovereign,
community-driven alternative to **Google Workspace** and **Microsoft 365**.

One platform, **20+ apps**: an office suite, files, mail, calendar, chat and meetings, a creative
suite, a no-code app builder, automation, an AI assistant… all running on **your** server.

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://github.com/kubuno/core/blob/main/LICENSE)
![Rust](https://img.shields.io/badge/Rust-edition_2021-orange.svg)
![React](https://img.shields.io/badge/React-19-61dafb.svg)
![Database](https://img.shields.io/badge/database-PostgreSQL_|_MySQL_|_SQLite-336791.svg)
![Apps](https://img.shields.io/badge/apps-20%2B-4D38DB.svg)
![Self-hosted](https://img.shields.io/badge/self--hosted-100%25-1e8e3e.svg)

</div>

---

## What is Kubuno?

Kubuno is a **complete cloud platform you run yourself**. Instead of renting your email,
documents, photos and files from a Big Tech vendor, you host them — on a home server, a VPS or a
company rack — and keep full ownership and control.

It is built as a small **core** (the platform's "operating system") plus a constellation of
**independent apps**. The core handles accounts, authentication, storage, real-time events,
administration and proxying; each app is its **own process** and its **own repository**, so you
install only what you need and the platform grows without ever becoming a monolith.

## Why you'll like it

- **Truly modular** — every app is an independent process that registers with the core at startup. Install, update or remove apps from the administration console; nothing is hard-wired.
- **Your data, your rules** — 100% self-hosted, no third-party service required, no telemetry.
- **Administered like an organisation** — organisational units with inherited, lockable settings, groups, delegated admin roles, audit log, security dashboard, alerts, rules and printable reports.
- **Secure by default** — Argon2id password hashing, short-lived JWTs with HttpOnly refresh cookies, AES-256-GCM for data at rest, a tamper-evident audit chain, account lockout and anti-DDoS hardening, and a **seccomp sandbox** that forbids process execution inside apps.
- **Fast & lean** — a Rust + Axum backend on the database you choose: **PostgreSQL, MySQL/MariaDB or SQLite** (a couple of apps still require PostgreSQL). The database also carries the **event bus** and the **job queue** — no Redis, no extra broker.
- **One consistent interface** — a single React 19 host loads every app **at runtime** through an import map and shared libraries (`@kubuno/sdk`, `@kubuno/ui`), so all apps share one shell, one design system and one theme.
- **Runs anywhere** — native packages for the core on Linux, Windows and macOS, a one-command **Docker image**, and self-contained **`.kbpkg`** app packages installed identically on every platform.
- **Truly international** — 13 languages out of the box, right-to-left included.

## The core

Everything starts with the **core** — the platform's "operating system", and the only piece every
installation needs. It is the server your users sign in to and the web interface they use; the
apps plug into it.

<table>
  <thead>
    <tr>
      <th width="52"></th>
      <th align="left">Repository</th>
      <th align="left">What it does</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/kubuno.svg" width="24" height="24" alt=""></td>
      <td><b><a href="https://github.com/kubuno/core">core</a></b></td>
      <td>Accounts and sign-in (passwords, SSO/OIDC, LDAP), organisational units, groups and roles, storage and quotas, real-time events, the administration console, app installation and updates, and the web interface that hosts every app</td>
    </tr>
  </tbody>
</table>

The core also publishes the libraries the apps are built on: the shared Rust crates (database,
storage, sandbox, module authentication) and the `@kubuno/ui`, `@kubuno/sdk` and `@kubuno/drive`
packages on npm.

## The apps

### Productivity & office

<table>
  <thead>
    <tr>
      <th width="52"></th>
      <th align="left">App</th>
      <th align="left">Repository</th>
      <th align="left">What it does</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/office.svg" width="24" height="24" alt=""></td>
      <td><b>Office</b></td>
      <td><a href="https://github.com/kubuno/office">office</a></td>
      <td>Full suite — Documents, Spreadsheets, Presentations, Projects, Diagrams, Data, Maths, Script and Whiteboard, with real-time co-editing</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/drive.png" width="24" height="24" alt=""></td>
      <td><b>Drive</b></td>
      <td><a href="https://github.com/kubuno/drive">drive</a></td>
      <td>Files — upload, sharing, search, versions, previews and remote mounts</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/calendar.png" width="24" height="24" alt=""></td>
      <td><b>Calendar</b></td>
      <td><a href="https://github.com/kubuno/calendar">calendar</a></td>
      <td>Calendars, invitations, meeting rooms, booking pages and CalDAV</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/tasks.png" width="24" height="24" alt=""></td>
      <td><b>Tasks</b></td>
      <td><a href="https://github.com/kubuno/tasks">tasks</a></td>
      <td>Task lists, sub-tasks and Kanban boards (CalDAV VTODO)</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/notes.png" width="24" height="24" alt=""></td>
      <td><b>Notes</b></td>
      <td><a href="https://github.com/kubuno/notes">notes</a></td>
      <td>Markdown notes, checklists, notebooks and backlinks</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/contacts.png" width="24" height="24" alt=""></td>
      <td><b>Contacts</b></td>
      <td><a href="https://github.com/kubuno/contacts">contacts</a></td>
      <td>Address book, groups and the organisation directory (CardDAV)</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/forms.png" width="24" height="24" alt=""></td>
      <td><b>Forms</b></td>
      <td><a href="https://github.com/kubuno/forms">forms</a></td>
      <td>Forms and surveys, with response analysis</td>
    </tr>
  </tbody>
</table>

### Communication

<table>
  <thead>
    <tr>
      <th width="52"></th>
      <th align="left">App</th>
      <th align="left">Repository</th>
      <th align="left">What it does</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/mail.png" width="24" height="24" alt=""></td>
      <td><b>Mail</b></td>
      <td><a href="https://github.com/kubuno/mail">mail</a></td>
      <td>Multi-account mail client (IMAP/SMTP) with labels, filters and spam filtering</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/chat.png" width="24" height="24" alt=""></td>
      <td><b>Chat</b></td>
      <td><a href="https://github.com/kubuno/chat">chat</a></td>
      <td>Messaging, voice and video calls, and meetings</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/forum.png" width="24" height="24" alt=""></td>
      <td><b>Forum</b></td>
      <td><a href="https://github.com/kubuno/forum">forum</a></td>
      <td>Discussion boards with categories, topics, ranks and moderation</td>
    </tr>
  </tbody>
</table>

### Creative & media

<table>
  <thead>
    <tr>
      <th width="52"></th>
      <th align="left">App</th>
      <th align="left">Repository</th>
      <th align="left">What it does</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/paintsharp.png" width="24" height="24" alt=""></td>
      <td><b>PaintSharp</b></td>
      <td><a href="https://github.com/kubuno/paintsharp">paintsharp</a></td>
      <td>Creative suite — raster, vector, video, animation, PDF and font editors</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/photos.png" width="24" height="24" alt=""></td>
      <td><b>Photos</b></td>
      <td><a href="https://github.com/kubuno/photos">photos</a></td>
      <td>Photo library — albums, timeline and sharing</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/media.png" width="24" height="24" alt=""></td>
      <td><b>Media</b></td>
      <td><a href="https://github.com/kubuno/media">media</a></td>
      <td>Streaming — films and series (Watch) and music (Listen)</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/books.png" width="24" height="24" alt=""></td>
      <td><b>Books</b></td>
      <td><a href="https://github.com/kubuno/books">books</a></td>
      <td>Library of books, comics and e-books</td>
    </tr>
  </tbody>
</table>

### Build & automate

<table>
  <thead>
    <tr>
      <th width="52"></th>
      <th align="left">App</th>
      <th align="left">Repository</th>
      <th align="left">What it does</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/wiki.png" width="24" height="24" alt=""></td>
      <td><b>Wiki</b></td>
      <td><a href="https://github.com/kubuno/wiki">wiki</a></td>
      <td>Collaborative wiki — wikitext, templates, namespaces and categories</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/app.png" width="24" height="24" alt=""></td>
      <td><b>App</b></td>
      <td><a href="https://github.com/kubuno/app">app</a></td>
      <td>Visual no-code builder for complete web applications</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/flow.png" width="24" height="24" alt=""></td>
      <td><b>Flow</b></td>
      <td><a href="https://github.com/kubuno/flow">flow</a></td>
      <td>Visual workflow automation with native Kubuno connectors</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/code.png" width="24" height="24" alt=""></td>
      <td><b>Code</b></td>
      <td><a href="https://github.com/kubuno/code">code</a></td>
      <td>Collaborative web IDE with Git</td>
    </tr>
  </tbody>
</table>

### Utilities & AI

<table>
  <thead>
    <tr>
      <th width="52"></th>
      <th align="left">App</th>
      <th align="left">Repository</th>
      <th align="left">What it does</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/keestore.png" width="24" height="24" alt=""></td>
      <td><b>KeeStore</b></td>
      <td><a href="https://github.com/kubuno/keestore">keestore</a></td>
      <td>Password manager — KeePass 4 (<code>.kdbx</code>) vaults encrypted client-side</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/maps.png" width="24" height="24" alt=""></td>
      <td><b>Maps</b></td>
      <td><a href="https://github.com/kubuno/maps">maps</a></td>
      <td>Self-hosted maps — routes, saved places and tracks</td>
    </tr>
    <tr>
      <td align="center"><img src="https://raw.githubusercontent.com/kubuno/.github/main/profile/logos/assistant.png" width="24" height="24" alt=""></td>
      <td><b>Assistant</b></td>
      <td><a href="https://github.com/kubuno/assistant">assistant</a></td>
      <td>AI assistant running local models, with custom agents</td>
    </tr>
  </tbody>
</table>

### Platform services

| Repository | What it does |
|---|---|
| [stt](https://github.com/kubuno/stt) | Self-hosted speech recognition (Whisper) behind the platform's voice search |
| [p2pnas](https://github.com/kubuno/p2pnas) | Encrypted, self-healing peer-to-peer storage, mounted in Drive as "My Cloud" |

## Architecture

```
Frontend host (React 19) ── import map ──► apps loaded at runtime (/modules/<id>/entry.js)
        │
Core (Rust / Axum)  ── reverse proxy · events · auth · storage · admin ──►  apps (separate processes)
        │
Database — PostgreSQL, MySQL/MariaDB or SQLite (one namespace per app · events · job queue)
```

The **[core](https://github.com/kubuno/core)** is the platform's operating system. Each app lives in
its **own repository** and ships as a self-contained **`.kbpkg`** package that the core installs
itself. Apps depend on Kubuno's shared Rust crates (tagged git dependencies) and frontend libraries
(`@kubuno/*` on npm), never on the core directly — they talk to it over HTTP and well-defined
extension points, so they stay genuinely independent.

## Clients

- **[desktop](https://github.com/kubuno/desktop)** — a file sync engine (`kubuno-sync`, Rust) with offline outbox, conflict handling and live watch mode, usable as a library, a CLI daemon or a cross-platform desktop app.
- **[mobile](https://github.com/kubuno/mobile)** — native mobile apps: six Android apps today (Drive, Photos, Documents, Mail, Maps, Messages) sharing one set of device accounts, iOS planned.
- **[api-spec](https://github.com/kubuno/api-spec)** — the OpenAPI specification and generated clients for building native apps.

## Get Kubuno

The quickest way to a complete instance is the all-in-one **[Docker image](https://github.com/kubuno/docker)**:

```bash
docker pull ghcr.io/kubuno/kubuno:latest
```

Prefer a native install? The **[core](https://github.com/kubuno/core)** ships packages for
Debian/Ubuntu (`.deb`), Fedora/RHEL/openSUSE (`.rpm`), Windows (installer) and macOS (`.pkg`) on
its [Releases](https://github.com/kubuno/core/releases) page. Then add the apps you want from the
administration console, or install a downloaded `.kbpkg`:

```bash
sudo kubuno modules:install <app>-<version>-<os>-<arch>.kbpkg
```

**Building from source** requires Rust ≥ 1.82, Node.js ≥ 24 and a database (PostgreSQL 16, MySQL/MariaDB or SQLite) — each repository's
README explains its own build.

## Get involved

Contributions are welcome — **code, translations, design, testing, docs**. Open an issue on the
relevant repository to discuss any significant change before submitting a pull request. New to the
project? The [core](https://github.com/kubuno/core) is the best place to start reading.

## License

Everything is [AGPL-3.0-or-later](https://github.com/kubuno/core/blob/main/LICENSE) © Kubuno contributors.
