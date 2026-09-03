# GoodPostal MCP server

GoodPostal is email marketing where you bring your own email sending service. You connect Amazon SES, SendGrid, Mailgun, Postmark, SMTP2GO, or Mailtrap, pay them directly for delivery, and pay GoodPostal only for the software: $19 a month or $190 a year, half that for verified nonprofits, plus $0.05 per 1,000 emails sent. Contacts never change the price. There is a 14-day trial with no card.

This repository is the public listing for GoodPostal's two MCP servers. The servers run at goodpostal.com; nothing here needs to be installed.

## The two servers

| Server | Address | Login | Tools |
|---|---|---|---|
| GoodPostal | `https://mcp.goodpostal.com/mcp/goodpostal` | OAuth 2.1 with PKCE, starts automatically in your browser | 57 |
| GoodPostal Pricing | `https://mcp.goodpostal.com/mcp/pricing` | None | 3 |

Transport is Streamable HTTP for both. The GoodPostal server publishes OAuth discovery at `/.well-known/oauth-protected-resource`, so any client that follows the MCP authorization spec signs in without keys to copy.

## Connect

**Claude Code**

```bash
claude mcp add --transport http goodpostal https://mcp.goodpostal.com/mcp/goodpostal
```

**Cursor**, in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "goodpostal": {
      "url": "https://mcp.goodpostal.com/mcp/goodpostal"
    }
  }
}
```

**Codex CLI**

```bash
codex mcp add goodpostal --url https://mcp.goodpostal.com/mcp/goodpostal
codex mcp login goodpostal
```

**Claude desktop and web**: Settings, Connectors, Add custom connector, address `https://mcp.goodpostal.com/mcp/claude`.

**Anything else**: server address `https://mcp.goodpostal.com/mcp/goodpostal`, transport Streamable HTTP, auth OAuth 2.1 by discovery.

Full setup guide, with screenshots: https://goodpostal.com/docs/ai-integration

## What the GoodPostal server can do

- **Contacts and groups**: search, create, and update contacts, manage groups, add contacts to groups by filter, define custom fields.
- **Templates**: list, create, update, and preview email templates built from a library of 90 components, choose a design direction, send a test email.
- **Images**: upload or import images, create gradient, icon, and transition images, manage folders.
- **Campaigns**: create, update, review, and send campaigns, change campaign status, read campaign analytics.
- **Sending setup**: list connected sending services, manage sender identities, set and verify the tracking domain, update email branding.
- **Workspace**: plan usage, brand guidelines, workspace info, documentation search.

Every write goes through the same permission checks as the dashboard. A workspace's data is never visible to another workspace.

## What the pricing server can do

No login, no workspace, rate limited. Three tools:

- `list_email_providers`: every provider in the dataset, six sending services and seven per-contact marketing platforms.
- `get_provider_pricing`: the full scraped price table for one provider, with the date it was last verified.
- `estimate_goodpostal_cost`: the monthly GoodPostal bill for a send volume, with Amazon SES delivery shown as the reference.

Prices are scraped from published pricing pages every week. Ask your client "what would 5,000 contacts and two sends a month cost on Mailchimp versus GoodPostal with SES" and it has the numbers.

## Links

- Product: https://goodpostal.com
- Docs: https://goodpostal.com/docs
- AI integration guide: https://goodpostal.com/docs/ai-integration
- Changelog: https://goodpostal.com/changelog
- Privacy: https://goodpostal.com/privacy
- Terms: https://goodpostal.com/terms
