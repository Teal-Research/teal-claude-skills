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
5. **Screenshots** (optional) - Hosted image URLs to embed in the article

## API Configuration

- **API Endpoint:** `https://api.intercom.io/articles`
- **API Token:** `dG9rOjg1NTA5ZTcxXzliNDlfNDE4ZV84NDIzX2NkYWJjZWJkZTc1YzoxOjA=`
- **Author ID:** `7170316`
- **State:** Always use `draft` - never publish automatically

## Article Formatting Guidelines

### Structure

1. **Bold intro statement** - Open with: `<p><b>In this article, we'll cover [topic].</b></p>`
2. **Horizontal dividers** - Use `<hr>` between major sections
3. **H2 headers** - Clean section titles (e.g., `<h2>Section Name</h2>`)
4. **H3 subheaders** - For subsections within a major section
5. **Short paragraphs** - 2-3 sentences max, scannable
6. **Screenshots** - Embed after the relevant instruction or description
7. **Closing section** - End with `<h2>Where should I go from here?</h2>` linking to related articles

### HTML Elements

- Paragraphs: `<p>text</p>`
- Bold: `<b>text</b>`
- Links: `<a href="url">text</a>`
- Unordered lists: `<ul><li>item</li></ul>`
- Ordered lists: `<ol><li>step</li></ol>`
- Section dividers: `<hr>`
- Images: `<img src="url" alt="descriptive alt text">`

### Content Guidelines

- Write for job seekers using Teal
- Use "you" to address the reader directly
- Keep explanations practical and actionable
- Include pro tips where relevant
- Link to the Teal app features being discussed (e.g., `https://app.tealhq.com/job-search`)

### Style Notes

1. **No description subtitle** - Articles jump straight into content after the title
2. **Bold intro** - Always start with a bold statement explaining what the article covers
3. **Horizontal rules** - Use `<hr>` between every major H2 section
4. **Short paragraphs** - Maximum 2-3 sentences per paragraph
5. **Active voice** - Use "you" to address the reader directly
6. **Practical focus** - Emphasize actionable steps over theory
7. **Links in context** - Hyperlink feature names to their app URLs
8. **Consistent closing** - Always end with "Where should I go from here?" section
9. **Screenshots after text** - Place images immediately after the instruction or description they illustrate

## Example Article Structure

```html
<p><b>In this article, we'll cover how to use [feature] to [accomplish goal].</b></p>

<hr>

<h2>First Major Section</h2>

<p>Short paragraph explaining the concept. Keep it to 2-3 sentences maximum for scannability.</p>

<img src="https://i.imgur.com/XXXXXXX.png" alt="Description of what the screenshot shows">

<p>Another short paragraph if needed. Break up long explanations into multiple paragraphs.</p>

<hr>

<h2>Section with Steps</h2>

<p>To accomplish this task:</p>
<ol>
<li>First step</li>
<li>Second step</li>
<li>Third step</li>
</ol>

<img src="https://i.imgur.com/XXXXXXX.png" alt="Result after completing the steps">

<h3>Subsection If Needed</h3>

<p>Use H3 for subsections within a major section. Keep subsections brief.</p>

<hr>

<h2>Where should I go from here?</h2>

<p>We recommend checking out these articles next:</p>
<ul>
<li><a href="https://help.tealhq.com/en/articles/XXXXX">Related Article Title</a> - Brief description</li>
<li><a href="https://help.tealhq.com/en/articles/XXXXX">Another Related Article</a> - Brief description</li>
</ul>
```

## Screenshot Workflow

When articles need screenshots, follow this workflow:

### Step 1: Create Playwright Script

Generate a Node.js script using Playwright that:
- Launches a browser in non-headless mode
- Navigates to the relevant Teal pages
- Pauses for user login and manual interactions
- Captures screenshots at key interaction points

**Script template:**

```javascript
const { chromium } = require('playwright');
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

function prompt(question) {
  return new Promise(resolve => {
    rl.question(question, resolve);
  });
}

(async () => {
  console.log('🚀 Launching browser for Teal screenshots...\n');
  
  const browser = await chromium.launch({ 
    headless: false,
    slowMo: 100
  });
  
  const context = await browser.newContext({
    viewport: { width: 1512, height: 900 }
  });
  
  const page = await context.newPage();

  await page.goto('https://app.tealhq.com');
  
  await prompt('👤 Please log in to Teal in the browser window.\n   Press Enter when logged in... ');

  // Navigate to feature page
  console.log('\n📍 Navigating to [FEATURE]...');
  await page.goto('https://app.tealhq.com/[FEATURE-PATH]');
  await page.waitForLoadState('domcontentloaded');
  await page.waitForTimeout(2000);

  // Screenshot 1: Initial state
  console.log('📸 Screenshot 1: [Description]');
  await page.screenshot({ path: 'screenshot_01_[name].png' });

  // Interactive screenshots - prompt user to perform action, then capture
  await prompt('\n👆 [Instruction for user action].\n   Press Enter when ready... ');
  await page.screenshot({ path: 'screenshot_02_[name].png' });

  // Continue pattern for additional screenshots...

  console.log('\n✅ Done! Screenshots saved.');
  
  await prompt('\nPress Enter to close browser... ');
  rl.close();
  await browser.close();
})();
```

**Key patterns:**
- Use `waitForLoadState('domcontentloaded')` instead of `networkidle` (more reliable)
- Add `waitForTimeout(2000)` after navigation for dynamic content
- Use interactive prompts for actions that require user input (dropdowns, modals)
- Name screenshots with numbered prefixes for ordering: `screenshot_01_`, `screenshot_02_`, etc.

### Step 2: User Runs Script

Instruct the user to:

```bash
cd /Users/emilywoodward/playwright-script
node capture_[feature]_screenshots.js
```

### Step 3: User Uploads Screenshots

Screenshots must be hosted externally. Recommend:
- **Imgur** (free, easy): imgur.com - drag & drop images, copy direct links
- **Cloudinary** (free tier): cloudinary.com
- **AWS S3** (if available)

Direct links should look like: `https://i.imgur.com/XXXXXXX.png`

### Step 4: Embed in Article

Once the user provides hosted URLs, embed screenshots in the article HTML:

```html
<img src="https://i.imgur.com/XXXXXXX.png" alt="Descriptive alt text for accessibility">
```

**Placement guidelines:**
- Place screenshots immediately AFTER the text describing what's shown
- After step-by-step instructions, show the result
- After "click X" instructions, show the UI element or resulting state

**Alt text guidelines:**
- Describe what the screenshot shows, not what action to take
- Be specific: "Settings panel showing Send Alerts toggle" not "Settings panel"
- Keep under 125 characters when possible
- Don't start with "Image of" or "Screenshot of"

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

## Common Teal App Links

- Job Search: `https://app.tealhq.com/job-search`
- Job Tracker: `https://app.tealhq.com/jobs`
- Resume Builder: `https://app.tealhq.com/resumes`
- Companies Tracker: `https://app.tealhq.com/companies`
- Contacts Tracker: `https://app.tealhq.com/contacts`

## Common Related Articles

- Getting Started: Job Tracker: `https://help.tealhq.com/en/articles/9508859-getting-started-job-tracker`
- Getting Started: Resume Builder: `https://help.tealhq.com/en/articles/9508872-getting-started-resume-builder`
- Getting Started: Resume Designer: `https://help.tealhq.com/en/articles/9955498-getting-started-resume-designer`
- Getting Started: Contacts Tracker: `https://help.tealhq.com/en/articles/9955505-getting-started-contacts-tracker`
- Getting Started: Companies Tracker: `https://help.tealhq.com/en/articles/9955511-getting-started-companies-tracker`
- Using AI: Bullets: `https://help.tealhq.com/en/articles/9519206-using-ai-bullets`
- Using Teal's Job Search: `https://help.tealhq.com/en/articles/13456939-using-teal-s-job-search`

## Complete Workflow

1. Collect required information (title, source content)
2. **If screenshots needed:**
   a. Generate Playwright script for the specific feature
   b. User runs script to capture screenshots
   c. User uploads to Imgur and provides direct URLs
   d. Embed URLs in article HTML
3. Transform source content into formatted HTML following Teal's style
4. Generate the shell script with the article content
5. Present both files to the user
6. Remind user the article will be created as a draft for review before publishing
