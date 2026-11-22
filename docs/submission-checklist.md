# Submission checklist

Every requirement in the official guide that applies to our entries, with where we stand. **Submitted Nov 20.** Field-by-field text in `demos/devpost-submitted.md`. Re-checked against the guide on **Nov 19**; the only rule change since Nov 13 is the pitch length (4 minutes, was 5). Deadline: **Fri Nov 20, 12:00 PM CST** on Devpost.

Legend: ✅ done · 🟡 partly done · ❌ not started · ➖ not entering

## What we're entering

| Category | Entering | Prize |
|---|---|---|
| Main track: **Agentic Payments & AI** | yes | $2,000 |
| Chain award: **Best use of Arc** | yes | $1,000 |
| Bounty: **ElevenLabs** | yes | 3 months of Scale per member |
| Bounty: **QuickNode Streams** | yes | $500 |
| Bounty: Gemini Prediction Markets | ➖ | |
| Bounty: Grok Bot | ➖ | |
| Official Winner (automatic) | yes | up to $2,500 |

## Rules that apply to everyone

| Rule | Status | Notes |
|---|---|---|
| Built during the hackathon (from Thu Nov 12, 6 PM CST) | ✅ | Build repo `sunrobert/hotline` starts Nov 13. HQ repo holds only planning before that. |
| Exactly one main track; at most one chain award | ✅ | Agentic Payments & AI; Arc. |
| **Present in person at the closing ceremony, Sat Nov 21, UT Austin** | ❌ | Required to win anything, including bounties. Robert must be there. |
| Finalists: **4 min pitch + 2 min Q&A** (the guide changed from 5 min on Nov 19) | 🟡 | Pitch in `demos/pitch.md`, cut to 4 minutes with a cut order if it runs long. Q&A answers in `demos/qa-prep.md`. Not rehearsed. |

## What to submit (Devpost)

| Item | Status | Notes |
|---|---|---|
| Project name, short description, team members | 🟡 | Drafted in `demos/devpost.md`, with three name alternatives. |
| Main track, chain award, every bounty | 🟡 | Drafted in `demos/devpost.md`: Agentic Payments & AI, Arc, ElevenLabs, QuickNode. Opt in on Devpost. |
| Written answers: what, problem, how it works, what's unique, what's next | 🟡 | Drafted in `demos/devpost.md`. |
| Technologies and sponsor tools used | 🟡 | Drafted in `demos/devpost.md`. |
| Public GitHub repo with source and setup instructions | ✅ | https://github.com/sunrobert/hotline · README "Run it" section. |
| **Working demo or deployed app** | 🟡 | Works from the laptop through a tunnel. Judges can't call the Telnyx trial number (it only reaches verified numbers). Plan: the video plus the live demo at finals; the dashboard URL works while the laptop is up. |
| **2–3 minute demo video**, on YouTube or Drive, viewable by judges | ✅ | Recorded Nov 20 (2:59, Zoom, trimmed). Shows a live call with audio: 8 USDC approved with PIN, 60 blocked by the cap, an x402 price lookup, a Mandarin send, then the dashboard ledger. Uploaded to Drive. Does not show the QuickNode deposit or the outbound call; the live pitch covers those. |
| README with technical docs and architecture | ✅ | Decision loop, safety limits, architecture, Arc usage, tool API. |

## Agentic Payments & AI (main track)

| Requirement | Status | Evidence |
|---|---|---|
| Agent executes onchain transactions or reads the chain | ✅ | Real sends on Arc testnet, e.g. tx `0xfa62…6060` (29 USDC, approved by phone). |
| Document the agent's decision loop | ✅ | README "The decision loop". |
| Document the safety limits | ✅ | README "Safety limits" and "Known limitations". |
| Objective: spending controls and guardrails | ✅ | Caps, allowlist, gas reserve, approval threshold, spoken PIN, outbound approval calls. The core of the project. |
| Objective: agents paying per request (x402) | ✅ | `get_price`: the agent buys a spot price for 0.01 USDC per lookup over x402 v2 (exact scheme, EIP-3009 on Arc USDC), approved by the policy engine, settled on Arc in 1.3–2 s. First payment tx `0xaf44…6c51`. README "x402". |
| Recommended tools: x402, Circle Agent Wallets or Nanopayments, Solana Agent Kit | 🟡 | x402 used, following the v2 spec. Circle Wallets not yet (plan in `docs/circle-plan.md`); the wallet is a viem key held by the backend. |

## Best use of Arc

| Requirement | Status | Evidence |
|---|---|---|
| Core onchain functionality on Arc (testnet fine) | ✅ | All sends and deposit detection on Arc testnet. |
| Contract addresses used, in the README | ✅ | USDC system emitter, USDC ERC-20 interface, agent wallet. |
| Explain how the project uses Arc, in the README | ✅ | README "How it uses Arc": USDC as gas, EIP-7708 Transfer events, decimals, fee floor, finality. |
| Also submitted to a main track | ✅ | |
| Objective: combine Arc with Circle tools (Wallets, CCTP, Gateway, Paymaster) | ❌ | **Weak spot for the Circle judge.** No Circle product is used beyond USDC and Arc itself. |

## ElevenLabs bounty

| Requirement | Status | Evidence |
|---|---|---|
| ElevenLabs API or SDK as a core feature | ✅ | Voice is the whole interface. |
| **Demo video shows the integration working, with audio** | ✅ | Live phone call, English and Mandarin. |
| README says which ElevenLabs products are used and how | 🟡 | Covered across the README; needs one explicit list: Agents, webhook tools, SIP trunk and outbound calls, call-start webhook, language detection, voicemail detection, agent testing, two voices (Katie, Amy on v4 turbo), sound effects, browser SDK. |
| Also submitted to a main track | ✅ | |

## QuickNode Streams bounty (if we enter)

| Requirement | Status | Notes |
|---|---|---|
| Streams as a core data source | ✅ | The Stream triggers the outbound approval call. Verified live with the poller off: delivered 0.8 s after the block. |
| At least one Stream with a filter and a destination | ✅ | Arc testnet `logs`, filter keeps USDC system-emitter Transfers to the agent, webhook destination with HMAC verification. |
| README explains the Stream config and why | ✅ | README "QuickNode Streams: what makes the phone ring". |
| Account | ✅ | Build plan via the COLLEGEQN coupon, **card on file**. First month free from Nov 14; **cancel after finals and before it renews around Dec 14**, or it charges $49. |

## Participation perks (complete submission)

Working prototype in a public repo, README with technical docs, and the 2–3 minute video. Video is the only missing piece.
