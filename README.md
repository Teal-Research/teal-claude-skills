# Teal Claude Skills

A central repository for Claude Skills markdown files used by the Teal team.

## What are Claude Skills?

Skills are markdown files that provide Claude with specialized knowledge, workflows, or instructions for specific tasks. They help Claude perform consistently across different team members' conversations.

## Repository Structure

```
teal-claude-skills/
├── skills/
│   ├── analytics/           # Amplitude, data analysis
│   ├── support/             # Intercom, Help Center content
│   ├── operations/          # Internal processes, workflows
│   └── product/             # Product-specific knowledge
├── CHANGELOG.md             # Track all skill updates
└── README.md                # You are here
```

## How to Use

### Finding a Skill

1. Browse the `skills/` folder or use GitHub's search
2. Click on the skill file you need
3. Click the "Raw" button to see the plain markdown

### Adding a Skill to Claude

1. Go to [claude.ai](https://claude.ai)
2. Navigate to **Settings** → **Skills** (or access via a Project)
3. Click **Add Skill** or **Create Skill**
4. Copy the markdown content from this repo and paste it
5. Save the skill

### Updating an Existing Skill

1. Check the [CHANGELOG.md](CHANGELOG.md) for recent updates
2. Find the updated skill file in this repo
3. In Claude, go to your Skills and find the matching skill
4. Replace the content with the updated version from this repo
5. Save

## Contributing

### Adding a New Skill

1. Create a new `.md` file in the appropriate `skills/` subfolder
2. Use the naming convention: `skill-name.md` (lowercase, hyphens)
3. Include a clear header describing what the skill does
4. Update `CHANGELOG.md` with the addition
5. Commit and push
6. Post in #team-tools (or your designated Slack channel)

### Updating an Existing Skill

1. Edit the skill file
2. Update `CHANGELOG.md` with what changed
3. Commit with a descriptive message
4. Push to main
5. Slack notification will auto-post (see setup below)

## Slack Notifications Setup

See [docs/slack-setup.md](docs/slack-setup.md) for instructions on connecting this repo to Slack for automatic update notifications.

## Current Skills

| Skill | Category | Description |
|-------|----------|-------------|
| [teal-analytics.md](skills/analytics/teal-analytics.md) | Analytics | Amplitude event schema, metrics, and analysis patterns |
| [intercom-article-generator.md](skills/support/intercom-article-generator.md) | Support | Generate Help Center articles for Teal |

---

**Questions?** Reach out in #team-tools or ping Emily.
