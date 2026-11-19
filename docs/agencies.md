# Site Insights for agencies and many sites

Site Insights by KKV Labs is built for people who look after many sites: agencies, freelancers and anyone with a portfolio. One Google sign in covers every site that Google account can see, and one question can cover all of them.

## How it works with many sites

### Paired once

After you sign in, Site Insights finds every GA4 property and Search Console site your Google account can see and pairs them by domain. Each pair is one site. You can change a pair on your account page at https://insights.kkvlabs.com/account.

A site with only Search Console works too. If the same Google account also sees the site's GA4 property, the two are paired and the answers join Search Console clicks with GA4 sessions and engagement.

### Switched on

On the account page, switch on the sites your AI assistant may read. The assistant can only read sites you switched on. The number you can switch on depends on your plan: 1 on Free, 10 on Pro, 50 on Agency.

### Labelled your way

Give each site a label, such as a client's name (for example "Client: Acme"), and ask about it by that label in Claude or ChatGPT. The `site` input of every tool takes either the domain or the label.

### Compared in one call

Ask for every site ranked by clicks, impressions, CTR, position, sessions, users, key events or AI visits, with the change since the last period. The `compare_sites` tool does this in one call, and it counts as one lookup however many sites it covers. On the Agency plan that is up to 50 sites in one table.

The ready-made prompt `client_summary_all_sites` builds one table across every connected site, with clicks, sessions and AI sessions and their change, then lists the three sites that need attention first.

## Questions agencies ask

- "Weekly check for all my sites: what went up, what went down?"
- "Rank all my sites by clicks this month and show the change."
- "Why did my client's site lose clicks since 1 November?"
- "How many visits did ChatGPT and Perplexity send each site last month?"
- "Compare all my client sites by clicks this month."

## Give one Google account access to client properties

Site Insights reads whatever your Google account can see. To read a client's data, the client (or whoever manages their properties) adds your Google account to their GA4 property and their Search Console site. Read access is enough, because Site Insights only reads.

### Google Analytics 4

1. In GA4, open Admin.
2. Under the property, open Property access management.
3. Add a user: enter your Google account's email address and give it the Viewer role.
4. Save.

Only someone with the Administrator role on the property can add users.

### Search Console

1. In Search Console, open the client's property, then Settings.
2. Open Users and permissions.
3. Click Add user, enter your Google account's email address and choose Restricted permission. Restricted is enough.
4. Click Add.

Only an owner of the property can add users.

Then open https://insights.kkvlabs.com/account. If the new property is not listed yet, use Refresh from Google on the Sites list. Check the pair, add a label and switch the site on.

## Plans for many sites

| Plan | Price | Sites |
|---|---|---|
| Free | $0 | 1 site, 10 lookups a day |
| Pro | $12 a month, or $120 a year | Up to 10 sites, no daily lookup limit (fair use) |
| Agency | $39 a month, or $390 a year | Up to 50 sites, client labels and compare all sites, no daily lookup limit (fair use) |

It is a flat price: not a price per site or per client. Agencies pay the same whether a client site is busy or quiet.

## Teams

Today each person signs in with their own Google account and their own plan. Team seats on one account are planned for a later version.

In Claude Code, `--scope project` saves the server in the project's `.mcp.json` so your team gets it through git. Each person still signs in with their own Google account. See [claude-code.md](claude-code.md).

[Back to README](../README.md)
