---
title: "Veto"
date: 2026-04-20
date_display: "2026"
description: "A Manifest V3 browser extension for Edge and Chromium enforcing origin embed filtering, channel rules, and video access controls."
status: "active prototype"
domain: "Browser Architecture & Access Control"
technologies:
  - "JavaScript"
  - "Manifest V3"
  - "declarativeNetRequest"
  - "WAI-ARIA"
  - "PBKDF2 Cryptography"
github: ""
demo: "https://microsoftedge.microsoft.com/addons/detail/veto-youtube-video-ac/mgenhkdhpgjfpdclndfnbaieojcikiol"
addon: "https://microsoftedge.microsoft.com/addons/detail/veto-youtube-video-ac/mgenhkdhpgjfpdclndfnbaieojcikiol"
featured: true
weight: 70
---

## Overview

**Veto** is a Manifest V3 browser extension developed for Microsoft Edge (Android & Desktop) and Chromium browsers that enforces deterministic access controls over video streaming and embedded media.

It is published and available on the **[Microsoft Edge Add-ons Store](https://microsoftedge.microsoft.com/addons/detail/veto-youtube-video-ac/mgenhkdhpgjfpdclndfnbaieojcikiol)**.

It implements exact-origin YouTube embed filtering, dual-mode channel allowlisting/blacklisting, video-level allowlists/blocklists across HTML5 media elements, time-delayed cooling-off changes, and daily temporary playback overrides.

---

## The Problem: Algorithmic Distraction & Unchecked Media Access

Modern video platforms rely on recommendation algorithms designed to maximize session duration through infinite feeds, autoplaying sidebars, and algorithmic related-video queues. Existing ad-blockers and content filters operate at the domain level: they either block all of YouTube or allow all of it, with no granular controls over specific educational channels or embedded video players on external academic websites.

Veto was engineered to provide fine-grained, policy-driven control over media playback:
- Enforcing default-deny policies on embedded players across external websites.
- Providing dual-mode allowlist and blocklist evaluation on direct YouTube channels and standalone video IDs.
- Introducing intentional friction via PBKDF2 passcode protection and mandatory cooling-off waiting periods to prevent impulsive policy circumvention.

---

## Technical Architecture & Core Mechanisms

```
[Web Page / Frame Load] ──> [interceptor.js (Main World)]
                                     │
                                     ▼
                            [content.js (Isolated World)]
                                     │
                    ┌────────────────┼────────────────┐
                    ▼                                 ▼
         [YouTube Player State]             [HTML5 Media Elements]
         - Video ID extraction              - Normalized URL / src
         - Uploader channel ID verification - Fail-closed unverified media
                    │                                 │
                    └────────────────┬────────────────┘
                                     │
                                     ▼
                      [Veto Policy Evaluation Engine]
                      - Disjunctive YouTube Decision Logic
                      - Approved HTTPS Embed Origin Rules
                      - Time-Delayed Cooling-Off Verification
                                     │
                                     ▼
                       [Permit / Overlay Block State]
```

### 1. Multi-World Content Script Interception
Veto injects scripts at `document_start`:
- **`interceptor.js` (Main World)**: Operates directly inside the target page's JavaScript execution context to inspect embedded player initialization parameters and media element hooks before playback starts.
- **`content.js` (Isolated World)**: Manages secure communication with the background service worker, inspects DOM mutations, and renders the accessible blocked-playback overlay without leaking extension state into page scripts.

### 2. Disjunctive Decision Logic on YouTube
To prevent requiring every single lecture in an approved course to be individually cataloged, Veto implements a disjunctive rule set:
- **Allowlist Mode**: Playback is permitted if the 11-character video ID is on the video allowlist **or** the verified channel ID is on the channel allowlist. If the channel uploader cannot be verified, an explicitly allowlisted video ID is still permitted to play.
- **Fail-Closed Guarantee**: Media elements whose origin or uploader cannot be verified fail closed and are blocked from execution.

### 3. Embed Origin Filtering
An approved channel or video is strictly blocked if embedded on an unauthorized external domain. Embeds require explicit HTTPS origin registration, enforcing default-deny everywhere else across the web.

### 4. Intentional Friction & Cooling-Off Architecture
To counteract impulsive browsing habits:
- Rule changes (e.g. adding a distracting channel or reducing restrictions) enter a **Mandatory Waiting Period** queue.
- Security controls use salted PBKDF2 cryptographic passcodes stored in `chrome.storage.local`.
- A **Timed Lockdown Mode** temporarily freezes all rule configurations, disabling overrides for the duration of a focused work block.

---

## Engineering Takeaways

- **Keyboard Event Passthrough**: Standard blockers often capture `keydown` events, interfering with YouTube's native 2× playback spacebar-hold or seek keys (J/K/L). Veto uses zero-interception event modeling, restoring keyboard focus directly to the HTML5 video container upon permission.
- **Declarative vs. Dynamic Rules**: Combining declarative net request rules with DOM-level media stream interception enables sub-millisecond filtering before media buffers begin buffering video chunks.
