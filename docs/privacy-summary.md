# Privacy summary

Short version: read only access, used only to answer the questions you ask your AI assistant, kept for at most 60 minutes, never sold, and deleted in one click.

This is a summary. The privacy policy is the full and binding text: https://www.kkvlabs.com/site-insights/privacy (last updated 18 November 2026). Terms: https://www.kkvlabs.com/site-insights/terms

## Who runs it

Site Insights by KKV Labs is run by KKV Labs LLC, in the United States.

## What we ask Google for

When you sign in with Google, we ask for these permissions and nothing more:

- Your basic profile and email address (openid, email), to create your account and sign you in.
- See and download your Google Analytics data (`analytics.readonly`), to answer questions about your GA4 properties.
- View Search Console data for your verified sites (`webmasters.readonly`), to answer questions about search performance, URL inspection and sitemaps.

Both data permissions are read only. Site Insights cannot change your Analytics or Search Console settings, properties, users or sitemaps.

## How we use it

Only to provide the feature you asked for: when your AI assistant calls a Site Insights tool, we read the matching data from Google and return it to that assistant, at your request. Every request checks that the site belongs to your account and is switched on.

Our use of data from Google follows the Google API Services User Data Policy, including its Limited Use requirements. We do not sell it, we do not use it for advertising, and we do not use it to develop, improve or train AI or machine learning models.

## What we store

- Your name, email address and Google account id.
- Your Google tokens, encrypted with AES 256 and never sent to any AI assistant.
- Your list of GA4 properties and Search Console sites, how they are paired, which are switched on and any labels.
- Your plan, billing status and a count of tool calls per day for plan limits.
- Analytics and Search Console numbers only in a short cache, for at most 60 minutes. Then they are deleted.

## What we never receive

- Your conversations. Your AI assistant sends us a tool call (for example: top queries for a site and a date range) and we send back the data. Your prompts and the answers you read stay with the assistant you use.
- Your card number. Payments are handled on Stripe's own checkout page.

## Tokens given to AI assistants

They last one hour, work only for Site Insights and are rotated. Our logs record error types only, never tokens, email addresses or query text.

## Who processes data for us

Vercel (hosting), Supabase (database), Stripe (payments) and Google (the source of the data you ask about).

## Deleting your data

- **Disconnect** on your account page revokes our access at Google, deletes the stored Google tokens and ends every AI assistant connection.
- **Delete all my data** does the same, cancels any paid plan and deletes every record we hold about you, straight away.
- You can also remove Site Insights in your Google account under third party access. The next call then fails, and we clear the stored tokens.
- Or email support@kkvlabs.com.

[Back to README](../README.md)
