# Standard ROVO output contract

Use this structure so Slack and Confluence stay consistent across teams:

- `report_header`: `EOD Status - <project_key> - <YYYY-MM-DD>`
- `executive_summary`: 3-5 lines, decision-ready and non-technical
- `today_completed`: bullet list of major completed items
- `in_progress`: bullet list of meaningful in-flight work
- `risks_blockers`: explicit blocker/risk bullets with owner and next step
- `next_24h`: bullet list of planned next actions
- `channel_targets`: Slack channel(s) and Confluence destination
- `source_timestamp_utc`: report generation timestamp in UTC

## Paste-ready Confluence block template

```md
h2. EOD Status - <project_key> - <YYYY-MM-DD>

*Executive Summary*
<3-5 line crisp summary>

*Completed Today*
- ...

*In Progress*
- ...

*Risks / Blockers*
- ...

*Next 24 Hours*
- ...
```
