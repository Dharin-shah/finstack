# IB Analyst AI Agent — n8n Workflow Skill

> A comprehensive AI-powered Investment Banking analyst workflow for n8n.
> Built for analysts, associates, and anyone who wants IB-grade research on autopilot.

## What This Does

Email a list of companies → get back a full IB-style research package:
- **Company Profiles** with financial metrics
- **Comparable Company Analysis (Comps)** with trading multiples
- **DCF Valuation Summary** with implied share prices
- **M&A Screening** — potential acquirers/targets
- **Industry & Sector Analysis**
- **SWOT + Risk Assessment**
- **Excel attachment** with structured data for modeling
- **Styled HTML report** delivered to your inbox

## Architecture

```
┌──────────────┐    ┌──────────────┐    ┌───────────────┐    ┌──────────────────┐
│ Gmail Trigger │───▶│ Subject Gate │───▶│  Sanitize &   │───▶│  IB Research     │
│ (poll/min)   │    │ "IB Research"│    │  Extract Cos  │    │  Agent (GPT-4o)  │
└──────────────┘    └──────────────┘    └───────────────┘    └────────┬─────────┘
                                                                      │
                                              ┌───────────────────────┼──────────────────┐
                                              │                       │                  │
                                        ┌─────▼─────┐         ┌──────▼──────┐    ┌──────▼──────┐
                                        │ Wikipedia  │         │ Web Search  │    │ Financial   │
                                        │ Tool       │         │ Tool        │    │ Data Tool   │
                                        └─────┬─────┘         └──────┬──────┘    └──────┬──────┘
                                              │                       │                  │
                                              └───────────────────────┼──────────────────┘
                                                                      │
                                                              ┌───────▼────────┐
                                                              │ Build Report   │
                                                              │ + Comps Table  │
                                                              │ + DCF Summary  │
                                                              └───────┬────────┘
                                                                      │
                                                         ┌────────────┼────────────┐
                                                         │                         │
                                                   ┌─────▼─────┐           ┌──────▼──────┐
                                                   │ Create    │           │ (Optional)  │
                                                   │ Excel/CSV │           │ Slack/WA    │
                                                   └─────┬─────┘           │ Approval    │
                                                         │                 └──────┬──────┘
                                                         │                        │
                                                   ┌─────▼────────────────────────▼──┐
                                                   │     Send Report Email           │
                                                   │     (HTML + Excel attachment)   │
                                                   └────────────────────────────────-┘
```

## The IB Analyst Skill (System Prompt)

```
You are a senior Investment Banking analyst at a bulge bracket bank.
You produce institutional-quality research for deal teams and clients.

Your research must include:

### 1. Company Profile
- Legal name, ticker, exchange, GICS sector/industry
- HQ, CEO, founding year, employee count
- Business description (what they do, revenue segments, geographic mix)

### 2. Financial Summary (Latest Available)
- Market Cap, Enterprise Value
- Revenue (LTM), Revenue Growth YoY
- EBITDA, EBITDA Margin
- Net Income, EPS
- P/E, EV/EBITDA, EV/Revenue, P/B
- Debt/EBITDA (Leverage), Interest Coverage
- FCF, FCF Yield
- Dividend Yield (if applicable)
- ROE, ROIC

### 3. Comparable Company Analysis
Build a comps table with 3-5 closest peers for each target:
| Company | Ticker | Mkt Cap | EV/Revenue | EV/EBITDA | P/E | Rev Growth | EBITDA Margin |

### 4. Simplified DCF Indicators
- Estimated WACC range
- Terminal growth rate assumption
- Implied valuation range (low/mid/high) based on:
  - Comps-based (median peer multiples applied)
  - DCF-implied (if estimable from available data)

### 5. M&A Context
- Recent M&A activity in the sector
- Potential strategic acquirers (and why)
- Potential acquisition targets (and why)
- Relevant precedent transactions with multiples

### 6. SWOT Analysis
- Strengths, Weaknesses, Opportunities, Threats
- Competitive moat assessment (none/narrow/wide)

### 7. Risk Factors
- Company-specific risks
- Industry/macro risks
- Regulatory risks
- Key man / concentration risks

### 8. Catalyst Timeline
- Upcoming earnings dates
- Product launches / regulatory decisions
- M&A speculation / strategic review potential

### 9. Investment Thesis
- Bull case (2-3 sentences)
- Base case (2-3 sentences)
- Bear case (2-3 sentences)
```

## Tools Required

### Core Tools (included in workflow)
| Tool | Purpose | n8n Node |
|------|---------|----------|
| **Wikipedia** | Company background, history, business description | `toolWikipedia` |
| **Web Search** | Latest news, earnings, M&A activity | `toolHttpRequest` → Google/SerpAPI |
| **Code Tool** | Financial calculations, ratio computation | `toolCode` |

### Recommended API Integrations (enhance with these)
| Tool | Purpose | How to Add |
|------|---------|------------|
| **Alpha Vantage** | Real-time stock data, financials, ratios | Free API key → HTTP Request Tool |
| **Financial Modeling Prep** | DCF data, comps, financial statements | Free tier available → HTTP Request Tool |
| **Yahoo Finance (via RapidAPI)** | Stock quotes, analyst ratings, earnings | RapidAPI key → HTTP Request Tool |
| **SEC EDGAR** | 10-K, 10-Q filings, insider transactions | Free, no key needed → HTTP Request Tool |
| **News API** | Latest company/sector news | Free tier → HTTP Request Tool |
| **Polygon.io** | Market data, options flow | Free tier → HTTP Request Tool |
| **Serper.dev** | Google search results as API | $5/mo for 2500 queries → HTTP Request Tool |

### Optional Enhancements
| Tool | Purpose |
|------|---------|
| **Google Sheets** | Write comps table to shared sheet |
| **Slack** | Human-in-the-loop approval before sending |
| **Notion** | Archive research to knowledge base |
| **Airtable** | Deal pipeline tracking |
| **Google Drive** | Store PDF/Excel reports |

## Quick Start

### Prerequisites
- n8n instance (Docker or cloud)
- OpenAI API key (GPT-4o recommended)
- Gmail OAuth2 credentials

### Setup
1. Import `ib-analyst-workflow.json` into n8n
2. Configure credentials (OpenAI, Gmail)
3. (Optional) Add API keys for financial data providers
4. Activate the workflow
5. Send an email with subject containing "IB Research" to trigger

### Trigger Email Format
```
Subject: IB Research
Body: Please analyze Stripe, Plaid, and Adyen for a fintech sector overview.
```

### What You Get Back
- Professional HTML email with full IB-style research
- CSV/Excel attachment with all financial data in tabular format
- Comps table, DCF indicators, SWOT, risk factors, M&A context

## Customization Ideas

- **Sector Focus**: Modify the system prompt for specific sectors (healthcare, energy, tech)
- **Deal-Specific**: Add prompts for "prepare CIM outline" or "identify bolt-on targets"
- **Pitch Book Mode**: Generate slide-ready bullet points
- **Weekly Digest**: Schedule to run weekly on a watchlist
- **Multi-Language**: Add translation node for cross-border deals

## Limitations

- Financial data is based on AI knowledge + Wikipedia (not real-time)
- Add financial APIs (Alpha Vantage, FMP) for live data
- DCF is indicative only — no substitute for a proper model
- Always verify data before using in client-facing materials

## License

MIT — use it, fork it, build on it.

---

*Built with n8n + GPT-4o. Part of the FinanceStack toolkit.*
