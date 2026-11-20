# FAQ

## About Site Insights

**What is Site Insights by KKV Labs?**
A hosted remote MCP server that lets Claude, ChatGPT and other AI assistants read your Google Analytics 4 and Google Search Console data. You paste one link, `https://insights.kkvlabs.com/mcp`, sign in with Google once, and ask about every site you manage in plain English. It is read only.

**What is a Google Analytics MCP?**
MCP (Model Context Protocol) is the standard way Claude, ChatGPT and other AI assistants connect to outside tools. A Google Analytics MCP server gives the assistant tools that read your GA4 data, so you can ask about your traffic in plain English. Site Insights is a hosted one that also reads Search Console.

**What is a Google Search Console MCP?**
A connector that gives Claude, ChatGPT or another AI assistant tools to read your Search Console data through MCP. You ask about clicks, queries, pages and indexing in plain English and the assistant pulls the numbers from Google.

**Is Site Insights verified by Google?**
Yes. Google approved Site Insights by KKV Labs in November 2026, so sign in shows no warning. Access is read only, and you can disconnect at any time.

**Why did KKV Labs build it?**
KKV Labs runs about 10 sites of its own and checked Google Analytics, Search Console, Bing and Clarity for each of them by hand every week. Google's own GA4 MCP server is downloaded about 36,845 times a week (PyPI, 17 November 2026), but it is made to run on your own computer or a server you set up, and it needs a Google Cloud project and credentials first. We could not find a hosted connector that reads GA4 and Search Console together, so we built one.

## Setup

**Is there a Google Analytics MCP server URL I can paste into Claude?**
Yes: `https://insights.kkvlabs.com/mcp`. Add it in Claude under Customize, then Connectors, then + Add, then Add custom connector. See [claude.md](claude.md).

**Does it work in both Claude and ChatGPT?**
Yes. In Claude (web, desktop and mobile), add it as a custom connector under Customize, then Connectors. In ChatGPT, on chatgpt.com on the web, open Plugins, click Add, then Add custom MCP server. Both use the same link and the same Google sign in. See [chatgpt.md](chatgpt.md).

**Do I need a paid Claude or ChatGPT plan?**
Claude: Free, Pro, Max, Team and Enterprise can all add a custom connector; on Team and Enterprise an owner may need to allow custom connectors first. ChatGPT: works on chatgpt.com (web). Checked with Plus on 18 Nov 2026. OpenAI lists custom MCP servers for Pro, Business, Enterprise and Edu.

**Does it work in Claude Code and other MCP clients?**
Yes. It is a standard remote MCP server with OAuth sign in. We tested Claude Code end to end, and confirmed Cursor, OpenAI Codex, Zed and Goose against their docs on 18 Nov 2026. See [claude-code.md](claude-code.md) and [other-clients.md](other-clients.md).

**Do I need a Google Cloud project or credentials file?**
No. Site Insights is hosted: you sign in with Google in the browser.

**Which Google access do I need?**
A Google account that can see the GA4 property or the Search Console site. Viewer access is enough.

**The assistant says my site is not connected. What now?**
Open https://insights.kkvlabs.com/account and switch the site on. Then ask again in a new chat.

## Data

**Which data can it read?**
Anything your Google account can see in GA4 and Search Console: every property and site, every dimension and metric including custom ones, standard, pivot and realtime GA4 reports, every Search Console search type, URL inspection and sitemaps. See [tools.md](tools.md).

**Which Search Console data does it read?**
Search performance for every search type (web, image, video, news, Discover and Google News) by query, page, country, device, date and search appearance, plus URL inspection and sitemaps. Up to 25,000 rows per call, paged, for every site your Google account can see.

**Does it need Google Analytics too?**
No. A site with only Search Console works. If the same Google account also sees the site's GA4 property, the two are paired and the answers join Search Console clicks with GA4 sessions and engagement.

**Why is the latest Search Console data a few days old?**
Search Console finishes its numbers about two to three days after the day ends. Site Insights ends Search Console date ranges three days ago so a comparison never uses a half counted day, and every answer states its dates.

**Can it see my traffic from ChatGPT, Perplexity and other AI assistants?**
Yes. The `ai_traffic` tool reads GA4 and reports visits from ChatGPT, Perplexity, Copilot, Gemini, Claude and other assistants: the total, the share of all sessions, each assistant, the landing pages and the trend.

**Does the AI make up the numbers?**
Changes, percentages and the GA4 join are calculated on our server before the answer reaches the AI, so it does not have to do the maths. Ask for raw and you get Google's response exactly as Google sent it, to check the numbers yourself.

## Safety

**Is it safe to give it access?**
It asks Google for read only access to Analytics and Search Console, so it cannot change anything. Analytics numbers are kept in a short cache for at most 60 minutes and then deleted. Your Google token is encrypted and never sent to the AI assistant. You can delete all your data with one button. See [privacy-summary.md](privacy-summary.md).

**Can it change my Search Console or GA4 settings?**
No. It cannot submit sitemaps, remove URLs, or change a setting, a property or a user.

**How do I disconnect?**
In Claude, open the connector and click Disconnect. In ChatGPT, you can manage or disconnect apps in your settings. In Site Insights, open the account page and click Disconnect Google and AI assistants, or Delete all my data. You can also remove access in your Google account settings.

## Plans

**How many sites can I connect?**
One on the free plan, 10 on Pro ($9 a month) and 50 on Agency ($49 a month).

**What is a lookup?**
One tool call. One question can use two or three, so the Free plan's 10 lookups a day is about three to five questions. Listing your sites is free.

**Can my team use it?**
Today each person signs in with their own Google account and their own plan. Team seats on one account are planned for a later version.

**Can I get a refund?**
Cancel any time from your account page. If it is not for you, email support@kkvlabs.com within 30 days of a payment for a full refund.

## Compared with other options

**How is this different from Google's own GA4 MCP server?**
Google's server is free and made to run on your own computer or a server you set up, with a Google Cloud project and credentials, and it reads GA4 only. Site Insights is hosted, needs one Google sign in, reads GA4 and Search Console together and is built for many sites.

**Should I use a hosted Search Console MCP or self-host mcp-gsc?**
mcp-gsc is a good free, open source choice if you want to run a server on your own machine and set up a Google Cloud OAuth client. A hosted one like Site Insights works in claude.ai and ChatGPT on the web with one link, and includes GA4.

[Back to README](../README.md)
