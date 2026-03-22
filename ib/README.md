# IB Analyst Skill

AI skill that thinks like a junior analyst at a bulge bracket bank.

## What It Does

Given a company or set of companies, produces institutional-quality research:

| Phase | Output |
|-------|--------|
| Company Profile | Business description, segments, ownership, recent news |
| Financial Analysis | Full P&L, balance sheet, cash flow metrics, trading multiples |
| Comparable Company Analysis | 4-6 peers, comps table, implied valuation from peer medians |
| Valuation Framework | Multiples-based, precedent transactions, DCF indicators |
| M&A Analysis | Deal activity, potential acquirers/targets, synergy logic |
| Risk Assessment | SWOT, moat, categorized risks, catalyst timeline |
| Investment Thesis | Bull / base / bear case |

## Usage

Drop `SKILL.md` into your AI agent's context (Claude, GPT, n8n, LangChain, etc.) and ask:

```
Research Apple, Tesla, and NVIDIA — full IB report
```

```
Run comps on Shopify
```

```
Screen fintech companies for M&A targets under $5B market cap
```

```
Prepare a one-pager on Stripe for a client meeting
```

## Design Principles

- **Frameworks over freestyle** — follows the same structure every analyst learns in training
- **Phases, not vibes** — 8 sequential phases, no skipping
- **Estimates are labeled** — never passes off guesses as facts
- **Audience-aware** — output adapts to profile, comps, valuation, or full report
- **Tool-agnostic** — works with any LLM, any orchestrator, any delivery method
