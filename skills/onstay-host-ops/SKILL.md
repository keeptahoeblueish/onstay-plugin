---
name: onstay-host-ops
description: >-
  Operate an OnStay host account through the OnStay MCP server: inspect homes,
  check calendars and blocked dates, answer or close guest questions waiting for
  the host, teach a home's concierge new facts or guides, and manage early
  check-in and turnover crew settings. Use whenever the user asks about their
  OnStay properties, stays, blocked dates, guest conversations, concierge
  knowledge, or turnover operations.
---

# OnStay Host Operations

Use the `onstay` MCP server tools (`onstay_onstay_*`) to inspect and manage the
signed-in host's OnStay portfolio safely.

## Core Principles

1. **Resolve the home first**: Call `list_properties` when you do not yet have a
   home's UUID (`propertyId`). Never guess UUIDs.
2. **Confirm before mutating**: Tools marked destructive (`create_host_block`,
   `update_host_block`, `delete_host_block`, `reply_to_guest_escalation`,
   `acknowledge_guest_escalation`, `resolve_guest_escalation`,
   `teach_concierge`, `update_property_os_policy`,
   `save_turnover_crew_contact`, `add_house_note`, `decline_early_check_in`)
   change live property calendars, message guests, or update operations
   settings. State the exact home, dates, or message text clearly before
   executing a change unless the host already gave exact details and asked you
   to run it.
3. **Guest anonymity**: Guest conversations in OnStay are anonymous by default.
   Do not invent or attach reservation holder names to guest conversation
   threads.
4. **Door access stays in OnStay**: Smart locks, door codes, thermostats, Wi-Fi
   passwords, reservation edits, and approving early check-in requests are
   managed directly in the OnStay app (`https://onstay.ai`), never through MCP.

## Common Workflows

### 1. Daily Inbox & Escalation Triage
1. Call `list_properties` and `list_guest_conversations` to find open guest
   questions waiting for the host.
2. For each conversation with an open question, call `get_guest_conversation`
   to retrieve the full transcript and each open case's `caseId` and `version`.
3. Draft a concise, hospitable reply for the host to review. Once confirmed:
   - Call `reply_to_guest_escalation` (passing `conversationId`, `caseId`,
     `body`, and `version`) to send the answer to the guest.
   - If the answer states a reusable property fact (for example, where beach
     towels or spare firewood are stored), offer to call `teach_concierge` so
     the home's concierge knows it next time.
   - Use `acknowledge_guest_escalation` or `resolve_guest_escalation` when an
     issue was handled offline without sending a message.

### 2. Calendar Inspection & Owner Date Blocks
1. Call `get_calendar` with `propertyId`, `dateFrom`, and `dateTo` (`YYYY-MM-DD`)
   to check stays and blocked dates before proposing or creating a block.
2. Only host-created blocks (`eventType: "host_block"`) can be added, moved, or
   removed via `create_host_block`, `update_host_block`, and
   `delete_host_block`. Connected dynamic pricing hears about each change
   automatically, as it does from the OnStay calendar.

### 3. Teaching the Concierge & Turnover Operations
- **Teach facts, pages, or videos**: Call `teach_concierge` with `type: "text"`
  (`selectionText`), `type: "page"` (`sourceUrl`), or `type: "video"`
  (`youtubeUrl`).
- **Early check-in & crew**: Call `get_property_os` to inspect early check-in
  rules, turnover crew contacts, house notes, and pending early check-in
  requests. You may set `earlyCheckInMode` to `"off"` or `"ask_host"`, save crew
  contacts (`save_turnover_crew_contact`), add house notes (`add_house_note`),
  or decline a pending early check-in (`decline_early_check_in`). Direct the
  host to OnStay if they want to approve an early check-in or configure
  automatic early check-in fees.
