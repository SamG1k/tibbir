# TIBBIR site — notes for Claude

## About Sam (how to work with me)

- Self-taught, beginner-level dev. I build with AI help and deploy with Vercel. Don't assume I know the technical terms.
- I type fast and casual, with shorthand and lots of typos. Work out what I mean, don't correct my spelling. If something is genuinely unclear, ask one short question.
- Explain things in plain English. If I need to run a command or do something myself, give me the exact steps.
- Keep replies short and direct. No long explanations unless I ask.
- Be honest, no hype. If an idea is bad or won't work, tell me straight.
- I make the creative and content calls. You do them. When I correct something, just fix it, don't over-explain.
- If I push back, it usually means something was wrong or off-topic. Recheck it, don't argue in circles.

## Workflow

- Repo: `SamG1k/tibbir`. GitHub → Vercel. Anything pushed to `main` goes live automatically.
- Never push straight to `main` for site changes. Push to a test branch, Sam checks the Vercel preview, then merge to `main` only when Sam says so.
- Vercel preview: Vercel dashboard → tibbir project → Deployments → newest deployment for the branch → Visit (agentic page is `/`, TIBBIR is `/tibbir`).
- Commit with author name `SamG1k`.

## Files

- On branch `agentic-page` the pages are swapped: `index.html` = Agentic Economy homepage, `tibbir.html` = TIBBIR (served at `/tibbir` via `vercel.json` `cleanUrls`). The flip button top-right links to `/tibbir`. On `main` (until merged) `index.html` is still TIBBIR.
- TIBBIR page — single file, base64 images embedded.
- `CLAUDE.md` — this file. Excluded from deploys via `.vercelignore`.

## TIBBIR — project brief

TIBBIR is a crypto token connected to Ribbit Capital's portfolio ecosystem ("TIBBIR" = RIBBIT backwards). `index.html` is an info hub for the token: real events, documented breadcrumbs, sourced quotes. Tone is deliberate and sometimes mysterious (e.g. "The Video" section).

Contract address (bottom of page, `user-select: all`): `0xA4A2E2ca3fBfE21aed83471D28b6f65A233C6e00`

**Chain:** The site currently says Base / Virtuals Protocol — that is correct for when it was written (~3 months ago). About a month ago TIBBIR bridged to Robinhood Chain. This will be added later (not yet) — likely a new timeline event after "The World Is Flat" (Jul 2026), plus updates to hero, stats bar, Brian/Paul/Vlad rebel panels and the Stealth Launch event.

### Source of truth

The TIBBIR page (`tibbir.html` on `agentic-page`, `index.html` on `main`) is the source of truth. Before any task, read a stripped copy so you know the current content — it changes between tasks. If this file and the HTML disagree on content, trust the HTML. Don't read it raw (base64 images):

```bash
sed -E 's/data:image\/[a-zA-Z+]+;base64,[A-Za-z0-9+\/=]+/data:image;base64,STRIPPED/g' index.html > /tmp/tibbir-lite.html
```

Always edit the real `index.html`, never the lite copy.

### Design system

- Brutalist — thick dark borders, flat blocks, bold type. Inspired by ribbitcap.com
- Cream background `#f2efe6`, near-black text/borders `#1a1a14`, deep green highlights `#1a7a2e`
- Fonts: Space Grotesk (headlines/body), IBM Plex Mono (labels, hints, data)
- References: ribbitcap.com, gribbit.club, futurehumanism.co/ribbit-timeline

### Page structure (index.html)

1. Landing — one flipping coin (Ribbit front / TIBBIR back), "Click to enter the ribbit hole", green wipe
2. Nav + Hero
3. 01 Who Is Ribbit Capital (expandable) / 02 The Thesis (expandable)
4. Key Rebels — 3D flip cards: Vlad Tenev, Brian Armstrong, Alfonso de León, Michael Rihani, Rick Song, Paul Frambot. Hint: `hover to flip · click to expand`. Panel copy is placeholder.
5. Stats bar
6. 03 The Evidence — sticky draggable timeline, 17 events Jan 2024 → Jul 2026 (Tibbir Trust is an event, May 2024, with SEC LINK button)
7. Links (@ribbita2012), CA, footer

### Known issues in index.html (not fixed yet)

- Duplicate `<script>` block at the bottom; its timeline click handler references missing `#tlDetail` → console error on every timeline click.
- "Store + TEE" and "TEE Verified" (both Jan 2026) repeat the same Phala/TEE content.
- Section 01 says the ЯIBBIT rebrand was "early 2026"; the timeline says Oct 2025.
- Footer says © 2025.

### Hard rules

- **No fabricated content.** Never invent quotes, tweets or claims. Verbatim only, from sources. If unsure, flag it — don't guess.
- Images are base64-embedded in the HTML.
- Sam makes all creative/content decisions — execute them, don't elaborate.

### Working tips

- Use grep to find relevant CSS/HTML before editing; don't read the whole file.
- Card image crops: pixel-analysis edge detection; physical card edge ~22px beyond printed frame lines. Michael Rihani final crop: front `(144, 58, 733, 958)`, back `(796, 58, 1374, 959)`.
- Frame recolouring: thin-run method — dark pixel runs ≤6px wide within edge bands — recoloured to match each rebel's logo colour.

## Agentic Economy page (`index.html` on `agentic-page`)

A general page on the agentic economy, same colours/fonts as TIBBIR but its own look. Top bar: "AGENTIC ECONOMY" left, section links, green ЯIBBIT→TIBBIR flip button on the right linking to `/tibbir`.

Design went through several rounds; Sam's goal is **authentic, not AI-themed**. Current direction = editorial "field guide" / research report:
- Masthead (Vol. 01 · A field guide · Updated…), big headline, standfirst, "Compiled by SamG1k" byline
- Figures row with footnote markers
- Figures row (12) + status key. Status tags on items: Live / Preview / Announced / Forecast (as reported at the time)
- Organised in 5 pillars (per an outside review asking for broader coverage than payments/crypto):
- §1 The agents — two-column article, drop cap, pull quote
- §2 The infrastructure — isometric SVG stack (5 layers) + notes on MCP/AAIF and AWS AgentCore
- §3 Agents at work — case studies (Klarna, GitHub Copilot agent, Operator, Robinhood, ChatGPT checkout), spec-sheet layout
- §4 The economics — 4.1 pricing models table, 4.2 x402 sequence diagram, 4.3 money/forecasts + cases (Coinbase for Agents, Tempo, Virtuals)
- §5 Trust & governance — numbered open questions
- §6 How we got here — black band, compact two-column timeline with year tabs (2024/2025/2026/All) + "Next year" button
- §7 Who's building it — directory grouped: Agents & work / Infrastructure / Money
- §8 Glossary
- §9 Sources — numbered; footnotes `[n]` link to `#src-n`. Only cite pages actually read; cite the article that's *about* the fact, not a side mention
- (Companion note removed — TIBBIR is reached via the top-right button only)
- Avoid: tickers, hard shadows/hover lifts everywhere, eyebrow labels, identical card grids, accordions.

**Status:** layout done with placeholder text. Next step: fill content from Sam's links below. Every fact gets a footnote + source entry. Read each page directly (WebFetch); if a page can't be read, say so — don't fill from memory or search snippets. Show Sam a rundown before putting content on the page.

### Sam's source links (timeline content)

=== 2024 ===

- Jul 10, 2024 – Marc Andreessen sends $50K in BTC to AI agent Truth Terminal — https://decrypt.co/?p=239340
- Aug 2024 – Skyfire launches payment platform letting AI agents spend money autonomously — https://cointelegraph.com/news/coinbase-artificial-intelligence-ai-crypto-transactions-wallet-brian-armstrong
- Aug 30, 2024 – FIRST AI-to-AI crypto transaction (Brian Armstrong / Coinbase Developer Platform) — https://cointelegraph.com/news/coinbase-artificial-intelligence-ai-crypto-transactions-wallet-brian-armstrong
- Oct 11, 2024 – GOAT launches, first AI-agent-driven memecoin; Truth Terminal later becomes first AI crypto millionaire — https://medium.com/@0xai.dev/virtuals-protocol-luna-55b661df601e , https://www.theblock.co/amp/post/322002/marc-andreessen-funded-ai-bot-becomes-a-millionaire-after-fartcoin-holdings-rally
- Oct 16, 2024 – Luna = first agent launched via Virtuals IAO on Base
- Oct 26, 2024 – Luna = first AI agent to autonomously tip humans onchain — https://solanacompass.com/projects/luna
- Oct 2024 – Stripe acquires stablecoin firm Bridge for $1.1B (some sources say Feb 2025, likely close date) — https://ledgerinsights.com/stripe-acquires-crypto-wallet-privy
- Nov 8, 2024 – Coinbase launches AgentKit (wallets for AI agents) — https://www.coinbase.com/it/developer-platform/discover/launches/introducing-agentkit
- Nov 25, 2024 – Anthropic launches Model Context Protocol (MCP) — https://en.wikipedia.org/wiki/Model_Context_Protocol
- Nov 2024 – Ribbit "Hacking for Agentic Finance" hackathon (UNVERIFIED – find a source)

=== 2025 ===

- Mar 2025 – Ribbit Capital leads Crossmint's $23.6M round — https://www.crowdfundinsider.com/2025/03/237668-ribbit-capital-leads-23-6m-crossmint-funding-round/
- Apr 2025 – Google ships Agent2Agent (A2A) protocol — https://eco.com/support/en/articles/15192002
- Apr 29, 2025 – Mastercard launches Agent Pay
- Apr 30, 2025 – Visa launches Intelligent Commerce — https://www.digitalcommerce360.com/2025/05/06/visa-mastercard-ai-agentic-commerce/amp/
- May 6, 2025 – Coinbase launches x402 (stablecoin payments over HTTP), backed by AWS, Circle, Anthropic, Near — https://www.tradingview.com/news/cointelegraph:f25bb1df7094b:0-coinbase-x402-payments-protocol-to-make-ai-agents-more-autonomous/
- Jun 11, 2025 – Stripe acquires wallet provider Privy — https://www.theblock.co/post/357803/payment-giant-stripe-to-buy-crypto-wallet-firm-privy-report
- Aug 2025 – Ethereum Foundation releases ERC-8004 "Trustless Agents" (8 implementations in 24hrs) — https://blockeden.xyz/blog/2026/01/15/erc-8004-trustless-agents-ai-blockchain-coordination/
- Sep 16, 2025 – Google launches Agent Payments Protocol (AP2), 60+ partners, incl. A2A x402 extension — https://pymnts.com/news/artificial-intelligence/2025/google-debuts-agent-payments-protocol-bolster-ai-commerce
- Sep 24, 2025 – Cloudflare + Coinbase launch x402 Foundation — https://www.theblock.co/post/372064/cloudflare-coinbase-launch-x402-foundation
- Sep 29, 2025 – OpenAI launches Instant Checkout in ChatGPT + Agentic Commerce Protocol (with Stripe) — https://letsdatascience.com/news/openai-and-stripe-enable-agentic-commerce-in-chatgpt-965c7bf2

=== 2026 ===

- Jan 2026 – ERC-8004 heads to Ethereum mainnet (official launch event listed as Mar 17, 2026) — https://www.theblock.co/post/387345/ethereum-ai-agentic-economy-mainnet
- Feb 12, 2026 – Coinbase launches Agentic Wallets — https://cointelegraph.com/news/coinbase-launches-crypto-wallets-built-ai-agents
- Mar 18, 2026 – Tempo (Stripe + Paradigm) mainnet + Machine Payments Protocol — https://wyde.beehiiv.com/p/stripe-and-paradigm-launch-5-billion-tempo-blockchain-with-ai-agent-payment-protocol
- May 2026 – Robinhood lets third-party AI agents trade on its platform — https://qz.com/robinhood-ai-agent-trading-credit-card-070226
- 2026 – Mastercard Agent Pay for Machines (partners incl. Coinbase, Cloudflare, Stripe) — https://www.digitalcommerce360.com/2026/06/12/visa-openai-agent-led-payments/
- Now – x402 has processed 160M+ transactions, 90%+ on Base; Coinbase for Agents launches — https://thedefiant.io/coinbase-for-agents-ai-accounts-trade-pay-x402
