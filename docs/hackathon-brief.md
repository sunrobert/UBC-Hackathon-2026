# UBC 2026 Hackathon — Brief

Condensed from the official guide ([full copy](hackathon-guide-full.md)) and
https://www.universityblockchain.org/programs/hackathon. Captured 2026-11-05.

Submit on Devpost: https://ubc-hackathon-2026.devpost.com
Telegram: https://t.me/+NfVyaGKfiF5hY2Nh (link from the kickoff deck)
Kickoff changes: [kickoff-notes.md](kickoff-notes.md)

## Timeline (all CST)

| When | What |
|---|---|
| Thu Nov 12, 6:00 PM | Kickoff call **and hacking starts** (confirmed at kickoff; ignore Devpost's Friday-noon start) |
| Mon–Thu Nov 16–19 | Solana + Circle workshops, nightly sponsor office hours |
| Fri Nov 20, 12:00 PM | **Submission deadline on Devpost** |
| Fri Nov 20, 11:59 PM | Finalists notified |
| Sat Nov 21 | Finals at UT Austin: 5 min pitch + 2 min Q&A, winners at closing ceremony |

**You must be in Austin in person for the closing ceremony to win anything, including bounties.**

## Structure

- Pick **exactly one** main track.
- Optionally pick **one** chain award (Solana or Arc, never both), judged within your track.
- Opt into as many **bounties** as you qualify for.
- Every submission is automatically in the running for Official Winner (1st/2nd/3rd).
- All prizes stack (except Solana vs Arc).

## Main tracks ($2,000 each)

1. **Agentic Payments & AI** — agents that hold/send/receive stablecoins, pay per-request for APIs/data/compute (x402, Circle Agent Wallets / Nanopayments, Solana Agent Kit recommended). Must: execute or read onchain on any chain (devnet ok); document the agent's decision loop and safety limits.
2. **DeFi & Onchain Apps** — new primitives or meaningful improvements; compose with existing protocols; cross-chain via CCTP. Must: interact with smart contracts (deploying your own optional); README explains economic design + risk assumptions; list contract/program addresses.
3. **Consumer Apps** — crypto is invisible; abstract bridging, gas, seed phrases; daily-use. Must: touch the chain somehow; **working user-facing frontend** (web or mobile).

## Chain awards (within each track)

- **Best use of Solana** — $1,500 × 3. Anchor/native Rust, SPL, Token Extensions, Solana Pay. Core onchain functionality on Solana (devnet fine, using existing programs counts). README: program IDs + how Solana is used.
- **Best use of Arc** — $1,000 × 3. Circle's EVM L1, USDC as native gas. Hardhat/Foundry; combine with Circle Wallets, CCTP, Gateway, Paymaster. README: contract addresses + how Arc is used.

## Bounties

| Bounty | Prize | Requirement |
|---|---|---|
| Gemini Prediction Markets | $2,500 / $1,000 / $500 | Use Gemini prediction market data and/or trading APIs. 1st place also pitches at finals. |
| QuickNode Streams | $500 | Streams as core data source; ≥1 Stream with filter + destination; README explains config. |
| ElevenLabs | 3 mo Scale per member | Voice/audio central, not an add-on; demo video must show it with audio. |
| Grok Bot | Mechanical keyboard per member | Grok Bot on X does real work; include chat export + 3–4 sentence README note. |

## Official Winner (all submissions)

1st $2,500 + 3 mo ElevenLabs Pro per member · 2nd $1,000 · 3rd $500

## Participation (complete, working submission)

1 month ElevenLabs Creator, $49/mo QuickNode plan, X Premium (first 300 participants).

## Max stack example (from the organizers)

DeFi prediction market on Solana using Gemini API:
1st overall $2,500 + DeFi Track $2,000 + Solana $1,500 + Gemini 1st $2,500 = **$8,500**

## Who picks finalists (up to 13)

- 3 per track: top contender for Track Winner, Best use of Solana, Best use of Arc
- Top 3 contenders for Official Winner
- 1st place Gemini bounty team

Track Winner chosen by UBC team. Solana award by Solana rep. Arc award by Arc rep. Bounties by sponsor + UBC rep.

## Judging criteria (all categories)

1. Technical execution: functionality, depth, effective use of blockchain infra
2. Product & UX: clear problem, intuitive, quality
3. Innovation: originality
4. Impact & potential: real-world usefulness, could become a product
5. Demo: quality of live demo, clear communication

## What to submit

- Name, short description, team members
- Main track, chain award (or None), every bounty
- Written answers: What did you build? What problem? How does it work? What makes it unique? What next?
- Technologies / sponsor tools used
- **Public GitHub repo** with source + setup instructions (built during the hackathon)
- Working demo or deployed app
- **2–3 min demo video** (YouTube or Drive, accessible to judges)
- README with technical docs / architecture overview
- Track-specific items (contract addresses, decision loop + safety limits, etc.)

## Rules

- Teams of 1–4 recommended; solo fine.
- **No pre-existing projects.** Must be built during the hackathon: Nov 12, 6 PM CST to Nov 20, 12 PM CST. (Brainstorming, design docs, and research before that are fine. Code is not.)
- AI tools encouraged. Still has to be a working, substantive build.
- You keep all IP.
- Judges' decisions are final.
