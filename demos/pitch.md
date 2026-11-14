# Finals pitch (5 minutes, then Q&A)

**Hook:** "Every AI wallet demo shows the agent spending. Ours calls you first."

**The moment to protect:** the phone ringing on stage. Everything before it sets it up; everything after it explains why it matters. If time runs short, cut from the explanation, never from the call.

## Minute by minute

| Time | What happens | Words |
|---|---|---|
| 0:00–0:30 | The problem | "AI agents are getting wallets: they pay for APIs, data, compute. The question nobody's demo answers is: how does the human say no? An app notification gets swiped. A dashboard has to be open. A phone call interrupts you anywhere, on any phone, in your language." |
| 0:30–0:45 | The idea | "Hotline is a wallet agent on Arc. You call it to spend. And when it wants to move money you didn't ask for, it calls you, and nothing moves until you say yes." |
| 0:45–2:00 | Live inbound call, phone on speaker, dashboard on the projector | Send 8 to Alice: read-back, yes + PIN, chime. Send 60: refused, names the cap. "What's Ethereum at?": the agent answers and says the lookup cost a cent, paid on Arc (dashboard shows the x402 row). Switch to Mandarin for a 1 USDC send: Amy answers in Mandarin. "Every one of those decisions names its rule. Auto, ask first, blocked." |
| 2:00–3:15 | **The phone rings** | "Now money arrives on its own." Run the 20 USDC deposit. QuickNode Stream label appears. Phone rings on stage. Agent offers to sweep 15 to savings. Say yes with the PIN. Show the explorer. "Nothing moved until I said yes." |
| 3:15–4:00 | Why it's real | "The limits are code, re-checked at approval time. The agent can't be talked past a cap, can't pay an address it wasn't given, and can't be told by a 'developer' to skip the PIN. We tested that against the live agent: 29 of 29, in ten languages. And when it needs data, it pays for it itself over x402, a cent a lookup, inside the same limits." |
| 4:00–4:40 | Who it's for | "People who don't live in crypto apps. Older users. People who'd rather speak Mandarin, Spanish, or Hindi than read English menus. And anyone who wants an AI agent with a budget, but a human veto." |
| 4:40–5:00 | Close | "Any phone, any language, no app. Hotline: an AI wallet agent that calls you before it spends." |

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
