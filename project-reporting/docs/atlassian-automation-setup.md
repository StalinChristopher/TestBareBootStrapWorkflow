# Atlassian automation setup (manual)

Complete these steps in Atlassian Cloud after the GitHub workflow is installed.

## 1. Create incoming webhook rule

1. Open **Jira** → **Project settings** → **Automation** (or global Automation).
2. Create a rule with trigger: **Incoming webhook**.
3. Copy the webhook URL — this becomes GitHub secret `ROVO_AUTOMATION_WEBHOOK_URL`.
4. If Atlassian provides a webhook token, store it as `ROVO_AUTOMATION_WEBHOOK_TOKEN`.

## 2. Parse the signal payload

The GitHub workflow sends JSON:

```json
{
  "report_date": "YYYY-MM-DD",
  "run_time_utc": "ISO-8601",
  "project_key": "ABC",
  "slack_channel": "#channel-name",
  "request_source": "github_actions_daily_schedule",
  "prompt_hint": "Create a same-day crisp executive end-of-day status report..."
}
```

Use `project_key` and `slack_channel` from the payload to scope ROVO and route Slack delivery.

## 3. Invoke ROVO agent

Add an action to run the ROVO agent (or your team's equivalent) with:

- Jira project: `{{webhookData.project_key}}`
- Prompt context: `{{webhookData.prompt_hint}}`

## 4. Map ROVO output to Slack

Format output per [rovo-output-contract.md](./rovo-output-contract.md):

- `report_header`, `executive_summary`, `today_completed`, `in_progress`
- `risks_blockers`, `next_24h`, `channel_targets`, `source_timestamp_utc`

Post to the Slack channel from `slack_channel` in the webhook payload.

## 5. Optional Confluence append

Use the Confluence template in `rovo-output-contract.md` to append an EOD status page.

## 6. Test

1. Set GitHub secrets and variables in the project repo.
2. Run **Daily Project Report** via `workflow_dispatch` in GitHub Actions.
3. Confirm the automation rule fires and Slack receives the report.

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Webhook not received | Verify `ROVO_AUTOMATION_WEBHOOK_URL` secret; check workflow run logs |
| 401/403 on webhook | Set `ROVO_AUTOMATION_WEBHOOK_TOKEN` if required by your rule |
| Wrong Jira project | Update `ROVO_TARGET_PROJECT_KEY` variable in GitHub |
| Wrong Slack channel | Update `ROVO_TARGET_SLACK_CHANNEL` variable in GitHub |
