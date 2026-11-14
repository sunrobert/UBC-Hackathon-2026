# Circle wallets plan

Researched Nov 14 from Circle's developer docs. Goal: close the gap the Circle judge (Best use of Arc) and the Agentic Payments track will notice. Today the agent's wallet is a private key held by the backend. No Circle product is used beyond USDC and Arc itself.

## Recommendation: Circle Developer-Controlled Wallets for the agent

| Option | Fit | Why |
|---|---|---|
| **Developer-Controlled Wallets (DCW)** | **Recommended** | Server-side SDK (`@circle-fin/developer-controlled-wallets`). Circle's own quickstart uses **`ARC-TESTNET`** as the example chain, so this path is first-class. Keys are MPC-held by Circle under our entity secret; the backend never sees a private key. |
| Agent Wallets (Circle CLI) | Not for the backend | User-controlled MPC with email OTP, operated through the `circle` CLI. Built for an AI coding agent driving a terminal, not a server. Their spending policies **only enforce on mainnet**, per Circle's docs. |
| CCTP / Gateway / App Kits | Later, optional | Would add a cross-chain story (e.g. USDC arriving from Base Sepolia). Bigger scope, less central. |

**What changes for the pitch:** "The agent's keys never touch our server. Circle holds them in MPC, and every send still has to pass our policy engine and, above the limit, your voice."

## Robert's part (about 15 minutes)

1. Create a free Circle developer account at https://console.circle.com. Stop and tell me if it asks for a card.
2. Create a **testnet** API key (Console, API & Client Keys). Add to `hotline/.env.local`: `CIRCLE_API_KEY=...`
3. Nothing else: I generate and register the entity secret with the SDK, and the script writes it to `.env.local`.

## My part (about half a day)

1. **Spike, one hour.** Throwaway script: register entity secret, create a wallet set and an EOA wallet on `ARC-TESTNET`, fund it from the sender wallet, send 0.1 USDC back with `createTransaction`, poll `getTransaction` to `COMPLETE`, and confirm the tx on the Arc explorer. Measure how long until a tx hash exists, since the voice agent's tools must answer within about 15 seconds.
2. **`src/wallet/circle.ts`** implementing the existing `Wallet` interface: `send()` calls `createTransaction` (USDC ERC-20 interface `0x3600…0000`, 6 decimals, fee level MEDIUM) and returns once Circle reports a tx hash; `waitForReceipt()` polls to `COMPLETE` / `FAILED` / `CANCELLED` / `DENIED`; `balance()` keeps reading the native balance over RPC. Test-first against a fake Circle client.
3. **Config switch** `WALLET=circle|local`, so the old key path stays as a fallback for demo day.
4. **Knock-on changes:** the agent's address changes, so: move funds to the new wallet, re-run `npm run stream -- on` (the filter has the address baked in), teach `reset-demo` to send from the agent through Circle, and update the README's addresses and Arc section.
5. Re-run the live checks: an AUTO send by voice, an approval call, and the Stream deposit path.

## Risks

- **Async sends.** Circle returns a transaction id first and the hash later. If the hash takes more than a few seconds, the agent says "sending now" and the status tool reports it. The engine already works that way.
- **Two Transfer logs.** ERC-20 sends on Arc log from both the token contract and the system emitter. The Stream filter and poller already count only the system emitter.
- **Spending policies don't enforce on testnet**, so the README keeps saying the limits live in our backend. That is also the stronger story: Circle custody plus our policy engine plus your voice.
- **Demo-day fallback:** `WALLET=local` restores today's wallet with no code change.
