# Slack Notifications Setup

This guide walks through connecting the `teal-claude-skills` GitHub repository to Slack so the team gets notified when skills are updated.

## Option 1: GitHub + Slack Integration (Recommended)

This is the official GitHub/Slack integration and provides the most reliable notifications.

### Step 1: Install the GitHub App in Slack

1. Go to your Slack workspace
2. Click on **Apps** in the left sidebar
3. Search for **GitHub**
4. Click **Add** to install the GitHub app
5. Follow the prompts to authorize

### Step 2: Connect Your GitHub Account

In any Slack channel, type:
```
/github signin
```

Follow the link to authenticate with your GitHub account.

### Step 3: Subscribe to the Repository

In the Slack channel where you want notifications (e.g., `#team-tools`), type:

```
/github subscribe owner/teal-claude-skills
```

Replace `owner` with your GitHub username or organization name.

### Step 4: Customize Notifications

By default, you'll get notifications for issues, pulls, commits, releases, and deployments. For a skills repo, you probably only want **commits** and maybe **releases**.

To see current subscriptions:
```
/github subscribe list
```

To unsubscribe from noisy events:
```
/github unsubscribe owner/teal-claude-skills issues pulls deployments releases
```

To only get push/commit notifications:
```
/github subscribe owner/teal-claude-skills commits
```

### What Notifications Look Like

When someone pushes to the repo, Slack will post something like:

> **[teal-claude-skills]** 1 new commit to main
> `abc1234` Updated teal-analytics.md with webinar events - Emily

---

## Option 2: Slack Webhook (More Control)

If you want more customized notifications, you can use GitHub Actions with a Slack webhook.

### Step 1: Create a Slack Webhook

1. Go to [api.slack.com/apps](https://api.slack.com/apps)
2. Click **Create New App** → **From scratch**
3. Name it "Claude Skills Updates" and select your workspace
4. Go to **Incoming Webhooks** → Enable it
5. Click **Add New Webhook to Workspace**
6. Select the channel (e.g., `#team-tools`)
7. Copy the webhook URL

### Step 2: Add Webhook to GitHub Secrets

1. Go to your GitHub repo → **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Name: `SLACK_WEBHOOK_URL`
4. Value: Paste your webhook URL
5. Click **Add secret**

### Step 3: Create GitHub Action

Create a file at `.github/workflows/slack-notify.yml` in your repo:

```yaml
name: Notify Slack on Skill Updates

on:
  push:
    branches:
      - main
    paths:
      - 'skills/**'
      - 'CHANGELOG.md'

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 2

      - name: Get changed files
        id: changed
        run: |
          FILES=$(git diff --name-only HEAD~1 HEAD -- 'skills/' | tr '\n' ', ' | sed 's/,$//')
          echo "files=$FILES" >> $GITHUB_OUTPUT

      - name: Send Slack notification
        uses: slackapi/slack-github-action@v1.26.0
        with:
          payload: |
            {
              "blocks": [
                {
                  "type": "header",
                  "text": {
                    "type": "plain_text",
                    "text": "📝 Claude Skills Updated",
                    "emoji": true
                  }
                },
                {
                  "type": "section",
                  "text": {
                    "type": "mrkdwn",
                    "text": "*Files changed:*\n${{ steps.changed.outputs.files }}\n\n*Commit:* ${{ github.event.head_commit.message }}\n*By:* ${{ github.actor }}"
                  }
                },
                {
                  "type": "actions",
                  "elements": [
                    {
                      "type": "button",
                      "text": {
                        "type": "plain_text",
                        "text": "View Changes"
                      },
                      "url": "${{ github.event.head_commit.url }}"
                    },
                    {
                      "type": "button",
                      "text": {
                        "type": "plain_text",
                        "text": "View Changelog"
                      },
                      "url": "${{ github.server_url }}/${{ github.repository }}/blob/main/CHANGELOG.md"
                    }
                  ]
                }
              ]
            }
        env:
          SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
          SLACK_WEBHOOK_TYPE: INCOMING_WEBHOOK
```

### What This Notification Looks Like

```
📝 Claude Skills Updated
━━━━━━━━━━━━━━━━━━━━━━
Files changed: skills/analytics/teal-analytics.md

Commit: Added webinar conversion events
By: emily

[View Changes]  [View Changelog]
```

---

## Recommendation

**Start with Option 1** (GitHub Slack app) — it's simpler to set up and maintain. 

Move to **Option 2** (webhook + GitHub Action) if you want:
- Custom message formatting
- Notifications only for specific file changes
- Buttons/links in the notification
- More control over when notifications fire

---

## Testing

After setup, make a small change to any skill file (like adding a comment), commit, and push. You should see the notification in Slack within a minute or two.
