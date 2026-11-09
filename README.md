# Hotline — a voice agent that calls you before it spends

**UBC 2026 Hackathon HQ** · Agentic Payments & AI track · Arc testnet · Nov 13–20, 2026 · Finals Nov 21, UT Austin

> Status: **planning**. Hacking starts Fri Nov 13 at 12:00 PM CST. Per the rules, no project code exists in this repo before then. The build repo will be linked here on day one.

## The idea

Hotline is a phone number you call to run an onchain wallet with your voice. It holds USDC on Arc testnet and acts within limits you set.

- **"Send 5 to Alice."** Done, under your auto-approve threshold.
- **"Send 80 to Alice."** Over the threshold. The agent asks for a spoken yes and your PIN, then sends.
- **"Send 300."** Blocked. It tells you which rule stopped it.

The part no one else has: **it calls you.** When a deposit lands in the agent's wallet and your standing rule says act (keep 100 on hand, sweep the rest to savings), your phone rings. The agent explains what arrived, proposes the move, and waits for a spoken yes plus PIN before touching anything.

The phone call is the guardrail. Every prior voice-crypto project only takes calls. This one makes them.

And it speaks your language. Any phone, any language, no app. The agent covers 30+ languages and switches mid-call when you do: start in English, continue in Mandarin, and the rules, limits, and PIN stay the same underneath.

## The demo

1. Dial the number live. Show auto, ask-first, and blocked, out loud. Start in English, switch to Mandarin mid-call.
2. Hang up. Send testnet USDC from a laptop.
3. The phone rings on stage. Say yes. The transaction shows up on the Arc explorer.

About four minutes.

## Why this track, this chain, these bounties

| Target | Why it fits |
|---|---|
| **Agentic Payments & AI** (main track) | Judged on the agent's decision loop and safety limits. That is the whole product. |
| **Best use of Arc** | USDC as gas means "the agent spent 0.40 USDC" is a sentence a judge understands on the phone. Circle wallet SDK if it supports Arc testnet. |
| **ElevenLabs bounty** | Voice is the entire interface, not an add-on. Multilingual on a phone line is their home turf. The demo video has audio by construction. |
| **QuickNode Streams bounty** | A Stream watching the agent's wallet on Arc is what makes the phone ring. |

## How it works

```
Owner phone <── Twilio ──> ElevenLabs Agent ──server tools──> Backend (TypeScript)
     ^                                                           ├─ Policy engine: AUTO | CALL | BLOCK
     └── outbound approval call ─────────────────────────────────┤  (per-tx cap, daily cap, allowlist, gas reserve, approval threshold, PIN)
                                                                 ├─ Ledger: every decision, rule fired, tx hash
                                                                 ├─ Wallet on Arc testnet (Circle SDK or viem)
                                                                 ├─ Deposit trigger: QuickNode Streams (+ RPC poller fallback)
                                                                 └─ One-page dashboard
```

Solo build, TypeScript end to end, no custom contracts, **no real money**.

Stretch, in order: the agent paying a sub-cent USDC fee for a price quote (x402-style), then a swap or CCTP bridge.

## Repo layout

| Folder | What's here |
|---|---|
| [`ideas/01-hotline-voice-agent.md`](ideas/01-hotline-voice-agent.md) | The full design doc: architecture, decision loop, demo config, build order with cut lines, README checklist, open questions |
| [`docs/hackathon-brief.md`](docs/hackathon-brief.md) | Rules, tracks, prizes, timeline, submission checklist, condensed |
| [`docs/hackathon-guide-full.md`](docs/hackathon-guide-full.md) | The organizers' full guide |
| [`research/`](research/) | What's live on Arc, ElevenLabs telephony APIs, Circle testnet limits, prior voice-crypto projects |
| `demos/` | Demo script, video storyboard, pitch (coming) |
| `project/` | Empty until Nov 13 by rule. Build repo linked here on day one. |

## Timeline (CST)

| When | What |
|---|---|
| Nov 12, 6 PM | Kickoff call |
| Nov 13, 12 PM | Hacking starts |
| Nov 16–19 | Sponsor workshops and office hours |
| Nov 19 night | Target submission (deadline is Nov 20, 12 PM) |
| Nov 21 | Finals at UT Austin |

## Links

- Hackathon: https://www.universityblockchain.org/programs/hackathon
- Devpost: https://ubc-hackathon-2026.devpost.com
- Telegram: https://t.me/+Q0hy2P7nbIk2YWIx

## Team

Robert Sun ([@sunrobert](https://github.com/sunrobert)), solo.

"Hotline" is a working name.
