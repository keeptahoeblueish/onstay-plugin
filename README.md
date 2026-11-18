# OnStay

Connect your OnStay host account to Antigravity to view homes, inspect calendars, answer guest questions, teach your concierge, and manage turnover settings.

## Setup

1. Install **OnStay** from the Marketplace (or run `agy plugin install https://github.com/keeptahoeblueish/onstay-plugin`).
2. Under **Customizations > Installed > MCP Servers**, click **Authenticate** next to `onstay` (or start a prompt that uses OnStay).
3. Sign in with your OnStay email or mobile number on `https://onstay.ai`, choose **View only** or **View and change**, select **All homes** or a single home, and click **Allow**.

Alternatively, you can connect with a scoped Host API key (`onstay_live_...`) created in **Settings -> Integrations** at `https://onstay.ai/settings?tab=integrations`.

## Included Capabilities

### View (`onstay:view`)
- **Homes & Details**: `list_properties`, `get_property` (check-in/out times, Wi-Fi network name, parking, readiness, equipment guides; Wi-Fi passwords and door codes are never exposed).
- **Calendars**: `get_calendar` (stays and blocked dates across any date range).
- **Guest Conversations & Activity**: `list_guest_conversations`, `get_guest_conversation`, `get_portfolio_analytics`.
- **Operations & Crew**: `get_property_os` (early check-in policy, turnover crew contacts, house notes, and early check-in requests).

### View and Change (`onstay:change`)
- **Blocked Dates**: `create_host_block`, `update_host_block`, `delete_host_block` (connected pricing hears about each change, as it does from the OnStay calendar).
- **Guest Questions**: `reply_to_guest_escalation`, `acknowledge_guest_escalation`, `resolve_guest_escalation`.
- **Concierge Knowledge**: `teach_concierge` (text facts, public web pages, or YouTube videos).
- **Operations**: `update_property_os_policy` (`off` or `ask_host`), `save_turnover_crew_contact`, `add_house_note`, `decline_early_check_in`.

## Security & Boundaries

- **Door access stays in OnStay**: Smart locks, door codes, and thermostats cannot be viewed or operated by connected apps.
- **Instant revocation**: Disconnect any connected app at any time in **Settings -> Integrations** on OnStay (`https://onstay.ai/settings?tab=integrations`).
- **Setup guide & Privacy**: [https://onstay.ai/mcp](https://onstay.ai/mcp) · [https://onstay.ai/privacy](https://onstay.ai/privacy)
