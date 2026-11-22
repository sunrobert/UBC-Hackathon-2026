# Devpost: what was submitted (Nov 20, 2026)

The text pasted into each Devpost field at submission, kept so it can be reused or quoted. `devpost.md` is the longer working draft these were cut from.

- **Main track:** Agentic Payments and AI
- **Chain award:** Best use of Arc
- **Bounties:** ElevenLabs, QuickNode Streams
- **Repo:** https://github.com/sunrobert/hotline
- **Videos (Google Drive):**
  1. Main demo, 2:59: a live inbound call. 8 USDC approved with a spoken PIN, 60 USDC blocked by the per-transaction cap, an x402 price lookup, a 1 USDC send in Mandarin, then the dashboard ledger.
  2. Second clip: a 20 USDC deposit reported by the QuickNode Stream, Hotline phoning the owner, and the 15 USDC sweep after a spoken yes and PIN.

## Contract addresses (field limit 255 characters)

```
Arc testnet 5042002. USDC: 0x3600000000000000000000000000000000000000; USDC event emitter: 0xffffFFFfFFffffffffffffffFfFFFfffFFFfFFfE; agent: 0x354ea63B9120b9d98fd8FbD18145055561EFBa9D; x402 seller: 0xeeF0429CEBBCd8693d142D489A630cFAcB9B40aF
```

## Built with

arc, circle, usdc, x402, eip-3009, elevenlabs, quicknode, quicknode-streams, typescript, node.js, hono, viem, sqlite, telnyx, cloudflare, claude, ethereum, evm, webhooks, voice-ai

## Project description

Hotline is an AI wallet agent on Arc that calls you before it spends. Talk to it on any phone, in your language. Small sends go through, larger ones need your spoken yes and PIN, and anything over your limits is refused.

**What did you build?**
A phone-first AI agent that holds and spends USDC on Arc testnet, where the phone call is the guardrail.
- Call it. Say "send 1 USDC to Alice." Small amounts go through. Anything over your auto-approve limit needs a spoken yes and your PIN. Anything over a cap is refused, and the agent names the rule that stopped it.
- It calls you. When USDC lands in the wallet and your standing rule ("keep 10, sweep the rest to savings") wants to move it, the agent phones you, states the amount and destination, and waits for your yes and PIN.
- Any language. It switches mid-call when you do, with a native Mandarin voice.
- It pays for what it needs. Ask "what's Ethereum at?" and it buys the price for one cent of USDC over x402, settled on Arc in under two seconds, within the same limits.
- A dashboard shows balance, limits, pending approvals, and every decision with its rule and explorer link.

**What problem does it solve?**
AI agents are getting wallets, and the hard part is consent, not spending. A notification gets swiped and a dashboard has to be open. A phone call reaches you anywhere, works on any phone with no app, and speaks your language. Hotline makes "human approval for large transactions" something you can hear. It is for people who don't live in crypto apps, older and multilingual users, and anyone who wants an agent with a budget but a human veto.

**How does it work?**
- Decision loop. Every intent, spoken or onchain, goes to a policy engine that returns AUTO, CALL, or BLOCK. Rules run in a fixed order, so each decision names one rule. BLOCK: paused, invalid amount, not on the allowlist, over the per-transaction cap, over the daily cap, or would breach the gas reserve. CALL: the action came from a deposit, or is over the approval threshold; it needs a spoken yes and PIN. Anything else is AUTO.
- Safety limits. Caps and the allowlist are checked again at approval time. Recipients are named by label only, never by raw address. The PIN gets one retry and is never repeated back. A yes approves only the amount that was read out. Interrupted actions fail closed.
- Voice. An ElevenLabs agent with seven webhook tools, calls over a Telnyx SIP trunk, language detection, and voicemail detection. The caller's number comes from the call itself, so the model can't be told who the owner is.
- Deposits. A QuickNode Stream on Arc testnet logs filters for USDC transfers into the agent's wallet and delivers them to a signed webhook about 0.8 seconds after the block. That is what makes the phone ring.
- x402. The price feed answers 402 Payment Required. The policy engine approves the payment, the agent signs an EIP-3009 authorization for exactly 0.01 USDC, and the seller settles it on Arc and pays the gas.
- Arc. USDC is both the asset and the gas token, so the agent keeps its gas reserve in the money it manages. Every send respects Arc's 20 gwei fee floor.
- Tests. 319 unit tests, plus 29 of 29 behaviour tests against the live agent in ten languages, including callers trying to talk it past the PIN.

**What makes it unique?**
The agent calls you. Every voice-crypto project we found takes calls; none places an approval call. It also pays for data by itself over x402, inside the same limits, because a one-cent price lookup shouldn't need a phone call. The guardrails are enforced in code and tested against adversarial callers: the agent can't be talked past a cap, can't pay an address it wasn't given, and can't be told by a "developer" to skip the PIN.

**What would you build next?**
- Circle Developer-Controlled Wallets for custody, so the key never sits on a laptop.
- iMessage: texted receipts, small commands by text, and "that's over your limit, calling you now."
- Stronger identity than caller ID plus PIN, such as a callback to a verified number.
- More standing rules: bills, top-ups, alerts.

**Technologies and sponsor tools**
- Arc testnet: all transfers and deposit detection, USDC as gas, EIP-7708 Transfer events, EIP-3009 for x402.
- ElevenLabs: Agents, webhook tools, SIP inbound and outbound calls, language and voicemail detection, agent testing API, voices (Katie; Amy on v4 turbo), sound effects, browser SDK.
- QuickNode: Streams on Arc testnet logs with a custom filter and a signed webhook.
- Circle: USDC and its EIP-3009 transferWithAuthorization, the Arc faucet.
- Other: TypeScript, Node, Hono, viem, SQLite, Telnyx, Cloudflare Tunnel, Claude as the agent's model.

## Technical summary

**Architecture.** A TypeScript backend (Node, Hono, SQLite via node:sqlite, viem) holds the agent's wallet on Arc testnet and runs a policy engine. Three things feed it: ElevenLabs voice-agent webhook tools, for spoken commands over phone (Telnyx SIP trunk) or browser; a QuickNode Stream, for onchain deposits; and x402 payment requests, for paid data. Every intent becomes an action that the engine classifies as AUTO, CALL, or BLOCK. Rules run in a fixed order and the first match names the decision. The result is written to a ledger with its rule, status, and transaction hash.

**Decision loop.** BLOCK: paused, invalid amount, not on the allowlist, over the per-transaction cap, over the daily cap, or would breach the gas reserve. CALL: the action came from a deposit rather than the owner, or is over the auto-approve threshold; it needs a spoken yes and PIN, by inbound or outbound phone call. Otherwise AUTO. Caps and the allowlist are checked again at approval time. Interrupted actions fail closed on restart and are never re-sent.

**Voice.** ElevenLabs Agents with seven webhook tools mapped one-to-one to backend endpoints. The caller ID and conversation ID come from ElevenLabs system variables, so the model can't claim to be the owner. Language detection, voicemail detection, and end call are on. Voices: Katie (English) and Amy (Mandarin, eleven_v4_turbo).

**Deposits (QuickNode Streams).** Arc testnet logs dataset. The filter keeps only USDC Transfer logs from Arc's system emitter addressed to the agent. The destination is a webhook that verifies QuickNode's HMAC signature. Measured 0.8 seconds from block to backend. An RPC poller is the backup, and deposits are deduplicated on transaction hash and log index.

**x402 v2.** Exact scheme on eip155:5042002. After the policy engine approves the payment, the agent signs an EIP-3009 TransferWithAuthorization for exactly the price (0.01 USDC, valid 60 seconds). Each lookup has a 0.05 USDC budget. The seller verifies the signature offline, checks the chain, produces the data, then settles with transferWithAuthorization and pays the gas. Replayed, tampered, and expired payments are refused. Settlement takes 1.3 to 2 seconds.

**Arc specifics.** USDC is the gas token, so the agent's gas reserve is held in the same USDC it manages. Each transfer is logged twice, by the system emitter (EIP-7708, 18 decimals) and the ERC-20 interface (6 decimals); only the system emitter is counted. Sends respect the 20 gwei fee floor. Finality is one block.

**Testing.** 319 unit tests. 29 of 29 behaviour tests pass against the live agent via the ElevenLabs testing API, in ten languages, including adversarial callers.

## About the project

### Inspiration
AI agents are getting wallets. Every demo shows the agent spending, and almost none show the human being asked first. A notification gets swiped and a dashboard has to be open, but a phone call reaches you anywhere, on any phone, in your language, with no app. So we made the phone call the guardrail: an AI wallet agent that calls you before it spends.

### How we built it
- Policy engine: a pure TypeScript engine classifies every intent as AUTO, CALL or BLOCK. Rules run in a fixed order, so every decision names exactly one rule. Caps and the allowlist are checked again at approval time.
- Voice: an ElevenLabs Conversational AI agent with seven webhook tools, phone calls over a Telnyx SIP trunk, inbound and outbound calls, language detection and voicemail detection.
- Arc testnet: USDC is both the asset and the gas. Deposits are detected from Arc's EIP-7708 system Transfer events.
- QuickNode Streams: a filtered logs Stream delivers deposits to a signed webhook about 0.8 seconds after the block, and that is what triggers the approval call.
- x402 v2: the agent signs an EIP-3009 TransferWithAuthorization on Arc's USDC; the seller verifies it, then settles on chain and pays the gas.

### Challenges
- Arc logs every USDC transfer twice (18 and 6 decimals), so we had to match the system emitter to count each one once.
- Transactions under Arc's 20 gwei fee floor are silently dropped.
- viem polled receipts every 4 seconds on a chain with roughly one-second blocks; polling every 250 ms took paid lookups from 8.9 s to 1.3–2 s.
- No public x402 facilitator serves Arc testnet, so our seller settles its own payments.
- Making sure a caller can't talk the model past a cap, or into skipping the PIN by claiming to be "the developer."

### What we learned
Guardrails have to live in code, not in the prompt. The model proposes and the engine decides. Voice is a surprisingly strong consent channel: hearing the amount read back changes how people approve.
