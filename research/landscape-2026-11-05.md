# Landscape research — 2026-11-05

Searches used generic category terms only. Verify anything marked (unverified) against official docs before building.

## Arc (Circle's L1)

- **Mainnet is live** since Sept 16, 2026. USDC is gas, sub-second finality. Day-one apps: Aave V4, Morpho, Uniswap (v4 per one report), 100+ apps claimed.
  - https://www.theblock.co/news/ecosystems/2026-09-16-circle-launches-arc-mainnet-with-blackrock-and-visa-among-validators-mints-10-billion-arc-tokens-415250
- **Testnet** live since Oct 28, 2025. Community-deployed Uniswap V2 on testnet (unverified): https://github.com/circlefin/arc-node/issues/160
- Chainlink named as day-one integration but feed addresses not settled in any source found. Check https://docs.chain.link.
- Ecosystem directory: https://www.arc.io/ecosystem
- Official docs: docs.arc.network, https://developers.circle.com

## Circle Agent Stack

- Agent Wallets: user-controlled 2-of-2 MPC, agent never holds key shares. https://developers.circle.com/agent-stack/agent-wallets
- Spending policies: per-tx / daily / weekly / monthly transfer limits, recipient allowlists, contract blocklists. **Mainnet only. Testnet does not enforce policies.** https://developers.circle.com/agent-stack/agent-wallets/wallet-operations/custom-policies
- Circle CLI is the primary interface (email OTP). `circle wallet create --type agent --testnet` works; `circle wallet limit` is mainnet-only. https://developers.circle.com/agent-stack/circle-cli/command-reference
- Agent Nanopayments = x402 payments in sub-cent USDC, no gas. https://developers.circle.com/agent-stack/agent-nanopayments

## ElevenLabs Agents telephony

- Outbound call: `POST /v1/convai/twilio/outbound-call` with `agent_id`, `agent_phone_number_id`, `to_number`, optional `conversation_initiation_client_data` (use this to inject the approval context into the call). Returns `conversation_id` + Twilio `callSid`. https://elevenlabs.io/docs/api-reference/twilio/outbound-call
- Server tools (webhooks) configured in the agent's prompt config; the agent calls your backend mid-conversation. Also `elevenlabs tools add-webhook` via CLI.
- Inbound: link a Twilio number to the agent in the ElevenLabs dashboard.

## QuickNode Streams

- Arc testnet supported with all datasets; Arc mainnet listed "coming soon" on the REST API page at time of search. Re-check on Nov 13. https://www.quicknode.com/docs/streams/supported-chains
- Marketing page claims real-time Arc blocks/logs/traces: https://www.quicknode.com/chains/arc

## Prior art (voice + onchain)

All of these are **inbound only**: the user dials in and speaks a command. None found that place an outbound approval call.

| Project | Venue | Notes |
|---|---|---|
| Cymatic | ETHGlobal | Phone call -> onchain action, Python/FastAPI, phone-number-as-identity. https://ethglobal.com/showcase/cymatic-vedz7 |
| Call DeFAI Engine | Chainlink hack | Phone DeFi execution; Vapi STT + second independent ElevenLabs STT pass for verification. https://chain.link/hack-26/projects/call-defai-engine |
| Baseline | Devfolio Mar 2025 | Call-in onboarding, embedded wallet, Coinbase AgentKit. https://devfolio.co/projects/baseline-16c5 |
| VoiceVault | lablab.ai | Voice DeFi **on Arc**, browser voice not phone. https://lablab.ai/submissions/b0cnjqu41oqdf613oagnzgen |
| Circle tutorial | Circle blog | AI agent pays for and places a call with Agent Wallet. https://www.circle.com/blog/build-a-voice-call-automation-with-circle-agent-wallet-ai-assistants |

Also seen: eva, speaky, ethtalk, say-less, Chain Speak, basetone on ETHGlobal/Devfolio. Same shape.

## Three-layer read

- **Layer 1 (everyone knows):** voice is a nice input for crypto; "talk to your wallet" demos well.
- **Layer 2 (what's out there):** a dozen hackathon projects do exactly that. Sponsors keep listing it as an example, so it keeps getting built. Nobody has shipped one people use.
- **Layer 3 (where they're wrong):** they treat voice as an *input device*. The real advantage of a phone call in agentic finance is that it's an *interrupt*. Phones ring, screens don't. An agent with a budget needs a consent channel that reaches the human anywhere with zero app install. The phone call is the guardrail, not the UI.

## iMessage transport (added 2026-11-09)

Apple has no public iMessage API. Every route is a bridge. Vendor comparison pages are written by competitors; treat prices as approximate.

- **Self-hosted on a Mac:** Photon `imessage-kit` (TypeScript, open source) https://github.com/photon-hq/imessage-kit ; BlueBubbles (REST + webhooks); `imsg` CLI (macOS 14+, Full Disk Access). Mac must stay awake; a personal Apple ID sending volume can be flagged.
- **Hosted:** LoopMessage (~$20/mo shared for AI assistants per one source), Blooio, Tuco, Sendblue ($100/mo AI Agent tier reported as inbound-only), Linq (sales-gated, ~$250/line + setup per a competitor). https://www.sendblue.com/blog/best-imessage-api-comparison , https://blooio.com/blog/best-imessage-api-2026 , https://zerosettle.io/blog/best-imessage-api-providers/
- **SMS on Twilio:** unregistered US 10DLC is blocked outright (error 30034), pending registration doesn't count. Sole-proprietor brand: one campaign, one number, 1,000 msg/day; about $4 + $15 + $2/mo; approval from ~2 days to weeks. https://support.twilio.com/hc/en-us/articles/14910496447771-Shutdown-of-Unregistered-10DLC-Messaging
