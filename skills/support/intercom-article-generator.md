# Intercom Article Generator Skill

> **Version:** 1.0
> **Last Updated:** 2025-01-21
> **Category:** Support

## Overview

Generate Intercom Help Center articles for Teal.

## When to Use

Use when asked to:
- Create, write, or draft an Intercom article
- Write a help center article
- Draft a knowledge base article
- Turn a transcript into an article

## Trigger Phrases

- "Create an Intercom article"
- "Write a help center article"
- "Draft an article about [feature]"
- "Turn this transcript into an article"

---

## Skill Content

<!-- 
Replace everything below this line with your actual intercom-article-generator skill content.
Copy from your existing skill in Claude.
-->

---
name: intercom-article-generator
description: Generate Intercom Help Center articles for Teal. Use when asked to create, write, or draft an Intercom article, help center article, or knowledge base article. Triggers on requests like "create an Intercom article", "write a help center article", "draft an article about [feature]", or "turn this transcript into an article".
---

# Intercom Article Generator

Generate Help Center articles for Teal's Intercom knowledge base.

## Required Information

Before generating an article, collect the following from the user:

1. **Article title** - The title for the article
2. **Source content** - The content informing the article (video transcript, HTML, notes, etc.)
3. **Target audience** (optional) - Who the article is for (default: Teal users)
4. **Related articles** (optional) - Links to related Help Center articles for the "Where should I go from here?" section

## API Configuration

- **API Endpoint:** `https://api.intercom.io/articles`
- **API Token:** `dG9rOjg1NTA5ZTcxXzliNDlfNDE4ZV84NDIzX2NkYWJjZWJkZTc1YzoxOjA=`
- **Author ID:** `7170316`
- **State:** Always use `draft` - never publish automatically

## Article Formatting Guidelines

Follow Teal's Help Center formatting style. See `references/formatting-guide.md` for detailed examples.

### Structure

1. **Bold intro statement** - Open with: `<p><b>In this article, we'll cover [topic].</b></p>`
2. **Horizontal dividers** - Use `<hr>` between major sections
3. **H2 headers** - Clean section titles (e.g., `<h2>Section Name</h2>`)
4. **H3 subheaders** - For subsections within a major section
5. **Short paragraphs** - 2-3 sentences max, scannable
6. **Closing section** - End with `<h2>Where should I go from here?</h2>` linking to related articles

### HTML Elements

- Paragraphs: `<p>text</p>`
- Bold: `<b>text</b>`
- Links: `<a href="url">text</a>`
- Unordered lists: `<ul><li>item</li></ul>`
- Ordered lists: `<ol><li>step</li></ol>`
- Section dividers: `<hr>`

### Content Guidelines

- Write for job seekers using Teal
- Use "you" to address the reader directly
- Keep explanations practical and actionable
- Include pro tips where relevant
- Link to the Teal app features being discussed (e.g., `https://app.tealhq.com/job-search`)

## Creating the Article

Generate a shell script that creates the article via the Intercom API:

```bash
#!/bin/bash
INTERCOM_TOKEN="dG9rOjg1NTA5ZTcxXzliNDlfNDE4ZV84NDIzX2NkYWJjZWJkZTc1YzoxOjA="

curl -X POST "https://api.intercom.io/articles" \
  -H "Authorization: Bearer ${INTERCOM_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "Intercom-Version: 2.11" \
  -d '{
    "title": "ARTICLE_TITLE",
    "author_id": 7170316,
    "state": "draft",
    "body": "HTML_CONTENT_HERE"
  }'
```

### Script Output

1. Save the script to `/mnt/user-data/outputs/create_intercom_article.sh`
2. Also save the HTML content separately to `/mnt/user-data/outputs/intercom_article_content.html` for easy review
3. Remind user to run: `bash ./create_intercom_article.sh`

## Workflow

1. Collect required information (title, source content)
2. Read `references/formatting-guide.md` for style examples
3. Transform source content into formatted HTML following Teal's style
4. Generate the shell script with the article content
5. Present both files to the user
6. Remind user the article will be created as a draft for review before publishing
