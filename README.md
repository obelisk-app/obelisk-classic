<p align="center">
  <img src="public/obelisk-md.gif" alt="Obelisk" width="50%" style="max-height: 320px; object-fit: cover;" />
</p>

<h1 align="center">Obelisk</h1>

<p align="center">
  <b>The Discord alternative with Nostr login.</b><br/>
  Group chat for crypto and privacy folks — no email, no password, no phone number, just your Nostr keys.
</p>

<p align="center">
  <a href="https://classic.obelisk.ar">Live app (classic)</a> ·
  <a href="ROADMAP.md">Roadmap</a> ·
  <a href="DEPLOY.md">Self-host</a> ·
  <a href="docs/">Docs</a>
</p>

<p align="center">
  <a href="https://github.com/obelisk-app/obelisk-classic/stargazers"><img src="https://img.shields.io/github/stars/obelisk-app/obelisk-classic?style=flat&logo=github&color=b4f953&labelColor=0a0a0a" alt="GitHub stars" /></a>
  <a href="https://classic.obelisk.ar"><img src="https://img.shields.io/badge/chat-classic.obelisk.ar-b4f953?style=flat&labelColor=0a0a0a" alt="Join the Obelisk server" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/obelisk-app/obelisk-classic?style=flat&color=b4f953&labelColor=0a0a0a" alt="License" /></a>
  <a href="https://lacrypta.ar"><img src="https://img.shields.io/badge/built%20for-La%20Crypta%20IDENTITY-b4f953?style=flat&labelColor=0a0a0a" alt="La Crypta IDENTITY Hackathon" /></a>
</p>

---

> ⚠️ **This is "classic" Obelisk — maintenance mode.**
>
> The current Obelisk app is the **relay-only rewrite** at **[github.com/obelisk-app/obelisk](https://github.com/obelisk-app/obelisk)** (deployed at [obelisk.ar](https://obelisk.ar)). New features land there.
>
> **This repo** is the original Postgres + Prisma + Socket.io + NDK stack, deployed at [classic.obelisk.ar](https://classic.obelisk.ar). Kept online as long as users rely on it; security patches only — no new features.

Obelisk feels like Discord — servers, channels, voice, threads, reactions, forums, DMs — but your account is a Nostr keypair, not an email on a corporate server. Built for La Crypta's **IDENTITY Hackathon** (April 2026).

## The Obelisk family

| Repo | What |
|------|------|
| [obelisk-app/obelisk](https://github.com/obelisk-app/obelisk) | The current app — relay-only rewrite |
| [**obelisk-app/obelisk-classic**](https://github.com/obelisk-app/obelisk-classic) | This repo — original centralized stack |
| [obelisk-app/obelisk-relay](https://github.com/obelisk-app/obelisk-relay) | NIP-29 groups relay (Rust) |
| [obelisk-app/obelisk-sfu](https://github.com/obelisk-app/obelisk-sfu) | mediasoup SFU for voice |
| [obelisk-app/obelisk-bots](https://github.com/obelisk-app/obelisk-bots) | Nostr bots toolkit |

## Why (it shipped)

- **No personal data.** Identity is a Nostr keypair — no email, phone, or device fingerprint.
- **Self-hosted.** Every instance runs on its operator's VPS. No vendor in the middle.
- **Built to evolve fast.** Voice, zaps, WoT spam filtering, AI-agent admin CLI all landed in one hackathon cycle.

Used in production:
- **~75 users** at [classic.obelisk.ar](https://classic.obelisk.ar)
- **20+ users** migrated from La Crypta's Discord

## Features

- 🔑 **Nostr login** — NIP-07, nsec, or NIP-46 bunker (QR). No signup forms.
- 💬 **Real-time chat** — channels, threads, reactions, mentions, file uploads, NIP-50 search.
- 🎙️ **Voice channels** — WebSocket audio relay via Socket.io (works through tunnels).
- 🔒 **Encrypted DMs** — NIP-17 gift-wrapped private messages.
- 🛡️ **WoT spam filter** — new accounts scored against the server's follow graph. No CAPTCHAs.
- ⚡ **Bitcoin zaps** — NIP-47 NWC; wallet string encrypted client-side, per-user spend budgets.
- 🤖 **Admin CLI for AI agents** — `npm run admin` drives the same API the web UI uses. Role checks enforced server-side.
- 👮 **Moderation** — roles, mutes, warnings, bans, reports, audit log, forums.
- 🎮 **Games** — chess, tic-tac-toe, chain reaction.
- 🏠 **Self-hostable** — Docker Compose on a 2 GB VPS handles hundreds of concurrent users.
- 🌍 **i18n** — English and Spanish.

## Screenshots

<p align="center">
  <img src="docs/screenshots/landing-hero.png" alt="Landing page" width="800" />
</p>

<table>
  <tr>
    <td width="50%"><img src="docs/screenshots/chat-view.png" alt="Chat view" /><br/><sub><b>Chat</b> — servers, channels, threads, reactions.</sub></td>
    <td width="50%"><img src="docs/screenshots/voice-channel.png" alt="Voice channel" /><br/><sub><b>Voice</b> — WebSocket audio relay via Socket.io.</sub></td>
  </tr>
  <tr>
    <td><img src="docs/screenshots/login-modal.png" alt="Login modal" /><br/><sub><b>Login</b> — NIP-07, nsec, or NIP-46 bunker (QR).</sub></td>
    <td><img src="docs/screenshots/admin-panel.png" alt="Admin panel" /><br/><sub><b>Admin</b> — members, roles, permissions.</sub></td>
  </tr>
  <tr>
    <td><img src="docs/screenshots/moderation-dashboard.png" alt="Moderation dashboard" /><br/><sub><b>Moderation</b> — reports, mutes, bans, audit log.</sub></td>
    <td><img src="docs/screenshots/games-chess.png" alt="Games — chess" /><br/><sub><b>Games</b> — chess, tic-tac-toe, chain reaction.</sub></td>
  </tr>
</table>

## Stack

| Layer | Tech |
|-------|------|
| Frontend | Next.js 16 + TypeScript + Tailwind CSS v4 |
| Auth / Identity | Nostr (NDK v3 + nostr-tools) |
| API | Next.js API Routes + custom `server.ts` |
| Real-time | Socket.io (messages + voice audio relay) |
| Database | PostgreSQL |
| ORM | Prisma 7 + `@prisma/adapter-pg` |
| State | Zustand |
| Payments | Nostr Wallet Connect (NIP-47) + Lightning |
| Admin tooling | `scripts/admin-cli` — nsec / NIP-46 bunker CLI for humans & AI agents |
| Testing | Vitest + React Testing Library |
| Deploy | Docker Compose + Caddy (auto HTTPS) |

## Quick Start (dev)

```bash
git clone https://github.com/obelisk-app/obelisk-classic.git
cd obelisk
npm install
docker compose up -d db         # PostgreSQL
npx prisma migrate dev
npm run dev                     # Next.js + Socket.io at :3000
```

Open [http://localhost:3000](http://localhost:3000).

### Expose dev server over HTTPS (for NIP-07 / mobile testing)

```bash
npm run dev:raise               # dev server + Cloudflare tunnel
```

Requires a Cloudflare tunnel of your own. Create one with `cloudflared tunnel create <name>` and `cloudflared tunnel route dns <name> <your.host>`, then set `TUNNEL_NAME` and `TUNNEL_HOSTNAME` in `.env` (see [docs/cloudflare-tunnel.md](docs/cloudflare-tunnel.md)).

## Self-Hosting

See [DEPLOY.md](DEPLOY.md) for full setup. The short version:

```
Internet → Caddy (:443, auto Let's Encrypt) → Obelisk (:3000) → PostgreSQL (:5432)
```

A 2 GB VPS (~$5/month) handles hundreds of concurrent users with voice. All features work self-hosted — there is no cloud-only tier.

## Auth Flow

1. Client requests login (NIP-07 / nsec / NIP-46 bunker).
2. Server generates a challenge (random string + timestamp).
3. Client signs the challenge with the Nostr key.
4. Server verifies the signature against the pubkey.
5. Server creates a session in DB, returns a session token.
6. All subsequent API requests carry the token.

## Data Model

Prisma schema at [`prisma/schema.prisma`](prisma/schema.prisma). Core entities:

```
Server    → Channels, Members, Roles, Bans, Mutes, Reports, Warnings
Channel   → Messages (threads, reactions, reply_to)
Message   → author (Nostr pubkey), content, attachments, mentions
Member    → pubkey + role + cached Nostr profile
Session   → pubkey, token, expiresAt
```

## NIPs Used

| NIP | What | Where |
|-----|------|-------|
| NIP-01 | Events & profiles | Profile data (kind 0) |
| NIP-05 | DNS verification | Display verification badge |
| NIP-07 | Browser extension signer | Login |
| NIP-17 | Private DMs (gift-wrapped) | Direct messages |
| NIP-46 | Nostr Connect (bunker) | Login via QR + admin CLI auth |
| NIP-47 | Nostr Wallet Connect | In-chat Bitcoin zaps |
| NIP-57 | Lightning zaps | Zap receipts |
| NIP-65 | Relay list metadata | Auto-fetch user relays |

## Scripts

```bash
npm run dev               # dev server (Next.js + Socket.io)
npm run dev:raise         # dev server + Cloudflare tunnel
npm run raise             # production deploy
npm run build             # prisma generate + migrate deploy + next build
npm run test              # vitest run
npm run test:watch        # vitest watch
npm run test:coverage     # vitest + coverage report
npm run admin -- <cmd>    # CLI for admin operations (see scripts/admin-cli/)
npx prisma migrate dev    # run migrations
npx prisma db seed        # seed database
```

## Testing

Vitest + RTL, co-located `Component.test.tsx` files next to sources. A feature is not done until its tests are written, passing, and the full suite runs green.

## Contributing

Issues and PRs welcome. Before submitting:

1. Run `npm run test` — everything must pass.
2. Follow the La Crypta design system (`lc-*` CSS classes, `lc-green` accent).
3. For real-time endpoints: match the relations emitted over Socket.io to what the GET endpoint returns (otherwise UI breaks until refresh).

See [CLAUDE.md](CLAUDE.md) for detailed architecture & conventions.

## Roadmap

See [ROADMAP.md](ROADMAP.md). TL;DR: Phases 0–3 are done (foundation, auth, chat, admin/moderation, voice, DMs, multi-server, uploads, search, bots). Phase 4 (PWA, push, themes, launch polish) is in progress — the admin CLI shipped as part of it. Phase 6 (Lightning zaps over NWC) is partially live: wallet connect + user-to-user zaps work today; emoji zaps and leaderboards are still pending. Phase 5 sunsets the centralized DB for Nostr-native groups (NIP-28, NIP-29, NIP-59).

## Resources

- [NDK Docs](https://ndk.fyi) · [Nostr Protocol](https://nostr.com) · [NIPs](https://github.com/nostr-protocol/nips) · [Nostr WoT](https://nostr-wot.com/docs) · [La Crypta](https://lacrypta.ar)
- Docs: [voice system](docs/voice-system.md) · [WoT & invite credits](docs/wot-and-invite-credits.md) · [uploads](docs/uploads.md) · [Cloudflare tunnel](docs/cloudflare-tunnel.md) · [Bitcoin zaps (NWC)](docs/bitcoin-zaps-nwc.md) · [Admin CLI for agents](docs/admin-cli.md)
