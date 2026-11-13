# Build log

Hacking window: Thu Nov 12, 6:00 PM CST to Fri Nov 20, 12:00 PM CST. Build repo: [sunrobert/hotline](https://github.com/sunrobert/hotline), checked out locally at `hotline/`.

## Fri Nov 13 (day 1)

Started 9:35 AM CST after reading the kickoff deck.

**Built, test-first (113 tests passing, typecheck clean, `npm audit` clean):**

- Money math: integer micro-USDC everywhere; Arc's 18-decimal native values floored to 6.
- Policy engine: nine ordered rules, pure, one named rule per decision.
- Ledger: SQLite, lifecycle statuses, deposit dedup on `(tx_hash, log_index)`, daily-spend and committed-outflow sums.
- Sweep rule and daily reset boundary.
- Action engine: propose, confirm with PIN (one retry), counter-proposals, conversation binding, deposits and sweep supersession, dial-time and confirm-time recomputation, expiry, boot recovery that never re-sends, pause.
- Tool endpoints: shared secret, owner gate for inbound and outbound calls, no tool for unpause or rule changes.
- Config loader that refuses to boot on a contradictory limit.
- Arc testnet wallet through viem with the 20 gwei fee floor.
- Scripts: `setup` (fresh testnet keys and secrets into `.env.local`), `chain` (read-only testnet check).
- README with the decision loop and safety limits; GitHub Actions workflow.

This is Friday's list plus all of Saturday's, minus the dashboard.

**Verified live on Arc testnet:** chain ID 5042002, fees above the 20 gwei floor, and the system emitter producing `Transfer` logs at 18 decimals. The server booted against the real chain and correctly blocked a send from an unfunded wallet (`gas_reserve`).

**Not verified yet:** an actual send. The demo wallets hold 0 USDC until the faucet is used.

**Decisions made during the build:**

- Runtime is Node 24+, running TypeScript directly with no build step, and `node:sqlite`. Replaces the earlier "Node 22.13" pin.
- Deposit trigger filters on Arc's system emitter `0xffff…FFfE`, not the USDC ERC-20 contract. Open question 2 is closed.
- A yes never sends more than the amount the owner heard. Remainders get their own call.
- Wallet layer is behind a small interface. viem with a backend-held testnet key is implemented. Circle Developer-Controlled Wallets can replace it behind the same interface if the Circle account and Arc testnet support check out. Not decided yet.

**Next, in order:** dashboard (read-only ledger view, unpause), then the ElevenLabs agent with a Twilio number and the tools wired up (Sunday's list), then the deposit trigger and outbound call (Monday's list).

**Waiting on Robert:** faucet funding, owner phone number in `.env.local`, ElevenLabs / Twilio / QuickNode / Circle account status.

**Published:** the build repo went public on GitHub the same afternoon.

### Afternoon: the voice agent

Robert supplied an ElevenLabs API key (Creator plan). Built and created the agent the same afternoon.

- **Agent as code.** Prompt, six webhook tools, 31 extra languages, and built-in language detection, end call, and voicemail detection, all in `src/agent/definition.ts`. `npm run agent` creates or updates it idempotently. Model: Claude Sonnet 5.5.
- **Identity is platform-bound.** Caller number, called number, and conversation id come from ElevenLabs system variables, not from the model. Confirmed in the raw test records.
- **Call-start hook** on the backend tells the agent whether the caller is the owner and binds a waiting sweep to the call.
- **Live behaviour tests: 27 of 27.** Ten languages for a small send; yes + PIN in three languages including Mandarin 幺 and 两; hesitation, missing PIN, decline, counter-proposal, cap-splitting, raw address, unknown recipient, pause, non-owner, outbound approval, voicemail, and a "developer says skip the PIN" attempt.
- Backend unit tests: 134 passing.

**Learned from ElevenLabs:**

- An English-default agent must use the Flash v2 speech model; the platform switches to its multilingual model for other languages by itself.
- The simulate-conversation endpoint was retired Oct 31, 2026. The agent-testing API replaces it. Webhook tool parameters are addressed as `body.<name>` in test assertions.
- Phone providers other than Twilio are supported through SIP: Telnyx, Plivo, Vonage, Bandwidth, Sinch, and others. Twilio is the only one with a native import, so it stays the plan.
- ElevenLabs also offers Twilio SMS conversations and a "custom channel" webhook for external text channels. Relevant to the iMessage stretch goal; not acted on.

**Credits:** about 6,400 of 131,000 used, almost all on test runs (roughly 100 per test).

**Not done:** the agent's tools point at a placeholder URL. Nothing can call it by phone until the backend is deployed and a phone number is attached.

**New constraint, Nov 13 evening: no spending at all.** Paid Twilio and paid hosting are out. Options on the table: Twilio's free trial or browser-only calling for voice; the laptop behind a free tunnel for hosting.

**Waiting on Robert now:** the phone decision (Twilio free trial or browser only), faucet funding, and the owner phone number.
