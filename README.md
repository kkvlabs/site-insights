# Site Insights by KKV Labs: Google Analytics 4 and Search Console MCP for Claude and ChatGPT

Site Insights by KKV Labs is a hosted, read only MCP server: paste one link into Claude or ChatGPT, sign in with Google once, and ask about the Google Analytics 4 and Search Console data of every site you manage.

```
https://insights.kkvlabs.com/mcp
```

There is nothing to install and no Google Cloud project to set up. This repository holds the documentation only. The service itself is run by KKV Labs LLC and its source code is not public.

- Website: https://www.kkvlabs.com/site-insights
- Claude connector directory: https://claude.com/marketplace/connectors/site-insights
- Support: support@kkvlabs.com

## Contents

- [Quick start](#quick-start)
- [Also works with](#also-works-with)
- [What you can ask](#what-you-can-ask)
- [Tools](#tools)
- [Ready-made prompts](#ready-made-prompts)
- [How it compares](#how-it-compares)
- [Security and privacy](#security-and-privacy)
- [Pricing](#pricing)
- [FAQ](#faq)
- [Support](#support)
- [Links](#links)

## Quick start

You need a Google account that can see your GA4 property or Search Console site. Viewer access is enough.

### Claude (web, desktop and mobile)

1. Open Customize in the left sidebar (or Settings, then Customize), then Connectors.
2. Click + Add (top right), then Add custom connector. Name it `Site Insights by KKV Labs`, paste `https://insights.kkvlabs.com/mcp` and click Continue.
3. Keep the detected settings (Sign in now and Use Claude's published identity) and click Add.
4. Click Connect, sign in with Google and click Allow.

Site Insights by KKV Labs is also listed in the Claude connector directory: https://claude.com/marketplace/connectors/site-insights

Full guide with screenshots: [docs/claude.md](docs/claude.md)

### ChatGPT (chatgpt.com on the web)

1. Open Plugins, click Add (top right), then Add custom MCP server.
2. Name it `Site Insights by KKV Labs`, paste `https://insights.kkvlabs.com/mcp` as the Server URL and keep OAuth.
3. Tick I understand and want to continue, then click Create as a plugin.
4. Click Connect, sign in with Google and click Allow.

Full guide with screenshots: [docs/chatgpt.md](docs/chatgpt.md)

### Claude Code (terminal)

```bash
claude mcp add --transport http --scope user site-insights https://insights.kkvlabs.com/mcp
```

Then start Claude Code, type `/mcp`, pick site-insights and choose Authenticate.

Full guide: [docs/claude-code.md](docs/claude-code.md)

### Then switch on your sites

After sign in, open https://insights.kkvlabs.com/account. Every GA4 property and Search Console site your Google account can see is listed and paired by domain. Switch on the sites your assistant may read: 1 on Free, 10 on Pro, 50 on Agency. If no site is switched on, the assistant answers that the site is not connected.

> **Beta:** Google is still reviewing Site Insights. Until it's done, Google may show an "unverified app" warning when you sign in. That's expected and safe: choose "Go to Site Insights by KKV Labs" to continue. Access stays read only, and you can disconnect at any time.

## Also works with

Site Insights is a standard remote MCP server with OAuth sign in. Besides Claude, ChatGPT and Claude Code (tested by us), these apps support remote MCP servers by link with their own sign in, per their official docs (checked 18 Nov 2026). We have not tested them end to end.

| App | Setup |
|---|---|
| Cursor | Add the snippet to `~/.cursor/mcp.json`, then sign in when Cursor asks. |
| OpenAI Codex (CLI and IDE) | Add the snippet to `~/.codex/config.toml`, then run `codex mcp login site_insights`. |
| Zed | Settings, then AI, then MCP Servers, then Add Server, then Add Remote Server. Or add the snippet to `settings.json`. |
| Goose | Run `goose configure`, choose Add Extension, then Remote Extension (Streamable HTTP), and paste the link. |

Cursor (`~/.cursor/mcp.json`):

```json
{ "mcpServers": { "site-insights": { "url": "https://insights.kkvlabs.com/mcp" } } }
```

OpenAI Codex (`~/.codex/config.toml`):

```toml
[mcp_servers.site_insights]
url = "https://insights.kkvlabs.com/mcp"
```

Zed (`settings.json`):

```json
"context_servers": { "site-insights": { "url": "https://insights.kkvlabs.com/mcp" } }
```

More detail and the doc links for each app: [docs/other-clients.md](docs/other-clients.md)

## What you can ask

Ask in plain English. Name a site by its domain or by the label you gave it.

- "How did example.com do last week compared with the week before?"
- "Weekly check for all my sites: what went up, what went down?"
- "Why did my client's site lose clicks since 1 November?"
- "What are my top 20 queries this month, without my brand name?"
- "Which pages are on page 2 for queries with lots of impressions?"
- "How many visits did ChatGPT and Perplexity send each site last month?"
- "Is /pricing indexed? Which canonical did Google pick?"
- "Do any of my sitemaps have errors?"
- "Show my Discover clicks by page for the last 90 days."
- "Rank all my sites by clicks this month and show the change."

Numbers such as changes, percentages and the GA4 to Search Console join are calculated on our server, so the AI does not have to do the maths. Every answer states its dates. Search Console ranges end 3 days ago, because Google finishes Search Console data about 2 to 3 days after the day ends. GA4 ranges end yesterday.

## Tools

17 tools. All are read only (`readOnlyHint: true`). Every tool takes `raw: true` to return Google's response exactly as Google sent it. Full details, parameters and an example question for each: [docs/tools.md](docs/tools.md)

| Tool | Reads | What it does | Read only |
|---|---|---|---|
| `list_sites` | Your account | Your switched on sites, their paired GA4 and Search Console properties, your plan and calls used today. Free, not counted. | Yes |
| `site_overview` | GA4 and Search Console | Performance summary for one site with the change against the period before. | Yes |
| `top_queries` | Search Console | Every Google search query with clicks, impressions, CTR, position and change. | Yes |
| `top_pages` | GA4 and Search Console | Every landing page: Search Console clicks joined with GA4 sessions, engagement and key events. | Yes |
| `traffic_drops` | GA4 and Search Console | Pages and queries that lost the most clicks or sessions, and the day each drop started. | Yes |
| `quick_wins` | Search Console | Queries at positions 4 to 20 with plenty of impressions but a low CTR, ranked by extra clicks. | Yes |
| `ai_traffic` | GA4 | Visits from ChatGPT, Perplexity, Copilot, Gemini, Claude and other AI assistants. | Yes |
| `traffic_sources` | GA4 | Sessions by channel, source and medium, source, medium or campaign, with change. | Yes |
| `compare_sites` | GA4 and Search Console | Ranks several or all sites by one metric with change. Counts as one call. | Yes |
| `search_console_query` | Search Console | Any Search Console query: every search type and dimension, filters, up to 25,000 rows per call. | Yes |
| `inspect_url` | Search Console | Google's full URL Inspection result for one URL. | Yes |
| `sitemaps` | Search Console | Every submitted sitemap as Google reports it, with errors and warnings. | Yes |
| `ga4_metadata` | GA4 | Every dimension and metric the property has, custom ones included. | Yes |
| `run_ga4_report` | GA4 | Any GA4 report with any dimensions and metrics, filters and up to 4 date ranges. | Yes |
| `run_ga4_pivot_report` | GA4 | A GA4 pivot report. | Yes |
| `run_ga4_realtime_report` | GA4 | What is happening on the site in the last 30 minutes. | Yes |
| `run_ga4_batch_reports` | GA4 | Up to 5 GA4 reports in one call. Counts as one call. | Yes |

Site Insights cannot change a setting, a property or a sitemap. Google is asked for `analytics.readonly` and `webmasters.readonly` only.

## Ready-made prompts

The server also ships five MCP prompts. In Claude Code they show up as commands when you type `/`.

| Prompt | What it does |
|---|---|
| `weekly_site_check` (Weekly site check) | A short weekly health check for one site. |
| `why_traffic_dropped` (Why did traffic drop?) | Finds what lost traffic and when it started. |
| `quick_wins_this_month` (Quick wins this month) | Pages and queries to improve first. |
| `ai_traffic_report` (AI traffic report) | Visits from ChatGPT, Perplexity, Copilot, Gemini and Claude. |
| `client_summary_all_sites` (Client summary for all sites) | One table across every connected site. |

## How it compares

The main choice is hosted or self-hosted. If you want a free, open source server that you run yourself, Google's [analytics-mcp](https://github.com/googleanalytics/google-analytics-mcp) (GA4) and [mcp-gsc](https://github.com/AminForou/mcp-gsc) (Search Console) are good options. Site Insights is for people who want one link, one Google sign in, GA4 and Search Console together, and many sites.

| | Reads | Setup | Many sites | Price | Source |
|---|---|---|---|---|---|
| Google's GA4 MCP server (analytics-mcp) | Google Analytics only | Runs on your computer or a server you host. Needs Python, a Google Cloud project, two APIs switched on and gcloud credentials | Any property your login sees. No pairing with Search Console | Free, open source | GitHub README and PyPI stats, read 17 Nov 2026 |
| **Site Insights by KKV Labs** | GA4 and Search Console, joined page by page | Hosted. Paste one link into Claude or ChatGPT and sign in with Google | Pairs GA4 and Search Console per site, labels, compare all sites | Free for 1 site. $12 a month for 10 sites, $39 for 50 | Our product |
| mcp-gsc | Search Console only | Runs locally. Needs a Google Cloud OAuth client or service account, and uv | Works across the properties on your Google account | Free, open source | GitHub README, read 18 Nov 2026 |

Want to run Google's own server? KKV Labs has a step by step guide: https://www.kkvlabs.com/guides/how-to-set-up-google-analytics-mcp-server

A longer comparison, including hosted tools, is on https://www.kkvlabs.com/site-insights

## Security and privacy

- **Read only.** Google is asked for read only access to Analytics and Search Console. Site Insights cannot change a setting, a property or a sitemap.
- **No analytics data kept.** Numbers from Google pass through to your AI assistant. They sit in a short cache for at most 60 minutes, then are deleted.
- **We never see your chat.** Claude or ChatGPT calls our tools. We see the tool call, not your prompt or the answer you read.
- **Tokens locked away.** Your Google token is encrypted (AES 256) and never leaves our server. The AI assistant gets a short lived token that only works for Site Insights.
- **Delete any time.** Disconnect, or delete everything with one button: we revoke access at Google, cancel any plan and delete every row we hold about you.
- **Google's rules apply.** Use of data from Google follows the Google API Services User Data Policy, including its Limited Use rules. No ads, no selling, no training AI models.

Summary: [docs/privacy-summary.md](docs/privacy-summary.md). Full privacy policy: https://www.kkvlabs.com/site-insights/privacy. Terms: https://www.kkvlabs.com/site-insights/terms

## Pricing

| Plan | Price | Includes |
|---|---|---|
| Free | $0 | 1 site (a GA4 property and its Search Console property), 10 lookups a day, every tool |
| Pro | $12 a month, or $120 a year | Up to 10 sites, no daily lookup limit (fair use), every tool |
| Agency | $39 a month, or $390 a year | Up to 50 sites, client labels and compare all sites, no daily lookup limit (fair use) |

A lookup is one tool call. One question can use two or three, so 10 lookups is about three to five questions a day. Listing your sites is free. Cancel any time from your account page, and if it is not for you, email us within 30 days of a payment for a full refund. Team seats on one account are planned, not available yet.

## FAQ

**Is there a Google Analytics MCP server URL I can paste into Claude?**
Yes. Site Insights by KKV Labs is a hosted one: `https://insights.kkvlabs.com/mcp`. In Claude, add it under Customize, then Connectors, then + Add, then Add custom connector. Sign in with Google and it reads both GA4 and Search Console.

**How do I connect Google Search Console to Claude?**
Add Site Insights as a custom connector in Claude with the link above, sign in with the Google account that can see your Search Console site, and switch the site on at https://insights.kkvlabs.com/account. Steps: [docs/claude.md](docs/claude.md).

**How do I connect Google Analytics 4 to ChatGPT?**
On chatgpt.com, open Plugins, click Add, then Add custom MCP server. Paste the link as the Server URL, keep OAuth, tick I understand and want to continue, click Create as a plugin, then sign in with Google. Steps: [docs/chatgpt.md](docs/chatgpt.md).

**How do I connect Google Search Console to Claude Code?**
Run `claude mcp add --transport http --scope user site-insights https://insights.kkvlabs.com/mcp`, then type `/mcp` in Claude Code, pick site-insights and choose Authenticate. Steps: [docs/claude-code.md](docs/claude-code.md).

**How do I connect both GA4 and Google Search Console to Claude in one place?**
One Google sign in covers both. Site Insights pairs each GA4 property with its Search Console site by domain, and tools such as `site_overview` and `top_pages` answer from both at once.

**Is there a hosted GA4 MCP so I don't have to set up Google Cloud credentials?**
Yes. Site Insights is hosted. You sign in with Google in the browser. There is no Google Cloud project, credentials file or install.

**Should I use a hosted Search Console MCP or self-host mcp-gsc?**
Self-host mcp-gsc if you want a free, open source server on your own machine and are happy to set up a Google Cloud OAuth client. Use a hosted one like Site Insights if you want it to work in claude.ai and ChatGPT on the web with one link, and want GA4 in the same place.

**How can I see how much traffic my site gets from ChatGPT and Perplexity by asking Claude?**
Ask "How many visits did ChatGPT and Perplexity send me in the last 90 days?". The `ai_traffic` tool reads GA4 and returns the total, the share of all sessions, each assistant, the landing pages and the trend.

**What is a good GA4 MCP for an agency managing many client sites?**
Look for one that pairs GA4 with Search Console per site, lets you label sites by client and compares all of them in one call. Site Insights does all three. The Agency plan covers up to 50 sites for $39 a month. See [docs/agencies.md](docs/agencies.md).

More questions: [docs/faq.md](docs/faq.md)

## Support

Email support@kkvlabs.com with what you saw and which step you were on.

## Links

- Site Insights home: https://www.kkvlabs.com/site-insights
- Search Console MCP page: https://www.kkvlabs.com/site-insights/search-console
- Claude guide: https://www.kkvlabs.com/site-insights/connect-claude
- ChatGPT guide: https://www.kkvlabs.com/site-insights/chatgpt
- Claude Code guide: https://www.kkvlabs.com/site-insights/claude-code
- Claude connector directory listing: https://claude.com/marketplace/connectors/site-insights
- Your account (switch on sites, plan, disconnect): https://insights.kkvlabs.com/account
- How to set up Google's own GA4 MCP server: https://www.kkvlabs.com/guides/how-to-set-up-google-analytics-mcp-server
- How to see ChatGPT traffic in Google Analytics: https://www.kkvlabs.com/guides/how-to-see-chatgpt-traffic-in-google-analytics
- Privacy policy: https://www.kkvlabs.com/site-insights/privacy
- Terms: https://www.kkvlabs.com/site-insights/terms

Documentation licensed CC BY 4.0, see [LICENSE](LICENSE). The Site Insights service is proprietary. Changes: [CHANGELOG.md](CHANGELOG.md).

© KKV Labs LLC
