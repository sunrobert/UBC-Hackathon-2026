# Submission checklist

Every requirement in the official guide that applies to our entries, with where we stand. Re-checked against the guide on **Nov 13**. Deadline: **Fri Nov 20, 12:00 PM CST** on Devpost.

Legend: ✅ done · 🟡 partly done · ❌ not started · ➖ not entering

## What we're entering

| Category | Entering | Prize |
|---|---|---|
| Main track: **Agentic Payments & AI** | yes | $2,000 |
| Chain award: **Best use of Arc** | yes | $1,000 |
| Bounty: **ElevenLabs** | yes | 3 months of Scale per member |
| Bounty: **QuickNode Streams** | decide | $500 |
| Bounty: Gemini Prediction Markets | ➖ | |
| Bounty: Grok Bot | ➖ | |
| Official Winner (automatic) | yes | up to $2,500 |

## Rules that apply to everyone

| Rule | Status | Notes |
|---|---|---|
| Built during the hackathon (from Thu Nov 12, 6 PM CST) | ✅ | Build repo `sunrobert/hotline` starts Nov 13. HQ repo holds only planning before that. |
| Exactly one main track; at most one chain award | ✅ | Agentic Payments & AI; Arc. |
| **Present in person at the closing ceremony, Sat Nov 21, UT Austin** | ❌ | Required to win anything, including bounties. Robert must be there. |
| Finalists: 5 min pitch + Q&A (deck says 2 or 5 min of Q&A) | ❌ | Prepare for 5 min of Q&A. |

## What to submit (Devpost)

| Item | Status | Notes |
|---|---|---|
| Project name, short description, team members | ❌ | "Hotline" is still a working name. |
| Main track, chain award, every bounty | ❌ | Opt in to each bounty on Devpost. |
| Written answers: what, problem, how it works, what's unique, what's next | ❌ | Draft in this repo first. |
| Technologies and sponsor tools used | ❌ | List below under each sponsor. |
| Public GitHub repo with source and setup instructions | ✅ | https://github.com/sunrobert/hotline · README "Run it" section. |
| **Working demo or deployed app** | 🟡 | Works from the laptop through a tunnel. Judges can't call the Telnyx trial number (it only reaches verified numbers). Plan: the video plus the live demo at finals; the dashboard URL works while the laptop is up. |
| **2–3 minute demo video**, on YouTube or Drive, viewable by judges | ❌ | Must show ElevenLabs working **with audio** (bounty rule). |
| README with technical docs and architecture | ✅ | Decision loop, safety limits, architecture, Arc usage, tool API. |

## Agentic Payments & AI (main track)

| Requirement | Status | Evidence |
|---|---|---|
| Agent executes onchain transactions or reads the chain | ✅ | Real sends on Arc testnet, e.g. tx `0xfa62…6060` (29 USDC, approved by phone). |
| Document the agent's decision loop | ✅ | README "The decision loop". |
| Document the safety limits | ✅ | README "Safety limits" and "Known limitations". |
| Objective: spending controls and guardrails | ✅ | Caps, allowlist, gas reserve, approval threshold, spoken PIN, outbound approval calls. The core of the project. |
| Objective: agents paying per request (x402) | ❌ | Stretch goal, not started. |
| Recommended tools: x402, Circle Agent Wallets or Nanopayments, Solana Agent Kit | ❌ | None used. The wallet is a viem key held by the backend. |

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
| **Demo video shows the integration working, with audio** | ❌ | |
| README says which ElevenLabs products are used and how | 🟡 | Covered across the README; needs one explicit list: Agents, webhook tools, SIP trunk and outbound calls, call-start webhook, language detection, voicemail detection, agent testing, two voices (Katie, Amy on v4 turbo), sound effects, browser SDK. |
| Also submitted to a main track | ✅ | |

## QuickNode Streams bounty (if we enter)

| Requirement | Status | Notes |
|---|---|---|
| Streams as a core data source | ❌ | Today a free RPC poller detects deposits. A Stream would become the primary trigger, with the poller as backup; dedup already handles both. |
| At least one Stream with a filter and a destination | ❌ | Filter: Arc testnet logs from the USDC system emitter to the agent wallet. Destination: webhook to the backend. |
| README explains the Stream config and why | ❌ | |
| Account | ❌ | Free trial reportedly needs no card. The guide's coupon (COLLEGEQN) is for the paid Build plan and its page says to enter it "before adding payment details," so likely a card: avoid under the no-spend rule. |

## Participation perks (complete submission)

Working prototype in a public repo, README with technical docs, and the 2–3 minute video. Video is the only missing piece.
