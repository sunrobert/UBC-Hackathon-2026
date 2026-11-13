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
