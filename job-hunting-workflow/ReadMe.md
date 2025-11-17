# 🚀 ULTIMATE AI Job Hunter - Enterprise Edition

<div align="center">

![n8n](https://img.shields.io/badge/n8n-Workflow-EA4B71?style=for-the-badge&logo=n8n)
![AI Powered](https://img.shields.io/badge/AI-Powered-00D9FF?style=for-the-badge&logo=openai)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)

**Fully automated AI-powered job hunting system that finds, analyzes, and applies to jobs while you sleep**

[Features](#-features) • [Quick Start](#-quick-start) • [Setup](#%EF%B8%8F-setup-guide) • [Architecture](#-architecture) • [FAQ](#-faq)

</div>
<img width="1489" height="479" alt="image" src="https://github.com/user-attachments/assets/feeccdb3-05da-4fb4-a9f7-1f6cd699f624" />


## 🎯 Overview

The **ULTIMATE AI Job Hunter** is a sophisticated n8n workflow that automates the entire job search process using multiple AI agents and integrations. It runs every 6 hours to:

1. 🔍 **Scrape** jobs from 4+ job boards
2. 🤖 **Analyze** each position with AI (Gemini)
3. 📊 **Score** matches based on your profile
4. 📝 **Generate** tailored resumes & cover letters
5. 📧 **Find** hiring manager contacts
6. 💬 **Send** personalized cold emails
7. 📈 **Track** everything in Google Sheets
8. 🔔 **Notify** you on Slack with top matches

---

## ✨ Features

### 🤖 Multi-Agent AI System
- **Agent 1**: Initial screening (role match, seniority, visa-friendly, salary)
- **Agent 2**: Skills analysis (matches your tech stack)
- **Agent 3**: Deep analysis with Gemini (ATS score, cultural fit, interview prep)
- **Agent 4**: Company research (funding, culture, tech stack, Glassdoor)
- **Agent 5**: Resume generation (tailored for each job)
- **Agent 6**: Cold email writing (personalized outreach)
- **Agent 7**: Interview prep (questions, topics, negotiation points)

### 📊 Data Sources
- ✅ Adzuna API (100 jobs/search)
- ✅ Remotive (remote-first jobs)
- ✅ Arbeitnow (EU/international)
- ✅ FindWork (dev-focused)
- ✅ Custom sources (easily add more!)

### 🎯 Smart Filtering
- **Composite scoring** (screening + skills + AI analysis)
- **Configurable threshold** (default: 80%)
- **Deduplication** (removes duplicate listings)
- **Salary filtering** (respects your minimum)
- **H1B-friendly detection** (filters citizen-only jobs)

### 📧 Contact Discovery
- **Hunter.io** - Find company email addresses
- **Apollo.io** - Discover hiring managers & decision-makers
- **Smart fallback** - Generic hiring@ emails when needed

### 📝 Auto-Generated Assets
- **Tailored resumes** (ATS-optimized, keyword-rich)
- **Cold emails** (150-200 words, personalized)
- **Interview prep guides** (technical & behavioral questions)
- **Company research reports** (culture, tech stack, funding)

### 📈 Tracking & Analytics
- **Google Sheets integration** (Job Tracker + Interview Prep tabs)
- **Google Drive storage** (all generated resumes)
- **Slack notifications** (rich cards with job details)
- **Analytics dashboard** (summary statistics)

---

## 🏗️ Architecture
```
┌─────────────────────────────────────────────────────────────────┐
│                    🕐 Scheduler (Every 6H)                      │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ⚙️ Master Config                             │
│  (Resume, Skills, Salary, Target Roles, API Keys)               │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│              📡 Parallel Job Source Fetching                    │
│   Adzuna │ Remotive │ Arbeitnow │ FindWork                      │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│               🔄 Normalize & Deduplicate                        │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                  🤖 AI AGENT PIPELINE                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │  Agent 1:    │→ │  Agent 2:    │→ │  Agent 3:    │          │
│  │  Screening   │  │  Skills      │  │  Gemini AI   │          │
│  │  (50+ score) │  │  Analysis    │  │  Deep Dive   │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│              ✅ Filter Top Matches (80%+ score)                 │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│              🔍 ENRICHMENT PHASE (Parallel)                     │
│  Hunter.io │ Apollo.io │ Company Research │ Glassdoor           │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│              📝 CONTENT GENERATION (Parallel)                   │
│  Interview Prep │ Tailored Resume │ Cold Email                  │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                    💾 STORAGE & OUTPUT                          │
│  Google Drive │ Google Sheets │ Email Send │ Slack              │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                    📊 Analytics Summary                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔧 Prerequisites

### Required
- [n8n](https://n8n.io/) (self-hosted or cloud)
- [Google Gemini API](https://ai.google.dev/) (Free tier available)
- Google Account (for Sheets & Drive)
- Email account (for sending)

### Optional (for enhanced features)
- [Adzuna API](https://developer.adzuna.com/) - Job board access
- [Hunter.io API](https://hunter.io/api) - Email finder (50 free searches/month)
- [Apollo.io API](https://www.apollo.io/api) - Contact discovery (50 free credits)
- [Slack Webhook](https://api.slack.com/messaging/webhooks) - Notifications
- [Glassdoor API](https://www.glassdoor.com/developer/) - Company ratings

---

## 🛠️ Setup Guide

### 1️⃣ Clone & Import
```bash
# Download the workflow file
wget https://raw.githubusercontent.com/YOUR_USERNAME/ai-job-hunter/main/job-hunt-workflow.json

# Import in n8n:
# Settings → Import Workflow → Select file
```

### 2️⃣ Get API Keys

<details>
<summary><b>🔑 Google Gemini API (Required)</b></summary>

1. Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Click "Get API Key"
3. Copy your key → paste in workflow nodes
4. Free tier: 60 requests/minute, 1500 requests/day

**Nodes to update:**
- `🤖 AGENT 3: Gemini Deep Analysis`
- `📚 AGENT: Interview Prep Generator`
- `📄 AGENT: Resume Generator`
- `✉️ AGENT: Cold Email Generator`
- `🔍 AGENT: Company Research`

</details>

<details>
<summary><b>🔍 Adzuna API (Optional)</b></summary>

1. Register at [Adzuna Developer](https://developer.adzuna.com/)
2. Get `app_id` and `app_key`
3. Update node: `📡 Source: Adzuna`
```javascript
// Replace in query parameters:
"app_id": "YOUR_ADZUNA_APP_ID",
"app_key": "YOUR_ADZUNA_APP_KEY"
```

</details>

<details>
<summary><b>📧 Hunter.io API (Optional)</b></summary>

1. Sign up at [Hunter.io](https://hunter.io/)
2. Free plan: 50 searches/month
3. Get API key from [API section](https://hunter.io/api_keys)
4. Update node: `📧 Hunter.io Email Finder`
```javascript
"url": "https://api.hunter.io/v2/domain-search?domain={{ $json.company }}.com&api_key=YOUR_HUNTER_API_KEY"
```

</details>

<details>
<summary><b>👥 Apollo.io API (Optional)</b></summary>

1. Create account at [Apollo.io](https://www.apollo.io/)
2. Free: 50 credits/month
3. Get API key from Settings
4. Update node: `👥 Apollo.io Contact Finder`
```javascript
"headerParameters": {
  "X-Api-Key": "YOUR_APOLLO_API_KEY"
}
```

</details>

<details>
<summary><b>💬 Slack Webhook (Optional)</b></summary>

1. Create Slack app: [Slack API](https://api.slack.com/apps)
2. Enable "Incoming Webhooks"
3. Add to workspace → copy webhook URL
4. Update Master Config node:
```javascript
"slack_webhook": "https://hooks.slack.com/services/YOUR/SLACK/WEBHOOK"
```

</details>

### 3️⃣ Configure Google Services

**Google Sheets:**
1. Create a new spreadsheet
2. Add two sheets: "Job Tracker" and "Interview Prep"
3. In n8n, connect Google Sheets nodes (OAuth2)
4. Select your spreadsheet in nodes:
   - `📊 Save to Job Tracker`
   - `📚 Save Interview Prep`

**Google Drive:**
1. Create a folder for resumes
2. Get folder ID from URL: `drive.google.com/drive/folders/FOLDER_ID`
3. Update Master Config:
```javascript
"google_drive_folder_id": "YOUR_DRIVE_FOLDER_ID"
```

### 4️⃣ Update Master Config

Open the `⚙️ Master Config` node and update:
```javascript
{
  "resume_text": "YOUR FULL RESUME HERE",
  "target_roles": ["Senior Software Engineer", "Staff Engineer", "Tech Lead"],
  "skills_primary": ["JavaScript", "React", "Node.js", "AWS", "Python"],
  "your_name": "Your Name",
  "your_email": "your.email@gmail.com",
  "linkedin_url": "linkedin.com/in/yourprofile",
  "github_username": "yourgithub",
  "years_experience": 8,
  "min_salary": 150000,
  "target_salary": 180000,
  "match_threshold": 80,
  "enable_auto_apply": false
}
```

### 5️⃣ Test Run

1. Click "Execute Workflow" button
2. Check each node for outputs
3. Verify Google Sheets populated
4. Check Slack for notification
5. Confirm emails sent (if enabled)

---

## ⚙️ Configuration

### Scheduling

The workflow runs **every 6 hours** by default. To adjust:

1. Open `⏰ Master Trigger - Every 6H` node
2. Change interval:
   - Every 3 hours: `{"field": "hours", "hoursInterval": 3}`
   - Daily at 9 AM: Use Cron expression `0 9 * * *`
   - Twice daily: `{"field": "hours", "hoursInterval": 12}`

### Scoring Thresholds

Adjust what qualifies as a "match":
```javascript
// In Master Config
"match_threshold": 80  // Default: 80% (strict)
                       // 70% (moderate)
                       // 60% (relaxed)
```

**Scoring breakdown:**
- Initial screening: 20%
- Skills match: 30%
- ATS score: 25%
- Experience match: 25%

### Job Sources

Add more sources by duplicating HTTP Request nodes:
```javascript
{
  "parameters": {
    "method": "GET",
    "url": "https://jobs.github.com/positions.json",
    "sendQuery": true,
    "queryParameters": {
      "parameters": [
        {"name": "description", "value": "engineer"},
        {"name": "location", "value": "remote"}
      ]
    }
  }
}
```

### Auto-Apply (⚠️ Use with caution)
```javascript
// In Master Config
"enable_auto_apply": false  // Set to true to auto-send emails
```

**Recommendation:** Keep `false` initially, review generated content, then enable.

---

## 📊 Workflow Stages

### Stage 1: Data Collection (Nodes 1-8)
- Triggers every 6 hours
- Fetches from 4 job boards in parallel
- Normalizes different API formats
- Filters jobs posted in last 24 hours
- Deduplicates based on company + title

**Output:** ~200-400 raw job listings

### Stage 2: AI Screening (Nodes 9-13)
- **Agent 1:** Checks role match, seniority, visa requirements, salary
- **Agent 2:** Analyzes skills overlap with your profile
- **Agent 3:** Deep AI analysis (Gemini) for ATS score, cultural fit, strengths/weaknesses
- Calculates composite score (0-100)
- Filters jobs scoring 80%+

**Output:** ~10-30 high-quality matches

### Stage 3: Enrichment (Nodes 14-19)
- Finds hiring manager emails (Hunter.io)
- Discovers decision-makers (Apollo.io)
- Researches company culture, funding, tech stack
- Pulls Glassdoor ratings
- Merges all data

**Output:** Fully enriched job profiles

### Stage 4: Content Generation (Nodes 20-24)
- **Parallel generation:**
  - Interview prep guide (technical + behavioral questions)
  - Tailored resume (ATS-optimized)
  - Personalized cold email (150-200 words)
- Parses AI responses
- Sorts by composite score

**Output:** Application-ready packages

### Stage 5: Storage & Outreach (Nodes 25-29)
- Saves resumes to Google Drive
- Logs to Google Sheets (2 tabs)
- Sends cold emails (if enabled)
- Posts to Slack with rich cards
- Generates analytics summary

**Output:** Complete job pipeline

---

## 🔌 API Integrations

| Service | Purpose | Cost | Limit | Required |
|---------|---------|------|-------|----------|
| **Google Gemini** | AI analysis, content generation | Free | 1500/day | ✅ Yes |
| **Adzuna** | Job listings | Free | 100/search | ⚠️ Recommended |
| **Remotive** | Remote jobs | Free | 50/request | ❌ No |
| **Arbeitnow** | EU/Intl jobs | Free | Unlimited | ❌ No |
| **FindWork** | Dev jobs | Free | Unlimited | ❌ No |
| **Hunter.io** | Email finder | $49/mo | 50/mo free | ⚠️ Recommended |
| **Apollo.io** | Contact discovery | $49/mo | 50/mo free | ⚠️ Recommended |
| **Glassdoor** | Company ratings | Varies | Varies | ❌ No |
| **Google Sheets** | Data tracking | Free | Unlimited | ✅ Yes |
| **Google Drive** | File storage | Free | 15GB free | ✅ Yes |
| **Slack** | Notifications | Free | Unlimited | ⚠️ Recommended |

**Total monthly cost (minimal setup):** $0  
**Total monthly cost (full features):** ~$100

---

## 💡 Usage

### Viewing Results

**Google Sheets - Job Tracker Tab:**
| Column | Description |
|--------|-------------|
| Company | Company name |
| Title | Job title |
| Location | Job location |
| Composite Score | Overall match score (0-100) |
| Skills Matched | Your matching skills |
| Skills Missing | Skills to learn |
| Priority | HIGH/MEDIUM/LOW |
| Salary Estimate | AI-estimated range |
| Glassdoor Rating | Company rating |
| URL | Application link |
| Contact Email | Hiring manager email |
| Status | Pending/Applied/Interview |

**Google Sheets - Interview Prep Tab:**
| Column | Description |
|--------|-------------|
| Company | Company name |
| Technical Questions | 10+ likely questions |
| Behavioral Questions | STAR method questions |
| System Design Topics | Areas to prepare |
| Questions to Ask | Thoughtful questions for them |
| Salary Strategy | Negotiation talking points |

**Slack Notifications:**
```
🎯 New Job Match Found!

Senior Software Engineer @ TechCorp

Score: 92%          Priority: HIGH
Location: Remote    Salary: $180-220K

Strengths: Strong React experience, microservices architecture, AWS expertise

[View Job] [Resume] [Interview Prep]
```

### Managing Applications

1. **Review Matches:** Check Slack or Sheets daily
2. **Prioritize:** Sort by composite score
3. **Customize Resume:** Download from Drive, tweak if needed
4. **Send Application:** Use generated cold email or apply directly
5. **Track Status:** Update "Status" column in Sheets
6. **Prepare:** Use interview prep guide before calls

---

## 🎨 Example Output

<details>
<summary><b>📊 Sample Job Analysis</b></summary>
```json
{
  "company": "TechCorp",
  "title": "Senior Full-Stack Engineer",
  "location": "Remote (US)",
  "compositeScore": 92,
  "screening": {
    "roleMatch": true,
    "seniorMatch": true,
    "h1bFriendly": true,
    "salaryOK": true,
    "score": 100
  },
  "skillsAnalysis": {
    "matched": ["JavaScript", "React", "Node.js", "AWS", "PostgreSQL"],
    "missing": ["Kubernetes", "GraphQL"],
    "score": 83
  },
  "aiAnalysis": {
    "overallScore": 92,
    "atsScore": 88,
    "experienceMatch": 95,
    "culturalFit": 85,
    "interviewChance": "85%",
    "priority": "HIGH",
    "strengths": [
      "10+ years full-stack experience",
      "Strong microservices background",
      "AWS expertise matches requirements"
    ],
    "weaknesses": [
      "Limited Kubernetes experience",
      "No GraphQL mentioned"
    ],
    "salaryEstimate": "$180-220K",
    "recommendedAction": "Apply immediately"
  }
}
```

</details>

<details>
<summary><b>📧 Sample Cold Email</b></summary>
```
Subject: Senior Engineer with 10yr microservices exp - TechCorp opportunity

Hi Sarah,

I noticed TechCorp is hiring a Senior Full-Stack Engineer and was impressed 
by your recent Series C funding and focus on scalable architecture.

In my current role at BigTech, I've:
- Built microservices handling 10M+ requests/day
- Led migration to AWS (40% cost reduction)
- Mentored 5 engineers, improving team velocity 40%

Your tech stack (React, Node, AWS) aligns perfectly with my expertise. 
I'm particularly excited about TechCorp's mission to democratize fintech.

Would you have 15 minutes this week to discuss how I could contribute to 
your engineering team?

Best regards,
John Doe
linkedin.com/in/johndoe
github.com/johndoe
```

</details>

<details>
<summary><b>📚 Sample Interview Prep</b></summary>
```json
{
  "technicalQuestions": [
    "Explain how you'd design a microservices architecture for high traffic",
    "How do you handle database scaling in distributed systems?",
    "Walk me through your approach to API versioning",
    "Describe your experience with CI/CD pipelines",
    "How do you ensure code quality in a fast-paced environment?"
  ],
  "behavioralQuestions": [
    "Tell me about a time you led a technical initiative (STAR method)",
    "Describe a situation where you had to make a trade-off between speed and quality",
    "How do you handle disagreements with team members?"
  ],
  "systemDesignTopics": [
    "Designing a scalable payment processing system",
    "Real-time notification system architecture",
    "Caching strategies for high-traffic APIs"
  ],
  "questionsToAsk": [
    "What are the biggest technical challenges your team is facing?",
    "How do you measure engineering success?",
    "What's the on-call rotation like?",
    "How do you approach technical debt?"
  ],
  "salaryNegotiation": {
    "targetRange": "$180-220K",
    "justification": [
      "10 years experience vs 8 years required",
      "Led teams of 5 engineers",
      "Proven track record scaling systems to 10M+ requests/day",
      "Market rate for Senior Engineers in SF: $175-230K"
    ]
  }
}
```

</details>

---

## 🔧 Customization

### Adding Custom Scoring Logic

Edit `🤖 AGENT 1: Initial Screening` node:
```javascript
// Add custom criteria
const remoteOK = text.includes('remote') || text.includes('work from home');
const equityMentioned = text.includes('equity') || text.includes('stock');

let score = 0;
if (roleMatch) score += 30;
if (seniorMatch) score += 20;
if (h1bFriendly) score += 25;
if (salaryOK) score += 20;
if (remoteOK) score += 5;      // NEW
if (equityMentioned) score += 5; // NEW

return screened.filter(j => j.json.screening.score >= 60); // Adjust threshold
```

### Targeting Specific Companies

Add to Master Config:
```javascript
"target_companies": ["Google", "Meta", "Amazon", "Netflix"],
"blocked_companies": ["BadCorp", "BoringInc"]
```

Then filter in screening:
```javascript
const targetCompanies = JSON.parse(config.target_companies);
const blockedCompanies = JSON.parse(config.blocked_companies);

const companyMatch = targetCompanies.length === 0 || 
  targetCompanies.some(c => job.company.toLowerCase().includes(c.toLowerCase()));
const notBlocked = !blockedCompanies.some(c => 
  job.company.toLowerCase().includes(c.toLowerCase()));

if (companyMatch && notBlocked) { /* proceed */ }
```

### Custom Email Templates

Modify the prompt in `✉️ AGENT: Cold Email Generator`:
```javascript
"text": "Write a cold email with this tone: [YOUR STYLE]

RULES:
- Start with a mutual connection (if any)
- Lead with biggest achievement
- Show knowledge of their product
- Include portfolio link
- End with specific ask

[Rest of prompt...]"
```

### Adding Notion Integration

Add after Google Sheets nodes:
```javascript
{
  "parameters": {
    "resource": "databasePage",
    "operation": "create",
    "databaseId": "YOUR_NOTION_DB_ID",
    "properties": {
      "Company": {"type": "title", "title": [{"text": {"content": "={{ $json.company }}"}}]},
      "Score": {"type": "number", "number": "={{ $json.compositeScore }}"},
      "Status": {"type": "select", "select": {"name": "To Apply"}}
    }
  }
}
```

---

## 🐛 Troubleshooting

### Common Issues

<details>
<summary><b>❌ "API key invalid" error</b></summary>

**Solution:**
1. Verify API key is correct (no extra spaces)
2. Check if key has necessary permissions
3. Ensure billing is enabled (for paid APIs)
4. Try regenerating the key

</details>

<details>
<summary><b>❌ No jobs found</b></summary>

**Possible causes:**
1. API sources are down → Check individual source nodes
2. Search terms too specific → Broaden `target_roles`
3. Threshold too high → Lower `match_threshold` to 60-70
4. All jobs older than 24h → Change date filter in normalization

**Debug:**
```javascript
// In 🔄 Normalize Data node, change:
const oneDayAgo = new Date(today - 24*60*60*1000);
// To:
const threeDaysAgo = new Date(today - 3*24*60*60*1000);
```

</details>

<details>
<summary><b>❌ Gemini rate limit exceeded</b></summary>

**Solution:**
1. Free tier limit: 60 requests/minute
2. Add delay between calls:
```javascript
// Add Sleep node between AI calls
{
  "parameters": {
    "amount": 2, // Wait 2 seconds
    "unit": "seconds"
  }
}
```

3. Or upgrade to paid tier: $0.00025 per request

</details>

<details>
<summary><b>❌ Emails not sending</b></summary>

**Check:**
1. SMTP credentials correct in Email node
2. Gmail: Enable "Less secure app access"
3. Outlook: Use app password, not main password
4. Email formatting: Remove invalid characters

**Alternative:** Use SendGrid or Mailgun nodes

</details>

<details>
<summary><b>❌ Google Sheets not updating</b></summary>

**Solution:**
1. Re-authenticate OAuth connection
2. Ensure sheet names match exactly ("Job Tracker", "Interview Prep")
3. Check if columns exist (auto-map may fail on first run)
4. Manually add headers in first row

</details>

<details>
<summary><b>⚠️ Low match scores</b></summary>

**Improve scores by:**
1. Update `resume_text` with more details
2. Expand `skills_primary` list
3. Add certifications/achievements
4. Include exact keywords from job descriptions

</details>

### Debug Mode

Enable verbose logging:
```javascript
// Add to any Code node
console.log('DEBUG:', JSON.stringify($input.all(), null, 2));
```

View logs: n8n UI → Executions → Select run → View node output

---

## 🚀 Roadmap

### Coming Soon
- [ ] LinkedIn job scraping integration
- [ ] Indeed API integration
- [ ] AngelList/Wellfound startup jobs
- [ ] Automatic interview scheduling
- [ ] Salary negotiation simulator
- [ ] Portfolio website generator
- [ ] GitHub profile analyzer
- [ ] LeetCode problem suggester

### Future Features
- [ ] Video interview prep (AI mock interviews)
- [ ] Application status tracker with reminders
- [ ] Offer comparison dashboard
- [ ] Recruiter outreach automation
- [ ] Skills gap analysis & course recommendations
- [ ] Network warm intro finder (LinkedIn mutual connections)
- [ ] ATS compatibility checker
- [ ] Resume A/B testing

### Want to contribute? See [Contributing](#-contributing)

---

## 🤝 Contributing

We welcome contributions! Here's how:

### Reporting Bugs
1. Check [existing issues](https://github.com/YOUR_USERNAME/ai-job-hunter/issues)
2. Create new issue with:
   - n8n version
   - Node versions involved
   - Error messages
   - Steps to reproduce

### Suggesting Features
1. Open issue with tag `enhancement`
2. Describe use case
3. Provide example implementation (if possible)

### Submitting Pull Requests
1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Test changes thoroughly
4. Update documentation
5. Commit: `git commit -m 'Add amazing feature'`
6. Push: `git push origin feature/amazing-feature`
7. Open Pull Request

### Development Setup
```bash
# Clone repo
git clone https://github.com/YOUR_USERNAME/ai-job-hunter.git
cd ai-job-hunter

# Install n8n locally
npm install -g n8n

# Start n8n
n8n start

# Import workflow
# n8n UI → Import Workflow → Select job-hunt-workflow.json
```

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details

**TL;DR:** Free to use, modify, distribute. No warranty. Give credit.

---

## ⚠️ Disclaimer

This workflow is for **educational and personal use** only.

- ⚠️ **Comply with job board Terms of Service** (rate limits, scraping policies)
- ⚠️ **Verify all AI-generated content** before sending
- ⚠️ **Respect privacy** when finding contacts
- ⚠️ **Use ethical outreach** practices
- ⚠️ **Don't spam** hiring managers

The authors are not responsible for misuse, account bans, or failed applications.

---

## 🙏 Acknowledgments

- [n8n](https://n8n.io/) - Workflow automation platform
- [Google Gemini](https://ai.google.dev/) - AI analysis
- [Hunter.io](https://hunter.io/) - Email discovery
- [Apollo.io](https://www.apollo.io/) - Contact data
- Job boards: Adzuna, Remotive, Arbeitnow, FindWork

---

## 📬 Contact

- **Issues:** [GitHub Issues](https://github.com/YOUR_USERNAME/ai-job-hunter/issues)
- **Discussions:** [GitHub Discussions](https://github.com/YOUR_USERNAME/ai-job-hunter/discussions)
- **Twitter:** [@YourHandle](https://twitter.com/yourhandle)
- **Email:** your.email@example.com

---

## ❓ FAQ

<details>
<summary><b>Is this legal?</b></summary>

Yes, if used responsibly. Always check job board Terms of Service. Most allow reasonable personal use. Don't exceed rate limits or scrape aggressively.

</details>

<details>
<summary><b>Will this get me hired?</b></summary>

This workflow dramatically increases your application volume and quality, but hiring still depends on:
- Your actual skills/experience
- Interview performance
- Market conditions
- Luck/timing

Think of it as a force multiplier, not a magic solution.

</details>

<details>
<summary><b>How much does it cost to run?</b></summary>

**Minimal setup:** $0/month (Gemini free tier + free job boards)
**Recommended setup:** ~$50-100/month (Hunter + Apollo paid tiers)
**Full setup:** ~$150-200/month (all premium APIs)

Most users find the minimal setup sufficient.

</details>

<details>
<summary><b>Can I use Claude/GPT-4 instead of Gemini?</b></summary>

Yes! Replace HTTP Request nodes with OpenAI/Anthropic API calls:
```javascript
// OpenAI example
{
  "method": "POST",
  "url": "https://api.openai.com/v1/chat/completions",
  "headers": {
    "Authorization": "Bearer YOUR_OPENAI_KEY"
  },
  "body": {
    "model": "gpt-4",
    "messages": [{"role": "user", "content": "YOUR PROMPT"}]
  }
}
```

</details>

<details>
<summary><b>How do I stop the workflow?</b></summary>

1. Deactivate: Click toggle in workflow header
2. Delete trigger: Remove `⏰ Master Trigger` node
3. Pause temporarily: Set interval to very high value (9999 hours)

</details>

<details>
<summary><b>Can I run this on n8n cloud?</b></summary>

Yes! n8n cloud supports all features. Benefits:
- No server maintenance
- Auto-scaling
- Always online
- 14-day free trial

Sign up: [n8n.cloud](https://n8n.cloud/)

</details>

<details>
<summary><b>What about international jobs?</b></summary>

Currently optimized for US jobs. For international:
1. Update search queries with your country
2. Add local job boards (e.g., Seek for Australia)
3. Adjust currency in salary filters
4. Modify visa filtering logic

</details>

<details>
<summary><b>How accurate is the AI analysis?</b></summary>

Gemini is ~85-90% accurate for:
- Skills matching
- ATS scoring
- Resume tailoring

Always review AI outputs before using. The workflow is a tool, not a replacement for human judgment.

</details>

[⬆ Back to Top](#-ultimate-ai-job-hunter---enterprise-edition)

</div>
