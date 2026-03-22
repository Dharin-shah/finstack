# FinStack

AI-powered finance workflows and agent skills. Built with n8n + GPT-4o.

## Workflows

### Investment Banking (`/ib`)
- **IB Analyst Agent** — Email-triggered deep company research with comps, DCF indicators, SWOT, M&A screening
- Outputs: Styled HTML report + Excel/CSV attachment

### Coming Soon
- Equity Research workflows
- Portfolio monitoring agents
- Risk analysis pipelines
- Deal pipeline automation

## Quick Start

1. Self-host n8n via Docker: `docker run -d -p 5678:5678 docker.n8n.io/n8nio/n8n`
2. Import a workflow JSON from any folder
3. Configure credentials (OpenAI, Gmail, financial APIs)
4. Activate and trigger via email

## Stack

- **n8n** — workflow automation
- **GPT-4o** — AI agent reasoning
- **Wikipedia + Web Search** — research tools
- **Financial APIs** — Alpha Vantage, FMP, Yahoo Finance (optional)

## License

MIT
