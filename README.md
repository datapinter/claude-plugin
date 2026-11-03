# DataPinter for Claude

<img src="https://raw.githubusercontent.com/datapinter/claude-plugin/master/assets/logo.png" alt="DataPinter" width="96" height="96">

Research marketplace products, sellers, keyword demand and affiliate performance with DataPinter. This plugin bundles a remote MCP connector and a research skill that guides source-grounded comparisons, identifier handling and service limits.

Maintained by **PT Solusi Penjual Pintar**. This repository is the public plugin distribution; the hosted DataPinter backend is a separate service. Publishing this repository does not mean the plugin has been approved for the Claude Directory.

## Requirements

- A DataPinter account with access to the requested research features. Account entitlements and normal service quotas apply in addition to MCP limits.
- Shopee research tools currently require an eligible paid plan and are unavailable to Free accounts. Discovering a tool does not guarantee that your plan includes it.
- A Claude client supporting plugins and remote MCP, with installation allowed by your organization when applicable.
- An internet connection to `https://api.datapinter.com/mcp` and DataPinter's OAuth sign-in pages.

No API key or password belongs in the plugin configuration or in chat. Research access uses OAuth with the `features:read` scope.

## Install the bundle in Claude Code

In Claude Code, add this repository as a marketplace, then install DataPinter:

```text
/plugin marketplace add datapinter/claude-plugin
/plugin install datapinter@datapinter-plugins
```

Run `/mcp`, select the DataPinter server and complete its browser OAuth sign-in when prompted. Review the requested access and approve it only for the intended DataPinter account. Restart the session if the installed plugin is not loaded yet.

The plugin adds the `datapinter-research` skill; Claude can use it when a request matches the research workflow. You can also invoke `/datapinter:datapinter-research` directly.

## Connect only the MCP server in Claude

For Claude's hosted custom-connector flow, add a custom web connector named **DataPinter** with URL:

```text
https://api.datapinter.com/mcp
```

Choose OAuth sign-in and **Register automatically** if client-registration options are shown. DataPinter currently advertises Dynamic Client Registration (DCR), rather than Client ID Metadata Documents (CIMD). Complete sign-in and consent in the browser. Interface labels may vary by Claude version and plan.

Adding only this connector makes the server's tools available; it does not install this repository's research skill. Avoid connecting duplicate copies of the same server in a session.

## Try it

- “Find 8 water bottles on TikTok Shop Indonesia. Compare returned prices, ratings and reported sales with source links.”
- “Find sunscreen stores on Tokopedia and compare the returned store information.”
- “Research Shopee keyword demand for botol minum and explain what the returned volumes do and do not establish.” (Requires an eligible paid plan.)

Choose the marketplace from the user's request, links, identifiers and region. If it is unclear, ask which marketplace they want and offer TikTok Shop as an option. Do not assume Shopee or silently switch a requested marketplace.

The configured research tools cover Shopee, TikTok Shop, Tokopedia, Lazada, Blibli, Temu, Amazon and Alibaba, with additional affiliate and cross-market research workflows. Operations and country coverage vary by tool; a marketplace name does not imply every feature or country is supported. See the [routing reference](https://github.com/datapinter/claude-plugin/blob/master/skills/datapinter-research/references/tool-routing.md).

## Limits and boundaries

- MCP allows 10 admitted calls per minute, a fair-use allowance of 100 resource units per day resetting at midnight WIB (Asia/Jakarta, UTC+7), and at most two concurrent calls per user across sessions.
- Resource units measure research usage, not the number of returned data records. An ordinary tool call costs one unit; supported affiliate batches accept up to five IDs and cost one unit per ID. For example, a search returning 20 products costs one unit, while a five-ID affiliate batch costs five units. One chat message may trigger multiple tool calls.
- Lists return at most 20 results. Normal account entitlements may reduce results further or prevent access. Admitted calls can consume quota and resource units even when an upstream request fails.
- Results may be cached, delayed, incomplete or unavailable. Reported sales, revenue and commission metrics do not guarantee future sales or profit. Compare currencies and reporting periods carefully.
- Research tools do not purchase goods, modify listings, contact affiliates, transfer money, expose private buyer records or delete accounts.

## Privacy and support

DataPinter receives research parameters and stores account-linked research history, OAuth connection records and operational usage records. Requested results return to the Claude client for the answer. Revoking a connection stops its access; it does not automatically delete stored records.

Manage connections in the [DataPinter app](https://app.datapinter.com/app/connectors). For support or data/account deletion requests, contact [WhatsApp +62 881 6866 088](https://wa.me/628816866088) or [support@datapinter.com](mailto:support@datapinter.com). Deletion requests are handled by a human team within 1 × 24 hours, with ownership verification as needed and applicable legal retention exceptions. DataPinter deletion does not delete conversations held by Claude or ChatGPT.

Published policies: [Privacy](https://datapinter.com/privacy-policy/), [Terms](https://datapinter.com/terms-and-conditions/).

Expected access restrictions return a notice with `status: "unavailable"`, a message and next steps. Claude should explain these kindly in the user's language, without presenting them as a broken tool or inventing research results:

- **Feature excluded from the plan:** explain the restriction and suggest upgrading in DataPinter to a plan that includes the feature. Waiting until tomorrow does not unlock it. For blocked Shopee research, offer TikTok Shop or another marketplace if the user wants an alternative; its own access rules and quota still apply.
- **Daily MCP allowance exhausted:** wait until midnight WIB. Upgrading does not bypass this fixed fair-use limit.
- **Account research quota exhausted:** check the remaining quota and renewal date in DataPinter; wait for renewal or upgrade/add quota if available. The daily MCP reset does not restore account quota.
- **Rate or concurrency limit:** respect `retryAfter` in seconds or wait for active calls to finish. Do not retry immediately or switch tools to bypass limits.
- **Marketplace maintenance:** try again later or offer another marketplace if the user wants one. Upgrading does not resolve maintenance.

For authentication failures, reconnect through OAuth. Never paste tokens into an issue. Send sanitized reproduction steps to support.

## Validate the plugin

```sh
claude plugin validate .claude-plugin/plugin.json
claude plugin validate .claude-plugin/marketplace.json
```

## License

MIT, copyright 2026 PT Solusi Penjual Pintar. The license covers the files distributed here; it does not license the hosted backend or grant additional service access. DataPinter is an independent service and does not claim endorsement by Anthropic, OpenAI or the named marketplaces.
