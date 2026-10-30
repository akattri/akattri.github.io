---
title: "Archon"
date: 2025-09-10
date_display: "2025"
description: "A browser extension and productivity dashboard integrating Google Calendar, local task queues, and Chrome bookmarks."
status: "prototype"
domain: "Browser Systems & Productivity"
technologies:
  - "JavaScript"
  - "Chrome Extensions API"
  - "Google Calendar API"
  - "OAuth 2.0"
  - "Web Storage"
github: "https://github.com/akattri/Archon"
demo: ""
featured: true
weight: 60
---

## Overview

**Archon** is an experimental browser extension and new-tab dashboard designed to consolidate daily developer workflow essentials: scheduled calendar commitments, ad-hoc tasks, search shortcuts, and hierarchical bookmarks into a fast, unified interface.

---

## Why I Built It

Most browser new-tab pages either present algorithmic clickbait or require third-party SaaS subscriptions that compromise user privacy.

Archon was built as a personal software experiment to explore:
- How browser extensions operate within sandboxed background service workers.
- How to authenticate securely against Google Calendar using OAuth 2.0 in an extension context.
- How to structure local-first state storage that persists without requiring a separate backend database.

---

## What I Learned & Engineering Takeaways

- **Manifest V3 Architecture**: Adapting to non-persistent background service workers, event-driven state hydration, and declarative content security policies.
- **OAuth Identity Flows**: Handling token retrieval and silent refreshes using the `chrome.identity` API and Google Cloud credential scopes.
- **Asynchronous Storage Patterns**: Navigating the asynchronous nature of `chrome.storage.local` to prevent UI state synchronization bugs when updating bookmark trees and task queues.

---

## Technical Architecture & Implementation

Archon was developed as a client-only browser extension:
- **Calendar Integration**: Fetches upcoming agenda items via Google Calendar API with scoped read access.
- **Local Task State**: Persistent client-side task queue supporting prioritization and completion states.
- **Bookmark Search**: Direct traversal of the Chrome bookmark hierarchy for quick-filter navigation.

---

## Future Directions & Open Questions

- **Offline Sync**: Implementing Conflict-Free Replicated Data Types (CRDTs) or operational transforms for multi-device synchronization without centralized lock-in.

