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

**Phone decision: Twilio's free Limited trial** (no card, 30 days, a temporary trial number, verified numbers only). Browser calling stays the fallback if ElevenLabs cannot import a temporary trial number, which is untested.

### Evening: the path from deposit to phone call

- **Deposit watcher.** Decodes Arc's system-emitter Transfer logs into deposits; ignores the ERC-20 emitter, transfers to others, dust, and pending logs. Runs as an RPC poller, the fallback trigger from the design, so the ring does not depend on QuickNode.
- **Call queue.** One call at a time, two attempts ninety seconds apart, then `expired_no_answer`. The amount is recomputed at dial time and then frozen: binding the call never changes it.
- **Dialer.** Places calls through ElevenLabs' Twilio outbound endpoint and polls the conversation status to learn when a call ends. Polling replaces the post-call webhook from the design: one less secret and one less thing to configure.
- **Scripts.** `npm run phone` imports the Twilio number and assigns the agent; `npm run demo:deposit -- 200` sends testnet USDC from the sender wallet, which is the on-stage trigger.
- Backend unit tests: 162 passing. The server boots with the poller running against Arc testnet.

**Twilio's free trial cannot carry the voice agent.** Robert noticed the trial number is shared. Twilio's trial docs go further: `<Stream>` and `<Dial><Sip>` are blocked on trial accounts, and those are the only ways to connect a call to ElevenLabs. `npm run phone` (native import) will not work on this account. The call queue, dialer interface, and deposit watcher are unaffected: the queue talks to a `Dialer` interface, so a different way of placing the call slots in behind it. Options are in the design doc's constraints section.

### Evening: dashboard and browser calling

- **Dashboard** at `/dashboard`: balance, limits, recipients, pending approvals, ledger with explorer links, unpause, and a development-only simulated deposit. One static page, no build step, no secrets in the source; the token goes in a header.
- **Browser calling.** "Call Hotline" starts a voice session with the agent from the page, with no phone number. The server issues a short-lived ElevenLabs conversation token. Because a browser session has no caller number, the page binds its conversation id with the dashboard token, and only that conversation's tool calls pass the owner gate.
- A waiting sweep is described to the agent at its recomputed amount when the call starts and bound at that same amount when the call connects, so the number heard is the number approved.
- Backend unit tests: 193 passing.

**Verified by running it:** the page renders in light, dark, and phone width; the sign-in gate rejects a wrong token; live state loads from Arc testnet; a simulated deposit appears in the ledger; the pinned ElevenLabs client loads from the CDN; and `/api/call/start` returned a real conversation token from ElevenLabs.

**Not verified:** an actual voice session (needs a microphone), and any tool call during one (needs the backend reachable from the internet, which needs a tunnel Robert has not approved yet).

**Not verified:** no real call has been placed and no real deposit has been detected. Both need Robert's inputs below.

**Waiting on Robert now:** the three Twilio values and his mobile number in `.env.local`, faucet funding for the sender and agent wallets, and a yes to install a free tunnel so ElevenLabs can reach the backend on his laptop.

### Tunnel (Nov 13, late morning)

Robert approved installing `cloudflared` (Homebrew, free, no account). `npm run tunnel` opens a Cloudflare quick tunnel to the laptop, writes `PUBLIC_URL`, and re-runs `npm run agent` so the ElevenLabs tools and the call-start hook point at it.

**Verified from the public internet** (with a placeholder owner number, since Robert's is not set yet): `/health` 200; a tool call without the secret 401; as the owner 200; as a stranger 403; `/api/state` without the token 401; `/dashboard` 200. The ElevenLabs tools were confirmed pointing at the tunnel.

**Gotcha:** the first version polled the new hostname immediately, macOS cached "no such host," and every retry failed for minutes. The script now waits 15 seconds and checks through Cloudflare's resolver.

**Caveat:** the address changes every time the tunnel restarts, and when it is down the agent's tools fail. Run `npm start` and `npm run tunnel` side by side whenever the agent is in use.

Telnyx: Robert is partway through the SIP connection on the free tier. FQDN, credentials, inbound, and an outbound voice profile all accepted so far.

### Funds and demo sizing (Nov 13)

Robert funded the demo wallets from Circle's faucet: 40 USDC each to `agent` and `sender`, confirmed on chain. The faucet caps at about 40 per address, so the demo was scaled down about tenfold: 5 USDC auto-approve, 50 per transaction, 200 a day, keep 10 and sweep the rest. Demo amounts are now 1 (auto), 8 (ask), 60 (blocked), and a 20 USDC deposit that sweeps 15. Sweeps are rounded down to whole USDC so the agent never reads out gas fractions. Tests: 200 passing.

Still to build: a `reset-demo` script to recycle rehearsal funds, since the faucet won't cover many runs.

### First real phone call (Nov 13, about 11:30 AM CST)

**The outbound approval call works end to end on free accounts.**

- Robert verified his mobile in Telnyx and filled the Telnyx values in `.env.local`. `npm run phone` imported the Telnyx number (+1 807 695 9853, a Canadian area code; kept, since the trial allows one number per lifetime) into ElevenLabs as a SIP trunk number assigned to the agent.
- Server and tunnel started; the tunnel repointed the agent's tools and call-start hook.
- A simulated deposit via the dashboard API triggered the sweep rule: 40 USDC on hand, keep 10 plus 1 for gas, propose 29 to savings. Policy said CALL (`stream_source`).
- The call queue placed the call through ElevenLabs' SIP outbound endpoint and Telnyx. Robert's phone rang, he approved by voice with his PIN, the agent called `confirm_action`, and the backend sent 29 USDC to the savings wallet.
- **Verified on Arc testnet:** tx `0xfa621075f960fa9eee9c8610dc9ab48a695f88e8748eac247a5075048d286060`, status success, agent to savings, 29 USDC, fee about 0.0005 USDC. Balances after: agent 10.9995, savings 29, sender 40.

**Bug found and fixed on the way:** `npm run phone` appended to `.env.local` without checking for a trailing newline, which glued the new phone-number-id line onto the end of the SIP password line. The import itself used the correct password. Repaired the file; both scripts now write through `setEnvValue`, which is unit-tested for the no-trailing-newline case.

**Not yet tested:** an inbound call (owner dials the Telnyx number), a "no" or wrong-PIN path by phone, Mandarin by phone, and a real onchain deposit (rather than simulated) triggering the call.

### Inbound Mandarin call and new voices (Nov 13, midday)

**Inbound call by phone, in Mandarin, worked end to end** (181 s). Robert dialled the Telnyx number from his verified mobile. The agent switched to Mandarin on his first sentence, reported the balance, auto-sent 1 USDC, asked for yes + PIN on 8 USDC and waited through hesitation ("再等一下"), asked for an explicit yes after he gave the PIN first, disambiguated a misheard "6-60" by asking 六 or 六十, blocked 60 (per-transaction cap) and an unknown recipient, and ended the call itself. It never repeated the PIN. On chain: Alice's test wallet holds 9 USDC.

**Voice problem and fix.** The agent used one American English voice (Eric) for every language, which made Mandarin sound like an accent and English sound aggressive to Robert. Now English uses **Katie** (phone-assistant voice Robert found), and the Mandarin language preset uses **Amy**, a native Beijing Mandarin voice, on the `eleven_v4_turbo` model. A language preset can override the speech model, so Mandarin is not stuck on the flash model ElevenLabs forces for English-default agents. Picked by ear from generated samples (about 1,400 credits).

**Prompt:** amounts are rounded when spoken; Mandarin uses 密码, 爱丽丝, 储蓄 and measure words instead of mixed English. Agent behaviour tests re-run after the change: **27/27**. Backend unit tests: 204.

**Small issues seen, not yet addressed:** the agent was interrupted twice mid-sentence when the caller started speaking.

### Rehearsal reset (Nov 13, afternoon)

`npm run reset-demo` returns rehearsal money from the savings and alice wallets to the sender and tops the agent to 15 USDC plus 5 cents for gas, so the sweep read out on stage is the same every run. Planned by a pure, unit-tested function (212 tests total). The agent is paused during the moves because a top-up is itself a deposit and would otherwise trigger the sweep and ring the phone.

**Run live:** savings to sender 28.99, alice to sender 8.99, sender to agent 13.06. The server logged the top-up as `observed (sweep_blocked)` and placed no call. After: agent 15.06, sender 64.92.

### Dashboard sounds (Nov 13, afternoon)

Robert asked for confirmation sounds and a Hotline Bling intro. The song itself is copyrighted, so instead: original sounds generated with ElevenLabs sound effects, picked by ear from 11 samples. **Intro:** a 2.5 s late-night R&B synth sting with a soft phone ring. **Confirm:** a clean two-tone chime (Japanese-style chimes were also tried). **Blocked:** a soft low tone.

ElevenLabs phone agents can only play built-in preset sounds, so custom sounds play on the dashboard, which is on the projector during the demo. The decision of which sound to play is a pure function over two ledger refreshes, served to the page and unit-tested (224 tests). Verified in the browser: module loads, files decode, toggle persists, no console errors. Not verified while signed in, because reading the dashboard token was blocked for the session; Robert should check it once.

### QuickNode Stream (Nov 13, evening)

Built test-first (251 tests): a filter that runs on QuickNode and turns Arc logs into deposits, a webhook that verifies QuickNode's HMAC signature, and `npm run stream -- check/on/off/status/retarget`. The tunnel script repoints a running Stream automatically.

**Verified live:**
- `check` ran our filter on QuickNode's servers against the reset top-up block (72214961) and returned exactly that 13.06 USDC deposit. Network name `arc-testnet` confirmed.
- With the RPC poller **off** and the agent paused, a real 1 USDC deposit (tx `0xbefbf715…a458`, block 72263454) arrived from the Stream **about 0.8 s after its block**. Ledger records `via: stream`; the paused agent logged it without calling.
- Stream switched off afterwards; server back to Stream hook plus poller.

**Cost:** Streams bill per block; Arc testnet makes about 105,000 blocks a day. The account shows an 80M-credit allowance, so an always-on Stream is affordable for the hackathon, but it stays on-demand. Usage read 0 right after the test, probably reporting lag.

**Gotcha:** the free quick-tunnel address stopped resolving after several hours even though cloudflared was still running. Restarting the tunnel fixed it. A permanent address (free Cloudflare account, named tunnel) is worth setting up before demo day.

## Sat Nov 14 (day 2): unattended work while Robert was out

- **Self-healing tunnel.** `npm run tunnel` now checks its public address every minute and starts a fresh tunnel after three failures in a row, or right away if cloudflared exits; each new address repoints the agent and any running Stream. If the local server is the thing that is down, it reports that instead of churning addresses. Decision logic unit-tested. **Verified live:** killed cloudflared; a new tunnel came up, the agent was repointed, and the new address answered publicly.
- **Cut-offs.** Filler sounds (um, uh, 嗯, 呃 and similar) no longer interrupt the agent mid-sentence. Every word that can answer a question (yes, no, ok, 好, 对, 是, 可以, 确认, 不, 等一下...) is excluded, and a test enforces it. Pushed to the live agent and read back. Not yet heard on a real call.
- **README:** full "ElevenLabs products used" table (bounty requirement).
- **Submission drafts** in `demos/`: Devpost answers, 2–3 min video script, 5-minute pitch with fallback, 20 Q&A answers. Written by a background helper; spot-checked here.
- **Circle plan** in `docs/circle-plan.md`: developer-controlled wallets on `ARC-TESTNET` (Circle's own quickstart uses that chain). Needs Robert's free Circle account and a testnet API key.
- Tests: 258 passing.

