# Project reporting — GitHub secrets & variables checklist

Configure these in **GitHub → Settings → Secrets and variables → Actions** for `StalinChristopher/TestBareBootStrapWorkflow`.

Do **not** commit secret values to this repository.

## Project-specific values

| Setting | Value |
|---------|-------|
| Jira project key | `ROC` |
| Slack channel | `#test-reporting-agent` |
| Schedule | Mon–Fri 9:00 AM IST (`30 3 * * 1-5` UTC) |

## GitHub Actions secrets

| Secret | Required | Purpose |
|--------|----------|---------|
| `ROVO_AUTOMATION_WEBHOOK_URL` | Yes | Incoming webhook URL from your Atlassian Automation rule |
| `ROVO_AUTOMATION_WEBHOOK_TOKEN` | Optional | `X-Automation-Webhook-Token` header value, if your rule requires it |

## GitHub Actions variables

| Variable | Value | Purpose |
|----------|-------|---------|
| `ROVO_TARGET_PROJECT_KEY` | `ROC` | Jira project key passed in the webhook payload |
| `ROVO_TARGET_SLACK_CHANNEL` | `#test-reporting-agent` | Slack channel passed in the webhook payload |

## Atlassian setup (manual)

Follow [atlassian-automation-setup.md](./docs/atlassian-automation-setup.md):

1. Create an **Incoming webhook** automation rule in Jira.
2. Copy the webhook URL → GitHub secret `ROVO_AUTOMATION_WEBHOOK_URL`.
3. Configure the ROVO agent scoped to Jira project `ROC`.
4. Map ROVO output to Slack per [rovo-output-contract.md](./docs/rovo-output-contract.md).
5. Optionally append to Confluence using the template in that doc.

## Validate

1. Set all secrets and variables above in GitHub.
2. Run **Daily Project Report** via **workflow_dispatch** in Actions.
3. Confirm the automation rule fires and `#test-reporting-agent` receives the report.

If `ROVO_AUTOMATION_WEBHOOK_URL` is not set, the workflow still runs but skips webhook delivery (see run summary).
