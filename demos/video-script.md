# Demo video script (2:30 target, 3:00 hard limit)

The video is what gets Hotline into finals. Judges screen submissions from Devpost, and each sponsor judges mostly from this video. Every judge needs one moment that is unmistakably theirs:

| Judge | Must see and hear |
|---|---|
| Track (UBC) | AUTO, CALL with yes + PIN, and BLOCK naming its rule |
| ElevenLabs | The voice working **with audio**, the switch to Mandarin, the outbound call |
| QuickNode | The deposit appearing on the dashboard labelled **via QuickNode Stream** |
| Arc / Circle | The transaction on the Arc testnet explorer |
| Track (objective 1) | The agent paying per request over x402: the price lookup and its ledger row |

## Shots

- **A:** Screen recording of the dashboard (balance, pending, ledger), sound on.
- **B:** Phone on camera, speaker on, screen visible when it rings.
- **C:** Terminal, large font, for the one deposit command.
- **D:** Arc testnet explorer tab for the final transaction.

Record A and B at the same time if possible (phone propped beside the laptop). Otherwise record the call audio from the phone and cut to the dashboard.

## Order matters

Do the inbound call **before** the deposit. With the agent reset to 15 USDC: sends of 1 and 8 leave about 6, the 20 USDC deposit brings it to about 26, and the sweep offered is **15**. Depositing first would offer 24 instead.

## Script

| Time | Shot | Narration / on screen |
|---|---|---|
| 0:00 | A | **Narration:** "AI agents are getting wallets. The hard part isn't spending. It's asking first. Hotline is a wallet agent on Arc that calls you before it spends." |
| 0:10 | B | Dial the agent. It answers in Katie's voice: "Hotline here. What do you need?" |
| 0:15 | B + A | **You:** "Send 8 USDC to Alice." **Agent** reads back the amount and recipient, says it's over the 5 USDC auto-approve limit, asks for yes or no and the PIN. **You:** "Yes. PIN [PIN]." **Agent:** "Approved. Sending now." Dashboard: row turns to sent, chime plays. |
| 0:45 | B + A | **You:** "Send 60 to Alice." **Agent:** refuses, names the 50 USDC per-transaction cap, says nothing was sent. Dashboard: blocked row, soft tone. |
| 0:55 | B + A | **You:** "What's Ethereum at?" **Agent:** gives the price and says the lookup cost one cent, paid on Arc. Dashboard: an **x402 payment** row appears. |
| 1:03 | B | **You, in Mandarin:** "再给爱丽丝转一个 USDC。" **Agent switches to Amy's Mandarin voice** and confirms the send. **You:** "谢谢,再见。" Agent hangs up. |
| 1:18 | A | **Narration:** "Every decision names its rule: auto, ask first, or blocked. Those limits live in code and are re-checked at approval time." Pan the ledger. |
| 1:28 | C | **Narration:** "Now money arrives on its own." Run `npm run demo:deposit -- 20`. |
| 1:33 | A | The deposit row appears with **via QuickNode Stream**; the intro sting plays. **Narration:** "A QuickNode Stream sees the deposit in under a second. My standing rule says keep 10, sweep the rest." |
| 1:43 | B | Phone rings. **Agent:** "This is Hotline. Money just arrived in your wallet, and your rule moves the extra to savings. I'd send 15 U S D C to savings. Yes or no, and your PIN?" **You:** "Yes. [PIN]." **Agent:** confirms. |
| 2:13 | D | Explorer: the 15 USDC transfer, agent wallet to savings, success. **Narration:** "Real USDC on Arc testnet. Nothing moved until I said yes." |
| 2:23 | A | **Narration:** "Any phone, any language, no app. An AI agent with a budget, and a human veto. That's Hotline." End card: name, repo URL, track and sponsors. |

## Before recording

1. `npm start` in one terminal, `npm run tunnel` in another, from the `hotline` folder. Wait for "Ready."
2. `npm run reset-demo` so the agent holds 15 USDC.
3. `npm run stream -- on`.
4. Open the dashboard, sign in, **Sound on**.
5. Phone: volume up, Do Not Disturb off for the agent's number, speaker on.
6. Quiet room. Close notifications on the laptop.
7. One dry run of the deposit beat, then `npm run reset-demo` again.

## After recording

1. `npm run stream -- off`.
2. **The PIN is spoken on camera.** Either bleep it in editing, or rotate it: change `OWNER_PIN` in `.env.local` to four new digits (avoid 1 and 4, which are easy to mishear), then restart `npm start`.
3. Upload to YouTube (unlisted) or Google Drive with "anyone with the link can view." Open the link in a private window to confirm judges can watch it.

## Cost per take

About 4 minutes of calls: roughly 2,300 ElevenLabs credits and 8 cents of Telnyx trial credit. Budget three takes.
