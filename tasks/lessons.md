# Lessons

Format: [date] | what went wrong | rule to prevent it

This file is read at the start of every session per global CLAUDE.md workflow. Add an entry any time an approach is corrected so the next session doesn't repeat it.

[2026-07-25] | Assumed the already-authenticated Notion/Slack MCP connectors pointed at the real client workspace and spent two recon agents confirming SFP data there before checking; both were sandbox/unrelated accounts | Verify connector workspace identity (Slack team domain, Notion top-level page/database titles) before trusting any connector-derived data as real, especially before spending agent calls on data-dependent recon.
