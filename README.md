# em-pulse

*Daily Intelligence for Engineers*

## What This Is

An AI-powered daily briefing system that integrates calendar, JIRA, Slack, and email to give you a clear picture of your day. Saves time on information gathering and context switching.

## Quick Start

1. **Install Required Tools:**
  - **gog** (Google CLI): [https://github.com/openclaw/gogcli](https://github.com/openclaw/gogcli)
  - **Atlassian MCP**: [https://github.com/atlassian/atlassian-mcp-server](https://github.com/atlassian/atlassian-mcp-server)  
  - **Slack MCP**: [https://github.com/redhat-community-ai-tools/slack-mcp](https://github.com/redhat-community-ai-tools/slack-mcp)
2. **Hand Off to Claude:**
  - Give your Claude assistant the `SETUP.md` file
  - Say: *"Set up my daily briefing assistant using this guide"*
  - Follow the customization prompts
3. **Test:**
  - Say "brief me" to get your first briefing
  - Verify all data sources are working



## What You Get

**Daily Morning Briefing:**

- Your agenda with meeting prep context
- Recent activity across JIRA/Slack/email since last briefing
- Meeting preparation with relevant background
- Heads-up on things happening across the team/org that may affect your work

**Persistent Context:**

- Maintains memory of ongoing work items and focus areas
- Tracks what you're working on across sessions
- Remembers key collaborators and communication patterns

**Deep Dive Capability:**

- Ask follow-up questions on any topic: "Dig deeper into [topic]"
- Get detailed analysis with full context
- Maintain conversation thread across multiple briefings



## Privacy & Security

- All data remains in your local environment
- No external data sharing
- Configure least-privilege access to required systems
- Review auto-generated memory files for sensitive content



## Value Delivered

- **Time Savings**: Less time on manual information gathering
- **Context Retention**: Stay on top of ongoing work across tools  
- **Proactive Detection**: Early identification of blockers and issues
- **Meeting Efficiency**: Show up prepared with relevant context for every meeting



## Customization

During setup, you'll configure:

- **JIRA integration:** Your Cloud ID and issue filtering (project, component, sprint)
- **Slack monitoring:** Team channels, project channels, and announcements  
- **Email contacts:** Manager and key collaborator email addresses
- **Work context:** Current projects, key collaborators, and focus areas

The system will guide you through configuring these during the setup process.



---

**Ready to get started?** Give `SETUP.md` to your Claude assistant and say "set up em-pulse for me".
