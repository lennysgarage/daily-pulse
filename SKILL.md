---
name: daily-briefing
description: Comprehensive daily briefing with calendar, JIRA activity, Slack updates, and email alerts. Use when user asks for "daily briefing", "brief me", "brief me on my day", or similar morning/EOD briefing requests.
---

# Daily Briefing

Comprehensive daily briefing with calendar, JIRA activity, Slack updates, and email alerts.

## When to use this skill

When user requests:
- "brief me"
- "daily briefing"
- "brief me on my day"  
- "give me my briefing"
- "morning briefing"
- "brief me eod" (end of day)

## Implementation

1. **Track timing:** Update "last briefing request" timestamp in memory
2. **Calculate timeframe:** Use stored timestamp from previous briefing to current time
3. **Gather data:**
   - Calendar: `gog calendar events` from last briefing to now
   - Email: `gog mail search` from last briefing to now (key people + "action required")
   - JIRA: Search my issues from last briefing timeframe
   - Slack: Monitor specified channels from last briefing timeframe

4. **Format output** based on briefing type (morning vs EOD)

## Data Sources

**Calendar:** `gog calendar events` with date ranges

**Email:** `gog mail search` - Focus on key contacts and "action required" messages
- Target contacts: [YOUR_MANAGER_EMAIL], [OTHER_KEY_CONTACTS]
- Search patterns: "action required", key contact names

**JIRA:** Use Atlassian MCP with cloudId `[YOUR_JIRA_CLOUD_ID]` (format: 12345678-1234-1234-1234-123456789abc) and filters:
- Issues assigned to me
- High priority items in my project/sprint
- New blockers affecting my work
- Critical/Major severity in my area
- Recently completed items

**Configure your filter - examples:**
```jql
# Your own tickets
assignee = currentUser()

# By project and sprint
project = "[YOUR_PROJECT]" AND sprint in openSprints()

# By component
component = "[YOUR_COMPONENT]" AND assignee = currentUser()
```

**Slack Channels - customize for your organization:**

**Team Channels:**
- [your-team-channel]
- [your-team-technical-discussions]

**Project/Working Group Channels:**
- [cross-functional-project-channels]
- [technical-working-groups]

**Announcement Channels:**
- [engineering-announcements]
- [company-announcements]

**DM Monitoring:**
- [YOUR_MANAGER_NAME]
- [KEY_COLLABORATOR_NAMES]

**Configuration Notes:**
- Replace all [PLACEHOLDER] values with your specific details
- Add/remove channels based on your needs
- Ensure you have access permissions for all monitored channels

## Morning Briefing Format

```
# [Day], [Date] Daily Brief

## Your Agenda Today
[Calendar events with clock emoji for meeting time rounded to nearest half-hour, in local time]
**CRITICAL:** Always include full agenda section. Never show "No meetings" without careful verification.
**EXCLUDE:** Do not mention or track "Heads Down" recurring time blocks.
**SHOW:** Distinguish between completed meetings and remaining meetings based on current time.

## Recent Activity (Since Last Briefing)
**My JIRA Updates:** [Assigned issues, status changes, new comments, blockers]
**Slack Signals:** [Key updates from monitored channels - focus on work-related content only]  
**Email Alerts:** [Important messages requiring action]

## Action Items for Today
**Ongoing Priorities:** [Persistent items until marked complete - confirm before adding/removing]
**Daily Focus:** [Generated based on calendar/context and current work]

## Meeting Prep
[Context for each meeting from JIRA/Slack/recent activity with specific prep recommendations]

## Heads Up
[Notable things happening across the team or org that may affect your work - deployments, incidents, announcements, dependency changes]

[Closing question about priorities or areas needing deeper analysis]
```

## EOD Briefing Format

```
# [Day] EOD Summary

## Today's Accomplishments
[Summary of business day activity from current business day]

## Tomorrow's Priorities  
[Preview of next day's calendar + key prep items]

## Action Items Status
[Updates on ongoing items, newly completed items]

## Overnight/Tomorrow Morning Prep
[Any urgent items to address]
```

## Action Item Management
- **Persistence:** Maintain ongoing list in memory
- **Addition:** ALWAYS ask permission before adding new items - NEVER add unilaterally
- **Removal:** ALWAYS ask permission before removing items
- **Completion:** Mark done when user confirms, notify user
- **Carryover:** Continue until explicitly told otherwise or user confirms completion
- **Scope:** Only track items that are your direct responsibility

## Meeting Prep Logic
- Search JIRA for relevant tickets involving meeting context
- Check recent Slack conversations related to meeting topics
- Flag any blockers or urgent items for discussion

## Clock Emoji Mapping (Local Time)
Round to nearest half-hour:
- :00-:14 → hour emoji
- :15-:44 → half-hour emoji
- :45-:59 → next hour emoji

## Steps

1. **Update timestamp:** Edit memory/reference_briefing_timestamp.md with current time
2. **Get calendar:** Run `gog calendar events` and parse carefully for completed/remaining meetings
3. **Check email:** Run `gog mail search` for key people and "action required"
4. **Query JIRA:** Use Atlassian MCP to search my issues with detailed analysis
5. **Check Slack:** Use Slack MCP to search monitored channels focusing on work-related signals
6. **Synthesize:** Combine data into a clear picture of the day
7. **Format output:** Use appropriate briefing format
8. **Update action items:** Review and update ongoing priorities with confirmation

## Execution Notes

This skill automatically triggers agent-based execution due to its complexity:
- Multiple data sources require parallel collection
- Background execution allows continued work while briefing is prepared
- Typical completion time: 2-5 minutes depending on data volume
