# IB Analyst Agent

AI-powered Investment Banking research workflow for n8n.

Email a list of companies → get back a full IB-style research package with comps, DCF indicators, SWOT analysis, M&A screening, and risk assessment.

## Files

- `skill.md` — The IB analyst skill definition, system prompt, and tools reference
- `workflow.json` — n8n workflow (import directly)

## Setup

1. Import `workflow.json` into n8n
2. Configure OpenAI + Gmail credentials
3. Send email with subject containing **"IB Research"**
4. Receive full research report with Excel attachment

## What's Included

| Section | Description |
|---------|-------------|
| Company Profile | Business overview, financials, key metrics |
| Comps Table | Peer comparison with trading multiples |
| DCF Indicators | WACC, terminal growth, implied valuation range |
| M&A Context | Sector activity, potential acquirers/targets, precedents |
| SWOT | Strengths, weaknesses, opportunities, threats |
| Risk Factors | Company, industry, regulatory, macro risks |
| Investment Thesis | Bull / base / bear case |

## Recommended APIs

| API | Purpose | Pricing |
|-----|---------|---------|
| Alpha Vantage | Stock data, financials | Free tier |
| Financial Modeling Prep | DCF, comps, statements | Free tier |
| Serper.dev | Web search | $5/mo |
| SEC EDGAR | Filings | Free |
