> Source: official "Hackathon Guide UBC 26" Google Doc, re-captured 2026-11-13 and re-checked 2026-11-19 (finalist pitch cut from 5 minutes to 4; two perk notes added). Changes since the Nov 5 copy: start time moved to Thu Nov 12 6 PM CST, ElevenLabs Discord redemption steps, and a sponsor perks section (Cursor/Grok, ElevenLabs, QuickNode credits).


## Welcome to the University Blockchain Conference hackathon! 

## This one-week hackathon is designed to provide new and experienced builders from all backgrounds the opportunity to research, build, and pitch their wildest crypto ideas to a panel of industry leaders and experts. Whether you're a seasoned developer or just getting started, there’s a place for you here.

Total prize pool: $22,000+ in cash, plus sponsor perks. See Hackathon Prizes below for how it breaks down.

Submission link: ubc-hackathon-2026.devpost.com

Workshop schedule: 

Telegram Link: https://t.me/+Q0hy2P7nbIk2YWIx 

## Event Structure

Hackers MUST submit their projects to EXACTLY 1 of the 3 main tracks

Participants may also choose to submit to as many bounties as they would like to AFTER they have chosen their primary track

Within your main track, you can also compete for ONE chain award: Best use of Solana or Best use of Arc (never both).

Every submission is automatically eligible for Official UBC 2026 Hackathon Winner (1st/2nd/3rd), which stacks with any other prize. See Hackathon Prizes for the full stacking rules.

Main tracks (required, pick exactly one)

- Agentic Payments and AI: AI agents that can safely hold, send, and receive stablecoins to pay for APIs, data, and compute.

- DeFi and Onchain Applications: New financial primitives and smart-contract apps: exchanges, lending, yield, derivatives, and payment rails.

- Consumer Applications: Everyday apps (payments, social, gaming, creator tools, loyalty) where the crypto is invisible to the user.

Chain awards (optional, pick one, judged within your main track)

- Best use of Solana: The best project built on Solana in each main track.

- Best use of Arc: The best project built on Arc, Circle’s stablecoin-focused Layer-1, in each main track.

Bounties (optional, enter as many as you qualify for)

- Gemini Prediction Markets: Projects built on Gemini’s prediction market data and trading APIs.

- ElevenLabs: Projects where voice or audio (text-to-speech, voice agents, sound, music) is central to the experience.

- QuickNode Streams: Projects that use real-time or historical onchain data from QuickNode Streams.

- Grok Bot: Projects where Grok Bot on X does real work, like automating workflows or acting on onchain activity.

### Hackathon Timeline

- Kickoff Call: Thursday, November 12 @ 6:00 PM CST

- Hackathon Start: Thursday, November 12 at 6:00 PM CST

- Note that Devpost starts on Friday 12:00 PM CST, ignore this. In-person hackathons on Devpost have a max hack length of 1 week.

- Submission Deadline: Friday, November 20 at 12:00 PM CST

- Workshops and Office Hours: Solana and Circle will host virtual workshops throughout Nov 16th - Nov 19th. All bounty sponsors will also host workshops/office hours to help explain what they are looking for in submissions 

- Judging: Saturday, November 21 (in-person review and demos)

- Final Presentations: Saturday, November 21 during UBC closing ceremony

### Pitch & Final Presentations

- Up to 13 teams will be selected to pitch in person to judges on Saturday, Nov 21st: 3 teams from each of the 3 main tracks (the top contender for Track Winner, Best use of Solana, and Best use of Arc), the top 3 contenders for Official UBC 2026 Hackathon Winner, and the 1st place Gemini bounty team

- Finalists will be notified by Friday, Nov 20 at 11:59 PM CST

- Each finalist team will have 4 minutes to present and 2 minutes for Q&A

- The judging panel will deliberate and determine winners immediately following all finalist pitches 

- Winners will be announced live at the UBC closing ceremony

## Hackathon Prizes

Total prize pool: $22,000+ in cash, plus sponsor perks

How prizes work

- Pick ONE main track (required). Each track has a $2,000 Track Winner.

- Pick ONE chain award (optional): Best use of Solana or Best use of Arc, judged within your main track. You cannot enter both.

- Enter any bounties (optional). Enter as many as your project qualifies for.

Every submission is also automatically in the running for the overall Official UBC 2026 Hackathon Winner. All prizes stack except Best use of Solana and Best use of Arc.

| Prize | Award | Who is eligible |
| Overall |  |  |
| Official UBC 2026 Hackathon Winner | 1st: $2,500 + 3 months of ElevenLabs Pro per member 2nd: $1,000 3rd: $500 | Every submission, automatically |
| Main tracks (one winner per track) |  |  |
| Track Winner | $2,000 per track (3 winners) | Every team, in the main track it chose |
| Best use of Solana | $1,500 per track (3 winners) | Projects built on Solana that select Solana as their chain award |
| Best use of Arc | $1,000 per track (3 winners) | Projects built on Arc that select Arc as their chain award |
| Sponsor bounties (judged by the sponsor and a UBC team representative) |  |  |
| Gemini Prediction Markets | 1st: $2,500 / 2nd: $1,000 / 3rd: $500 | Teams that opt in on Devpost |
| QuickNode Streams | $500 | Teams that opt in on Devpost |
| ElevenLabs | 3 months of ElevenLabs Scale per member | Teams that opt in on Devpost |
| Grok Bot | Mechanical keyboard per member + Grok Bot swag | Teams that opt in on Devpost |
| Participation |  |  |
| Participation prize | 1 month of ElevenLabs Creator, a $49/mo QuickNode plan*, and X Premium (Cursor, Grok, X, and more)* | Any team with a complete, working submission that meets all What to Submit requirements, at the judges’ discretion |
*QuickNode and X Premium perks are available for up to 300 hackathon participants.

Example: a DeFi project built on Solana that uses QuickNode Streams could stack DeFi Track Winner for $2,000, Best use of Solana for $1,500, the QuickNode bounty for $500, and an Official Winner place.

On Devpost: select your main track, your chain award (Solana, Arc, or None), and your bounties, then opt in to the matching prizes.

## Main Track: Agentic Payments and AI

### Overview

AI agents are starting to act on their own: calling APIs, buying data, and paying for compute. This track rewards projects that let agents hold, send, and receive stablecoins safely, and that build the rails for machine-to-machine commerce. It is recommended to use x402, Circle Agent Wallets or Nanopayments, or Solana Agent Kit.

### Objectives

Projects should aim to:

- Build agents that pay for APIs, data, or compute on a per-request basis (e.g., using the x402 payment protocol)

- Add spending controls and guardrails such as budgets, allowlists, and human approval for large transactions

- Create marketplaces or services that agents can discover and pay for in USDC

- Build tools that let LLMs read from and act on the blockchain safely

### Technical Requirements

Projects must:

- Enable agents to execute onchain transactions or read the blockchain on any chain (devnet/testnet is fine)

- Document the agent’s decision loop and the safety limits you put in place

### Prizes

Track Winner: $2,000. Projects in this track can also compete for one chain award: Best use of Solana ($1,500) or Best use of Arc ($1,000).

## Main Track: DeFi and Onchain Applications

### Overview

This track is for new financial primitives and onchain applications: exchanges, lending, yield, derivatives, payment rails, and other apps that rely on smart contracts. We’re looking for projects that are composable, capital-efficient, and safe to use.

### Objectives

Projects should aim to:

- Design new DeFi primitives or meaningfully improve existing ones (capital efficiency, risk management, liquidity)

- Compose with existing protocols rather than rebuilding them from scratch

- Make DeFi safer and more accessible through risk dashboards, simplified UX, or better onboarding

- Enable cross-chain flows, for example moving USDC between chains with CCTP

### Technical Requirements

Projects must:

- Interact with smart contracts on any chain (devnet/testnet is fine); deploying your own is optional 

- Explain the economic design and risk assumptions in your README

- Include the address of any program or contract your project deploys or uses

### Prizes

Track Winner: $2,000. Projects in this track can also compete for one chain award: Best use of Solana ($1,500) or Best use of Arc ($1,000).

## Main Track: Consumer Applications

### Overview

The next wave of crypto users won’t care that they’re using a blockchain. This track rewards consumer apps (payments, social, gaming, creator tools, loyalty, and more) where the crypto is invisible and the experience is as smooth as any mainstream app.

### Objectives

Projects should aim to:

- Onboard and retain retail users by abstracting the complications of crypto, including bridging, gas fees, and seed phrases

- Build something people would want to use every day, not just once

- Be intentional and thoughtful about their design and user experience

### Technical Requirements

Projects must:

- Interact with the blockchain in some way

- Provide a working, user-facing frontend (web or mobile)

### Prizes

Track Winner: $2,000. Projects in this track can also compete for one chain award: Best use of Solana ($1,500) or Best use of Arc ($1,000).

## Award: Best use of Solana (within each main track)

### Overview

Solana is a high-performance blockchain with fast finality and low fees, making it a strong fit for payments, DeFi, consumer apps, and AI agents. This award goes to the best Solana project in each main track. You compete only against other Solana projects in your own main track. A team can win its Track Winner plus Best use of Solana, but can never win both Best use of Solana and Best use of Arc. Select Best use of Solana as your chain award on Devpost.

### Objectives

Projects should aim to:

- Use Anchor or native Rust for any programs you write, and take advantage of Solana’s speed and low fees

- Use Solana-native primitives such as SPL tokens, Token Extensions, or Solana Pay

- Integrate with existing Solana protocols and tooling rather than rebuilding from scratch

- Deliver a smooth end-user experience with Solana wallets

### Technical Requirements

Projects must:

- Build your core onchain functionality on Solana (devnet is fine); deploying new programs is optional, and using existing ones counts

- Include the program ID(s) your project deploys or uses and explain in your README how your project uses Solana

- Must also be submitted to a main track and meet its requirements

### Prizes

$1,500 to the best Solana project in each main track (3 winners total).

## Award: Best use of Arc (within each main track)

### Overview

Arc is Circle’s EVM-compatible Layer-1 blockchain built for stablecoin finance, using USDC as its native gas token. This award goes to the best Arc project in each main track. You compete only against other Arc projects in your own main track. A team can win its Track Winner plus Best use of Arc, but can never win both Best use of Arc and Best use of Solana. Select Best use of Arc as your chain award on Devpost.

### Objectives

Projects should aim to:

- Build payment, treasury, or FX apps that use USDC as gas for predictable fees

- Use standard EVM tooling such as Hardhat or Foundry for any contracts you deploy

- Combine Arc with Circle tools like Wallets, CCTP, Gateway, or Paymaster

- Create user experiences where fees and balances are simple and stable

### Technical Requirements

Projects must:

- Build your core onchain functionality on Arc (testnet is fine); deploying new contracts is optional, and using existing ones counts

- Include the contract address(es) your project deploys or uses and explain in your README how your project uses Arc

- Must also be submitted to a main track and meet its requirements

### Prizes

$1,000 to the best Arc project in each main track (3 winners total).

## Bounty: Best Project built with ElevenLabs

### Overview

ElevenLabs provides AI audio tools including text-to-speech, speech-to-text, conversational voice agents, sound effects, and music generation. This bounty rewards projects where voice or audio is central to the experience.

### Objectives

Projects should aim to:

- Build voice interfaces for crypto, such as a wallet or trading assistant you can talk to

- Use ElevenLabs Agents to create conversational agents that can take onchain actions

- Improve accessibility by making apps fully usable by voice

- Use generated narration, music, or sound effects in games, content, or creator tools

### Technical Requirements

Projects must:

- Use the ElevenLabs API or SDK (text-to-speech, speech-to-text, Agents, etc.) as a core feature, not an add-on

- Your demo video must show the ElevenLabs integration in action, with audio

- Describe in your README which ElevenLabs products you used and how

- Must also be submitted to a main track and meet its requirements

### Prizes

Each member of the winning team receives 3 months of the ElevenLabs Scale tier.

## Bounty: Best Project built with Gemini Prediction Markets

### Overview

Gemini offers prediction markets where users trade on the outcomes of real-world events. Its developer platform exposes prediction market data and trading through APIs. This bounty rewards projects that build useful tools and experiences on top of Gemini Prediction Markets.

### Objectives

Projects should aim to:

- Build analytics and visualizations that track how market odds move over time

- Create trading tools, bots, or AI agents that act on prediction market data

- Bring prediction market data into other apps, such as news, social, or onchain applications

- Improve how users discover and understand markets

### Technical Requirements

Projects must:

- Use the Gemini Prediction Markets API (market data and/or trading endpoints)

- Must also be submitted to a main track and meet its requirements

### Prizes

Three winners: 1st place $2,500, 2nd place $1,000, 3rd place $500.

## Bounty: Best Use of QuickNode Streams

### Overview

QuickNode Streams is a real-time and historical blockchain data pipeline that pushes onchain data (blocks, transactions, logs, and receipts) directly to your destination of choice, such as webhooks, PostgreSQL, Snowflake, or S3, with guaranteed, in-order delivery and no polling. This bounty rewards projects that use Streams to power responsive, data-driven crypto experiences.

### Objectives

Projects should aim to:

- Build real-time apps that react to onchain events, such as wallet alerts, whale or trade trackers, or live dashboards

- Use Streams filters to transform raw chain data into exactly the data your app needs

- Backfill historical data to power analytics, custom indexers, leaderboards, or risk monitoring

- Trigger automated actions (notifications, bots, or offchain workflows) from onchain activity

### Technical Requirements

Projects must:

- Use QuickNode Streams as a core data source in your project

- Configure at least one Stream with a filter and a destination (e.g., webhook or database)

- Explain in your README how your Stream is configured (network, dataset, filter logic, and destination) and why

### Prizes

$500 to the winning team.

## Bounty: Best Use of Grok Bot

### Overview

Grok Bot is xAI’s assistant built into X, capable of running tasks, automating workflows, and acting on information in real time. This bounty rewards projects where Grok Bot does real work: automating a workflow, running agent tasks, watching onchain activity, or helping users act on their own. The more central Grok Bot is to your project, the better. X Premium (Cursor, Grok, X, and more) is available for up to 300 participants; redemption links will be shared before the hackathon.

### Objectives

Projects should aim to:

- Use Grok Bot to do real work, such as automating a workflow or running agent tasks

- Use Grok Bot to watch onchain activity and surface or act on what it finds

- Help users take action on their own, not just get answers

- Make Grok Bot central to the experience, not a novelty or add-on

### Technical Requirements

Projects must:

- Use Grok Bot as a core part of the project

- Include a Grok Bot chat export showing how you built or used it

- Include a short README (3–4 sentences) explaining Grok Bot’s role in your project

- Be working and technically sound

- Must also be submitted to a main track and meet its requirements

### Prizes

Each member of the winning team receives a mechanical keyboard, plus Grok Bot swag.

## General Guidelines

Team Composition

- Teams of 1-4 members recommended

- Solo builders welcome

- Cross-functional teams encouraged (engineering, design, product)

What to Submit

- Project name, short description, and all team members

- Your main track (one only), chain award (Best use of Solana, Best use of Arc, or None), and every bounty you're applying for

- Written answers to: What did you build? What problem does it solve? How does it work? What makes it unique? What would you build next?

- Technologies/sponsor tools used

- A link to the public GitHub repository, with source code and setup instructions, of the prototype that you made during this hackathon

- A working demo or deployed application

- Link to Google Drive or YouTube for your 2–3 minute demo video showing the product in action. Ensure the video is accessible to the judges

- Technical documentation/architecture overview included in a README file in the shared GitHub repo

- Any track-specific requirements listed earlier in the guide (e.g., contract address, track-specific questions, etc.)

## Judging Process

- Initial Screening: Review of all submissions

- Shortlisting: Selection of up to 13 finalists: 3 teams from each of the 3 main tracks (the top contender for Track Winner, Best use of Solana, and Best use of Arc), the top 3 contenders for Official UBC 2026 Hackathon Winner, and the 1st place Gemini bounty team

- Bounty Judging: Bounty winners are selected by each sponsor and a UBC team representative based on project submissions

- Live Demos: Finalists present to judges on stage (4 min + 2 min Q&A)

- Deliberation: Judges finalize rankings and award winners. Within each main track, a UBC team representative chooses the Track Winner, a Solana representative chooses Best use of Solana, and an Arc representative chooses Best use of Arc. The UBC team chooses 1st, 2nd, and 3rd place for Official UBC 2026 Hackathon Winner

- Announcements: Winners revealed at the closing ceremony

Judges’ decisions are final. Teams must be present in person for the closing ceremony to qualify for any prize, including both main track and bounty prizes.

## What We’re Looking For Across All Categories

- Technical ExecutionFunctionality, technical depth, and effective use of blockchain infrastructure.

- Product & UXClear problem, intuitive experience, and quality of the product.

- InnovationOriginality and creativity of the idea.

- Impact & PotentialReal-world usefulness, adoption potential, and ability to become a viable product.

- DemoQuality of the live product demonstration and ability to clearly communicate the project.

## Resources and Support

For Solana Builders:

- Solana Developer Docs

- Solana Cookbook

- Anchor Framework

For Circle / EVM Builders:

- Circle Developer Docs

- Arc Docs

- CCTP (Cross-Chain Transfer Protocol)

- Circle Wallets

- USDC Contract Addresses

- Circle Testnet Faucet

- Ethereum Developers

- Hardhat

- Foundry

For Gemini Prediction Markets Builders:

- Gemini Developer Platform

- Prediction Markets Overview

- Prediction Markets Getting Started

- Market Data

- Trading Quickstart

For ElevenLabs Builders:

- ElevenLabs Docs

- Developer Quickstart

- API Reference

- ElevenLabs Agents

- Libraries & SDKs

Participants can claim their free ElevenLabs access through Discord system:

1. Join the Discord server: https://discord.com/invite/VnBvbbcdEC

2. Gain access to the #│coupon-codes channel

3. Click “Start Redemption”

4. Select the event and fill out the form using the email used for registration

5. The bot sends the unique coupon code

Video Tutorial: https://youtu.be/S143_JtCtV8

For QuickNode Streams Builders:

- Streams Quickstart

- Using Filters with Streams

- Backfilling Historical Data

- Streams REST API Reference

- How to Stream Solana Program Data

General Support:

- UBC Hackathon Telegram

- Workshops and sponsor Q&A sessions

FAQ

Can I work on a pre-existing project?	No. Projects must be substantially built during the hackathon.

Can I submit to multiple main tracks?	No. Each project can only be submitted to one main track. You can still submit the same project to as many bounties as you like.

Do I need a team?	No, solo builders are welcome.

Can I use AI tools?	Yes, you are encouraged to use AI tools. Your project still needs to be a working, substantive build that meets the “What to Submit” requirements to be eligible for any prize.

How do I qualify for the participation prize?

Your team needs a complete submission that meets every item under “What to Submit”: a working prototype in a GitHub repo, a README with technical documentation, and a 2–3 minute demo video. We won’t award the participation prize to submissions that are incomplete, don’t run, or show minimal effort. All prizes, including the participation prize, are awarded at the judges’ discretion.

Who owns my project?	You retain all rights to your code and intellectual property.

## Let’s Hack

That’s everything the UBC team has for y’all!Pick your track, form your team (or go solo), and start building. We can’t wait to see what you create.

Questions? Ask in the Telegram, join office hours, or speak to an organizer.

- Nathan, on behalf of the UBC 26 Hackathon Organizer Committee

## Redeeming Sponsor Perks & Credits

### Cursor (Grok Pro Perk)

- Log in to Grok first, then visit the Cursor / Grok referral link to claim your first month for $0 (250 redemptions available).
- Must be with an account with no prior subscription

### ElevenLabs

- Join the Discord server, head to the #│coupon-codes channel, click "Start Redemption", and fill out the form. You can also watch the video tutorial for guidance.
- Coupon codes have been loaded and are ready under the "University Blockchain Conference (UBC Hackathon)" event name!

### QuickNode

- Visit the QuickNode Credits Guide to claim your credits.
