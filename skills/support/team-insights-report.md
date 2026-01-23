---
name: team-insights-report
description: "Generate casual, team-friendly insight reports from product data analysis. Use when asked to create reports, summaries, or analyses that need to be shared with the team — especially for churn analysis, feature feedback, support ticket patterns, user behavior insights, or any cross-functional data synthesis. Triggers on requests like 'create a report for the team', 'summarize this for staff', 'make this shareable', 'write up these findings', or 'help me explain this data to the team'."
---

# Team Insights Report Generator

Create concise, conversational reports that translate data analysis into team-friendly narratives.

## Core Philosophy

**Write like you're explaining to a smart colleague over coffee, not presenting to a board.**

- Lead with the story, not the numbers
- Use tables for comparison, not for showing off data
- One key insight per section
- End with clear "what to do" actions

## Report Structure

```markdown
# 🚨 [Punchy Headline That Captures The Insight]

**TL;DR:** [One sentence summary — what did we find and why does it matter?]

---

## What We Found

[Brief context: what data sources, what time period, why we looked]

---

## 🎯 The Big Picture

[The single most important finding, stated simply]

---

## [2-4 Supporting Sections]

[Each section answers ONE question with light data support]

---

## ✅ What We Should Do

### Right now
[1-3 immediate actions]

### Soon
[2-3 short-term actions]

### Strategic
[1-3 longer-term considerations]

---

*Data: [Brief source attribution]*
```

## Writing Guidelines

### Tone
- Conversational, not corporate
- "We found" not "Analysis indicates"
- "This tells us" not "This data suggests"
- Use contractions naturally
- Questions are okay: "But why are they canceling?"

### Numbers
- Round aggressively (47%, not 47.3%)
- Use comparisons over absolutes ("half as likely" vs "3.4% vs 6.5%")
- Limit to 3-5 key stats per report
- Put detailed numbers in tables, not prose

### Tables
Use for:
- Before/after or group comparisons
- Feature adoption gaps
- Action items with owners
- Pain points with example quotes

Avoid:
- Tables with only 2 columns of numbers
- More than 6 rows without a clear reason
- Decimal precision beyond what matters

### Headlines & Callouts
- Section headers should be scannable questions or statements
- Use emoji sparingly but effectively (🎯 🚨 💡 ✅ ⚠️)
- Blockquotes for key stats or user quotes

## Analysis Types

### Churn/Retention Analysis
Focus on: Who is leaving, when they leave, what they didn't do
Key question: "What separates churners from retained users?"
Template sections:
- Who Is Canceling?
- The Behavior Gap (churners vs retained)
- The Speed of Regret (time-to-cancel patterns)
- What Users Are Saying
- What To Do

### Feature Feedback Analysis  
Focus on: What's working, what's broken, what's missing
Key question: "What do users actually want vs what we think they want?"
Template sections:
- Top Requests (with volume)
- Pain Points (with quotes)
- What's Working Well
- Prioritized Recommendations

### Support Ticket Analysis
Focus on: Volume drivers, repeat issues, gaps in self-service
Key question: "Why are people contacting support instead of succeeding on their own?"
Template sections:
- Where Volume Is Coming From
- The Real Issues (behind the tickets)
- Quick Wins
- Systemic Fixes Needed

### User Segment Analysis
Focus on: How different groups behave differently
Key question: "Who are our best users and what makes them different?"
Template sections:
- Segment Definitions
- Behavioral Differences
- Conversion/Retention by Segment
- Implications for Product/Marketing

## Data Source Integration

### When combining Amplitude + Intercom
- Amplitude = what users DID (behavioral truth)
- Intercom = what users SAID (qualitative context)
- Lead with behavior patterns, support with user quotes
- Note data gaps honestly ("52% of users were untagged")

### When using Amplitude alone
- Focus on comparison: segments, time periods, feature adoption
- Use funnels to show drop-off points
- Call out statistical significance only if relevant

### When using Intercom alone
- Categorize by intent, not by topic tags
- Pull representative quotes (anonymized)
- Note volume and trends

## Output Format

**Default: Markdown (.md)**
- Notion-compatible
- Easy to paste into Slack/docs
- Version-control friendly

**When to use .docx instead:**
- Formal stakeholder presentations
- External sharing
- Print requirements

## Example Transformations

### ❌ Too data-heavy
"Analysis of 2,762 cancellation events over a 30-day period reveals that users who triggered the subscription:cancelation_scheduled event demonstrated a 3.4% rate of parsing_job_started events compared to a 6.5% baseline rate among the general subscriber population (n=10,037), representing a -48% differential."

### ✅ Team-friendly
"Cancelers barely touched the product. Only 3% imported a resume, compared to 7% of users who stuck around. They're paying for features they never try."

### ❌ Too vague
"Users are having issues with the product and many are canceling."

### ✅ Team-friendly  
"47% of support conversations are cancel requests. The median time from purchase to cancel? 35 minutes. They're not unhappy with Teal — they never really experienced it."
