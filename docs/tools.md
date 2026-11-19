# Tools

Site Insights by KKV Labs has 17 tools. Every tool is read only: each one is marked `readOnlyHint: true` and `destructiveHint: false`, and Google is asked for `analytics.readonly` and `webmasters.readonly` only.

You do not call these yourself. Ask your assistant a question in plain English and it picks the tool. This page is for when you want to know what each one does.

## Things every tool shares

- **site:** the site's domain (example.com) or the label you gave it. You can leave it out when your account has exactly one site switched on. An unknown name returns an error that lists your switched on sites, and it does not count as a lookup.
- **raw:** `true` returns Google's response exactly as Google sent it. For the computed tools, that means every Google request and response the tool used.
- **Every row.** Tools return every row and field Google sends. Big results are paged, never cut. The computed tools take `offset` and `page_size` (default 1,000, max 5,000) and say how many rows remain. The direct tools use Google's own paging (`start_row` for Search Console, `offset` for GA4).
- **Dates.** `period` is one of `last_7_days`, `last_28_days` (the default), `last_90_days`, `last_3_months`, `last_6_months`, `last_12_months`, `last_month` or `this_month`. Or pass `start_date` and `end_date` (YYYY-MM-DD). Named periods end when data is complete: Search Console 3 days ago, GA4 yesterday. Every answer states its dates.
- **Compare.** Where a tool shows change, `compare` is `previous_period` (the default: same length, right before), `previous_year` or `none`.
- **Search Console options.** `search_type` is `web` (default), `image`, `video`, `news`, `discover` or `googleNews`. `data_state` is `final` (default, complete data only) or `all` (include fresh, still changing data).

## Your account

### list_sites

**Returns:** the sites you switched on, each with its domain, label, paired GA4 property and Search Console property, plus your plan, its site limit and the tool calls you used today.

**Parameters:** none.

**Counts as a lookup:** no. Listing your sites is free.

**Example question:** "Which sites can you see, and how many lookups do I have left today?"

## Computed tools

These do the maths on our server: changes, percentages, the GA4 to Search Console join, quick win estimates and drop dates. The assistant quotes the numbers instead of working them out.

### site_overview

**Returns:** a performance summary for one site with the change against a comparison period. From GA4: sessions, users, new and active users, engaged sessions, engagement rate, key events, page views and average session duration. From Search Console: clicks, impressions, CTR, average position and the daily series. Plus the top 10 search queries, pages, traffic channels and landing pages.

**Parameters:** site, period or start and end dates, compare, search type, data state, raw.

**Example question:** "How did example.com do last week compared with the week before?"

### top_queries

**Returns:** every Google search query for one site from Search Console, with clicks, impressions, CTR, position and their change. Ranked by clicks, then impressions.

**Parameters:** site, dates, compare, search type, data state. Filters: `contains` (only queries with this text), `exclude` (leave out queries with this text, for example your brand name), `page` (only queries that led to pages whose URL contains this text), `device` (MOBILE, DESKTOP or TABLET), `country` (a three letter code such as usa). Sorting: `sort_by` (clicks, impressions, ctr_pct, position, clicks_change, impressions_change, position_change or query) and `sort_order`. Paging and raw.

**Example question:** "What are my top 20 queries this month, without my brand name?"

### top_pages

**Returns:** every landing page for one site, with Search Console clicks, impressions, CTR and position joined to GA4 sessions, engagement rate and key events for the same dates. Google clicks and what those visitors did, on one row. Ranked by clicks.

**Parameters:** site, dates, search type, data state, `sort_by` (gsc_clicks, gsc_impressions, gsc_ctr_pct, gsc_position, ga4_sessions, ga4_key_events or page), `sort_order`, paging, raw.

**Example question:** "Which pages get the most Google clicks, and how engaged are those visitors?"

### traffic_drops

**Returns:** every page and search query that lost Search Console clicks, and every landing page that lost GA4 sessions, against a comparison period. Largest loss first, with the day each drop started and the site totals.

**Parameters:** site, dates, compare, search type, data state, paging, raw.

**Example question:** "Why did clicks drop on my client's site, and when did it start?"

### quick_wins

**Returns:** search query and page pairs at average positions 4 to 20 with enough impressions but a click through rate below the typical rate for that position. Ranked by the estimated extra clicks a better title or page could bring.

**Parameters:** site, dates, search type, data state, `min_impressions`, `min_position` and `max_position` (to change the 4 to 20 range), paging, raw.

**Example question:** "Which pages should I improve first to get more clicks?"

### ai_traffic

**Returns:** visits from AI assistants from GA4: the total, the share of all sessions, each assistant, every landing page and the daily trend, with change. Assistants it recognises by referrer: ChatGPT, Perplexity, Copilot, Gemini, Claude, DeepSeek, Meta AI, Grok, Mistral, You.com and Phind.

**Parameters:** site, dates, compare, paging, raw.

**Example question:** "How many visits did ChatGPT and Perplexity send me in the last 90 days?"

### traffic_sources

**Returns:** every GA4 traffic source for one site with sessions, share, users, engagement, key events and change. Ranked by sessions.

**Parameters:** site, dates, compare, `group_by` (channel, source_medium, source, medium or campaign), paging, raw.

**Example question:** "Where did my sessions come from last month?"

### compare_sites

**Returns:** several or all of your switched on sites ranked by one metric, with change against a comparison period.

**Parameters:** `sites` (a list of domains or labels, up to 50; default every switched on site), `metric` (clicks, the default, or impressions, ctr, position, sessions, users, key_events, ai_sessions), dates, compare, `sort_by` (value, change or change_pct), raw.

**Counts as:** one lookup, however many sites it covers.

**Example question:** "Rank all my sites by clicks this month and show the change."

## Direct Search Console tools

These pass your request to Google's Search Console APIs and return the full result.

### search_console_query

**Returns:** a Search Console Search Analytics query with every option. Rows ranked by clicks, then impressions (date order when date is the first dimension). Every row and field Google sends.

**Parameters:** site, `dimensions` (any of query, page, country, device, date, searchAppearance), search type (web, image, video, news, discover or googleNews), dates, `dimension_filter_groups` (Google's filter groups, including regex), `aggregation_type` (auto, byPage, byProperty or byNewsShowcasePanel), `data_state` (final, all or hourly_all), `row_limit` (default 1,000, up to 25,000 per call), `start_row` for paging, `sort_by`, `sort_order`, raw.

**Example question:** "Show my Discover clicks by page for the last 90 days."

### inspect_url

**Returns:** Google's full URL Inspection result for one URL: index status (verdict, coverage, robots, indexing, fetch, crawl time, crawled as, the canonical Google picked and the one you declared, referring URLs, sitemaps), mobile usability, AMP and rich results.

**Parameters:** site, `url` (a full URL or a path starting with /), `language_code`, raw.

**Example question:** "Is /pricing indexed? Which canonical did Google pick?"

### sitemaps

**Returns:** every sitemap submitted in Search Console for a site, exactly as Google reports it: path, type, when it was last submitted and downloaded, pending, index flag, errors, warnings and contents by type.

**Parameters:** site, raw.

**Example question:** "Do any of my sitemaps have errors?"

## Direct GA4 tools

These call the GA4 Data API and return every row and field Google sends.

### ga4_metadata

**Returns:** every dimension and metric the GA4 property has, including its custom dimensions and metrics, with API name, UI name, description, category and type.

**Parameters:** site, `search` (only fields whose name or category contains this text), `custom_only`, paging, raw.

**Example question:** "Which custom dimensions does example.com's GA4 property have?"

### run_ga4_report

**Returns:** a full GA4 report with any dimensions and metrics the property has, custom ones included. Also returns Google's sampling, thresholding and quota information.

**Parameters:** site, `dimensions`, `metrics`, up to 4 `date_ranges` (or period or dates), `dimension_filter` and `metric_filter` (GA4 filter expressions), `order_bys`, `limit` (default 1,000, up to 250,000) and `offset`, `metric_aggregations`, `comparisons`, `keep_empty_rows`, `currency_code`, raw.

**Example question:** "Show sessions by my custom dimension plan_type and country."

### run_ga4_pivot_report

**Returns:** a GA4 pivot report: Google's pivot headers and every row.

**Parameters:** everything `run_ga4_report` takes, plus `pivots` (GA4 pivot objects). Google requires every requested dimension to appear in exactly one pivot.

**Example question:** "Pivot last month's sessions by country and device category."

### run_ga4_realtime_report

**Returns:** what is happening on the site in the last 30 minutes, for example active users by country, device category, screen name or minutes ago.

**Parameters:** site, `dimensions`, `metrics` (default activeUsers), `dimension_filter`, `metric_filter`, `order_bys`, `limit`, up to 2 `minute_ranges`, `metric_aggregations`, raw.

**Example question:** "How many people are on example.com right now, by country?"

### run_ga4_batch_reports

**Returns:** up to 5 GA4 reports for one site in a single call. Each report has its own dimensions, metrics, date ranges, filters, order by, limit, offset, aggregations, comparisons and keep empty rows.

**Parameters:** site, `requests` (1 to 5 report requests), raw.

**Counts as:** one lookup.

**Example question:** "In one go, show last month's sessions by channel, by device and by landing page."

## Lookups and plans

A lookup is one tool call. One question can use two or three. The Free plan has 10 lookups a day, and the count resets at midnight UTC. Pro and Agency have no daily limit under fair use. `list_sites` is free, `compare_sites` and `run_ga4_batch_reports` count as one each, and a wrong site name costs nothing.

[Back to README](../README.md)
