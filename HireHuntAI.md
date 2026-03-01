Below is a **complete professional `README.md`** for your project **Hire Hunt AI**.
I focused especially on **setup, installation, and running the workflow**, since that is the most important part for users.

You can directly paste this into your repository.

---

# Hire Hunt AI

Hire Hunt AI is an **AI-powered job discovery and application assistant** built using **n8n automation, AI models, and LinkedIn job scraping**.

The system automatically:

* Analyzes a candidate's **resume**
* Identifies **core domains**
* Generates **optimized LinkedIn job search filters**
* Scrapes **latest job listings**
* Evaluates **job–resume match score**
* Generates a **personalized cover letter**
* Sends **high-quality job matches via Telegram**
* Stores all results in **Google Sheets**

The entire workflow runs automatically after the user submits the form.

---

# Features

* AI Resume Analysis
* Automatic Domain Extraction
* Smart LinkedIn Job Search Generation
* Job Scraping Automation
* Resume–Job Matching Score
* AI Generated Cover Letter
* Telegram Job Alerts
* Google Sheets Job Database
* Smart Filtering for Relevant Jobs Only

---

# System Architecture

Workflow pipeline:

```
User Form Submission
        │
        ▼
Resume Extraction (PDF)
        │
        ▼
AI Domain Detection
        │
        ▼
Generate LinkedIn Search URLs
        │
        ▼
Scrape LinkedIn Jobs
        │
        ▼
Extract Job Data
        │
        ▼
AI Resume Matching + Cover Letter
        │
        ▼
Score Filtering
        │
        ▼
Telegram Job Notification
        │
        ▼
Save Data to Google Sheets
```

---

# Tech Stack

| Tool          | Purpose                     |
| ------------- | --------------------------- |
| n8n           | Automation Workflow Engine  |
| Google Gemini | Resume Domain Analysis      |
| Groq LLM      | Job Matching & Cover Letter |
| Telegram Bot  | Job Notifications           |
| Google Sheets | Job Database                |
| LinkedIn      | Job Source                  |
| JavaScript    | URL Filter Generation       |

---

# Installation & Setup Guide

## 1. Install n8n

You must have **Node.js v18+** installed.

### Install globally

```bash
npm install -g n8n
```

### Start n8n

```bash
n8n start
```

Open in browser:

```
http://localhost:5678
```

---

# 2. Import the Workflow

1. Open **n8n dashboard**
2. Click **Import Workflow**
3. Paste the provided workflow JSON
4. Save the workflow

---

# 3. Required API Credentials

You must configure the following credentials inside n8n.

---

## Google Gemini API

Used for **resume domain analysis**

1. Go to:

```
https://ai.google.dev
```

2. Generate API Key

3. In n8n

```
Credentials → Google Gemini(PaLM) API
```

Paste your API key.

---

## Groq API

Used for:

* Resume–job matching
* Cover letter generation

Create API key:

```
https://console.groq.com
```

Then in n8n:

```
Credentials → Groq API
```

Paste your API key.

---

## Telegram Bot Setup

Used to **send job notifications**.

### Step 1 — Create Bot

Open Telegram and search:

```
@BotFather
```

Run:

```
/newbot
```

Copy the **Bot Token**

---

### Step 2 — Get Chat ID

Message this bot:

```
@userinfobot
```

Copy your **chat_id**

---

### Step 3 — Add Credentials in n8n

```
Credentials → Telegram API
```

Add:

```
Bot Token
```

---

### Step 4 — Update Chat ID

Inside the node:

```
Details Send With Cover Letter
```

Replace:

```
chatId: YOUR_CHAT_ID
```

---

# Google Sheets Setup

This workflow stores job results in Google Sheets.

### Step 1

Create a new Google Sheet

Example:

```
Job Records
```

---

### Step 2

Create columns:

```
Job Title
Company Name
Company Location
Job Description
Apply Link
Cover Letter
```

---

### Step 3

Copy the **Sheet ID** from the URL

Example:

```
https://docs.google.com/spreadsheets/d/SHEET_ID/edit
```

---

### Step 4

Add Google Sheets OAuth credentials in n8n

```
Credentials → Google Sheets OAuth2
```

Authenticate with your Google account.

---

# Resume Requirements

The system currently supports:

```
PDF resumes
```

The resume is automatically parsed using the **Extract From File node**.

---

# Form Inputs

The user submits a form with the following inputs:

| Field            | Description                |
| ---------------- | -------------------------- |
| Resume           | Upload PDF resume          |
| Location         | Country preference         |
| Experience Level | LinkedIn experience filter |
| Work Mode        | Remote / Hybrid / Onsite   |
| Job Type         | Full-time / Contract / etc |

---

# LinkedIn Search Generation

The system dynamically creates **multiple optimized job searches** using combinations of filters.

Example combinations:

```
Location + Experience
Location + Remote
Experience + Job Type
Location + Experience + Remote
Location + Remote + Job Type
```

This ensures:

* Maximum coverage
* Highly targeted job results

---

# Job Matching Logic

Each job is scored between **0 – 100** based on:

### 1. Tech Stack Match

Highest weight

### 2. Experience Match

Compares role seniority

### 3. Project Relevance

Relevant projects improve score

---

# Score Filtering

Only jobs with:

```
Score > 50
```

are sent to the user.

This prevents irrelevant job notifications.

---

# Telegram Notification Example

The user receives:

```
Title: Software Engineer
Company: Google
Location: Bangalore

Apply Link: https://linkedin.com/jobs/view/12345

Job Match Score: 82

Cover Letter:
AI generated cover letter...
```

---

# Output Storage

All results are stored in **Google Sheets** including:

* Job title
* Company
* Location
* Description
* Apply link
* Generated cover letter

---

# Estimated Processing Time

After submitting the form:

```
5 – 10 minutes
```

This depends on:

* Number of jobs scraped
* AI processing time
* Network latency

---

# Important Notes

LinkedIn may rate-limit excessive scraping.

To reduce issues:

* Wait nodes are included
* Batch processing is used
* Requests are throttled

---

# Future Improvements

Possible upgrades:

* Direct **Auto Apply**
* **ATS Resume Optimization**
* Email Job Alerts
* Multi-platform scraping (Indeed, Glassdoor)
* AI Resume Builder
* Job Trend Analysis
* Chrome Extension

---

# Contributing

Contributions are welcome.

You can improve:

* Job scraping
* AI prompts
* scoring model
* automation performance
