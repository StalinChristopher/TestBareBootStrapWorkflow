# GitHub Actions configuration (ROVO mode)

Set these repository settings in the target project repo:

| Type | Name | Purpose |
|------|------|---------|
| Secret | `ROVO_AUTOMATION_WEBHOOK_URL` | Incoming webhook for Atlassian automation rule |
| Secret (optional) | `ROVO_AUTOMATION_WEBHOOK_TOKEN` | `X-Automation-Webhook-Token` header value |
| Variable | `ROVO_TARGET_PROJECT_KEY` | Jira project key (for example, `ABC`) |
| Variable | `ROVO_TARGET_SLACK_CHANNEL` | Slack channel (for example, `#channel-name`) |

If `ROVO_AUTOMATION_WEBHOOK_URL` is missing, the workflow still runs and publishes an execution summary but skips webhook delivery.

Never commit secret values to the repository.
