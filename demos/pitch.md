# Finals pitch (4 minutes, then 2 minutes of Q&A)

The guide changed on Nov 19: finalists get **4 minutes to present and 2 minutes for Q&A** (it was 5).

**Hook:** "Every AI wallet demo shows the agent spending. Ours calls you first."

**The moment to protect:** the phone ringing on stage. Everything before it sets it up; everything after it explains why it matters. If time runs short, cut from the explanation, never from the call.

## Minute by minute

The two calls are the same as in the demo video, in the same order, so there is one flow to rehearse. The talking around them is what got shorter. Planned end: 3:50, with 10 seconds spare.

| Time | What happens | Words |
|---|---|---|
| 0:00–0:20 | The problem | "AI agents are getting wallets. They pay for APIs, data, compute. But how does the human say no? A notification gets swiped. A dashboard has to be open. A phone call reaches you anywhere, in your language." |
| 0:20–0:30 | The idea | "Hotline is a wallet agent on Arc. You call it to spend. When it wants to move money you didn't ask for, it calls you. Nothing moves until you say yes." |
| 0:30–1:40 | Live inbound call, phone on speaker, dashboard on the projector | Say nothing over the agent. Send 8 to Alice: read-back, yes + PIN, chime. Send 60: refused, names the cap. "What's Ethereum at?": the agent answers and says the lookup cost a cent, paid on Arc (dashboard shows the x402 row). One 1 USDC send in Mandarin: Amy answers in Mandarin. Hang up, then one line: "Every decision names its rule. Auto, ask first, blocked." |
| 1:40–2:55 | **The phone rings** | "Now money arrives on its own." Run the 20 USDC deposit. QuickNode Stream label appears. Phone rings on stage. Agent offers to sweep the extra to savings. Say yes with the PIN. Show the explorer. "Nothing moved until I said yes." |
| 2:55–3:25 | Why it's real | "The limits are code, checked again at approval time. The agent can't be talked past a cap, can't pay an address it wasn't given, and can't be told by a 'developer' to skip the PIN. We tested that against the live agent: 29 of 29, in ten languages. And when it needs data, it pays for it itself over x402, a cent a lookup, inside the same limits." |
| 3:25–3:50 | Who it's for, and close | "It's for people who don't live in crypto apps, people who'd rather speak Mandarin or Spanish than read English menus, and anyone who wants an agent with a budget and a human veto. Any phone, any language, no app. Hotline: an AI wallet agent that calls you before it spends." |

## If it runs long

Check the clock twice. The deposit must be running by **1:45**; the phone call must be over by **3:00**.

1. **Behind at 1:15 (still on the inbound call):** skip the Mandarin send and hang up. The sweep the agent offers will then be 16 USDC, not 15, because one less dollar was spent. The agent says the amount itself, so nothing else changes.
2. **Behind at 3:00:** drop "Why it's real" to its first two sentences.
3. **Behind at 3:30:** say only the last two sentences of the close.

Never cut the ring. Never talk over the agent to save time; it makes the call slower.

## Q&A (2 minutes)

Two minutes is two or three questions. Answer in 20 seconds each, then stop. Full answers are in `qa-prep.md`; the ones most likely to come up on stage:

- "Caller ID can be spoofed" and "you say the PIN out loud" (1, 2)
- "Is the x402 real if you run the seller yourself?" (14b)
- "You don't use Circle Wallets or CCTP" (16): say not yet, and what it would replace.
- "Why a phone call instead of a notification?" (7)

## Fallback if the live call fails

Decide in five seconds; don't debug on stage.

1. **Phone doesn't ring within 15 seconds:** "The network here is shy, so here's the same call from this morning." Play the backup clip of the outbound call (keep it cued in a tab).
2. **Inbound call won't connect:** use **Call Hotline** on the dashboard and talk through the laptop. Same agent, same tools, same rules.
3. **Tunnel or Wi-Fi is down:** switch the laptop to the phone hotspot before the pitch starts, not during. If still down, play the full demo video.

## Stage setup

- Laptop on a phone hotspot, not venue Wi-Fi. Tunnel restarted after connecting.
- `npm run reset-demo`, then `npm run stream -- on`, ten minutes before.
- Dashboard signed in, Sound on, projector mirrored.
- Phone fully charged, ringer loud, Do Not Disturb off, held near the mic.
- Backup video downloaded locally, not streamed.
- Speak the PIN, then rotate it after the event.
