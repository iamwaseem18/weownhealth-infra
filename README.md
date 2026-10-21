# WeOwnHealth — Buildathon Infrastructure

> Buildathon infrastructure in 48 hours.

## Problem

A team needed production infrastructure for a [Midnight Network](https://midnight.network) hackathon project — a **Health Markers Passport** using zero-knowledge proofs — with a hard submission deadline. The application existed as code; it needed a live, verified deployment.

## What I Built

Full production infrastructure deployed in under 48 hours for the Midnight Network Buildathon (Wave 1).

### Infrastructure
- **DigitalOcean droplet** (ATL1) provisioned and hardened
- **Docker Compose** stack with:
  - Node.js/Express backend (Issuer + Coordinator service)
  - Next.js 14 frontend (patient/sponsor role switcher, dark Midnight theme)
  - Caddy reverse proxy (automatic TLS, API routing)
- **DNS** configured at `trials.weown.health` with apex redirect from `weown.health`
- **Caddy routing**: `/api/*` → Express backend, static files → frontend

### Demo Flow (Verified End-to-End)
1. Patient connects wallet
2. Credential issuance
3. Consent flow
4. Zero-knowledge proof generation
5. Eligibility result displayed

## Architecture

```
weown.health (redirect)
       │
       ▼
trials.weown.health
       │
       ▼
┌──────────────────────────────┐
│  Docker Compose              │
│                              │
│  ┌──────────┐  ┌──────────┐ │
│  │ Next.js  │  │ Express  │ │
│  │ Frontend │  │ Backend  │ │
│  │ (static) │  │ (/api/*) │ │
│  └─────┬────┘  └────┬─────┘ │
│        │             │       │
│  ┌─────▼─────────────▼────┐ │
│  │        Caddy           │ │
│  │   (TLS + routing)      │ │
│  └────────────┬───────────┘ │
└───────────────┼──────────────┘
                │ :443
                ▼
```

## Outcome

Live demo verified end-to-end before the submission deadline. The project was selected for Buildathon Wave 1.

## Stack

`Docker` · `Caddy` · `Next.js 14` · `Node.js` · `Express` · `DigitalOcean` · `Zero-Knowledge Proofs` · `Midnight Network`

## Context

Built as Platform Engineer at [WeOwn](https://weown.net) for the Midnight Network Buildathon (2026). Application source is in the [WeOwnHealth](https://github.com/WeOwnHealth) org.
