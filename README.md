
```
# n8n: Latest AI News + Job Digest (Simple Workflow)

## 📌 Purpose

Daily automated email that collects the latest **AI headlines** (past 24 hours) and recent job postings for **DevOps Intern** and **AI Automation Intern** in India — using a simple **n8n** workflow with **three nodes only**:

1. **Schedule Trigger** (cron) — runs daily  
2. **Perplexity (Message a Model)** — Sonar Pro model with system + user prompt  
3. **Gmail** — sends the resulting HTML email  

> **Important:** This setup contains exactly **three nodes**.  
> No HTTP requests, Gemini, or extra steps are included.

---

## 🛠 Prerequisites

- An **n8n instance** (local or hosted) with UI access  
- **Perplexity** account credentials configured in n8n  
- **Gmail OAuth2** credentials configured in n8n  
- Workflow activation permission in n8n  

---

## 🔄 Workflow Overview

### 1. Schedule Trigger
- Cron trigger to run the workflow daily at your preferred time.

### 2. Perplexity Node
- **Type:** `Message a model`  
- **Model:** `sonar-pro`  
- Uses **system prompt** (HTML formatting rules) and **user prompt** (AI news + jobs).

### 3. Gmail Node
- Email **subject** and **HTML body** come directly from Perplexity output.
- Sends to your desired email address.

---

## 📡 Node Wiring

```

Schedule Trigger  -->  Perplexity (Message a model)  -->  Gmail (Send a message)

````

**Gmail Message Field Example:**
```n8n
{{$json["choices"][0]["message"]["content"]}}
````

*(Ensure Gmail node sends HTML email.)*

---

## 🖋 System Prompt

```text
You are a cutting-edge AI news researcher and job data collector.

Every time you run, you must:
1. Search for and retrieve the most recent developments in Artificial Intelligence published within the last 24 hours.
2. Find 2–3 latest job openings in India posted within the last 24 hours for:
   - DevOps Intern
   - AI Automation Intern
3. Ensure all data is accurate, fresh, and from trusted sources.

For each AI news item:
- Include the full headline.
- Provide a one-sentence summary.
- Include the full URL.

For each job listing:
- Include Job Title, Company, Location, Posting Platform & Time, Application Link.

**IMPORTANT OUTPUT REQUIREMENTS:**
- Return a single self-contained HTML document with inline CSS styling.
- Clear section headings, card-style boxes, and tables.
- Light background color and styled clickable links.

**HTML Output Structure:**
<html>
  <head>
    <style>
      body { font-family: Arial, sans-serif; background-color: #f8f9fa; padding: 20px; }
      h2 { color: #2c3e50; }
      .news-item, .job-table { background: #fff; padding: 15px; margin-bottom: 15px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
      .news-item h3 { margin-top: 0; color: #007bff; }
      .news-item p { margin: 5px 0; }
      table { width: 100%; border-collapse: collapse; }
      th, td { border: 1px solid #ddd; padding: 8px; }
      th { background-color: #007bff; color: white; }
      a { color: #007bff; text-decoration: none; }
      a:hover { text-decoration: underline; }
    </style>
  </head>
  <body>
    <h2>🧠 Latest AI News (Past 24 Hours)</h2>
    <div class="news-item">
      <h3>Headline</h3>
      <p><strong>Summary:</strong> One sentence summary here.</p>
      <p><a href="FULL_URL">Read more</a></p>
    </div>

    <h2>💼 DevOps Intern Jobs (India | Last 24 Hours)</h2>
    <table class="job-table">
      <tr>
        <th>Job Title</th>
        <th>Company</th>
        <th>Location</th>
        <th>Platform & Time</th>
        <th>Application Link</th>
      </tr>
      <tr>
        <td>Job Title</td>
        <td>Company Name</td>
        <td>Location</td>
        <td>Platform · Time</td>
        <td><a href="FULL_URL">Apply Here</a></td>
      </tr>
    </table>

    <h2>🤖 AI Automation Intern Jobs (India | Last 24 Hours)</h2>
    <table class="job-table">
      <tr>
        <th>Job Title</th>
        <th>Company</th>
        <th>Location</th>
        <th>Platform & Time</th>
        <th>Application Link</th>
      </tr>
      <tr>
        <td>Job Title</td>
        <td>Company Name</td>
        <td>Location</td>
        <td>Platform · Time</td>
        <td><a href="FULL_URL">Apply Here</a></td>
      </tr>
    </table>
  </body>
</html>
```

---

## 💬 User Prompt

```text
what are the latest headline in ai development in the 24 hours?
include any model launches or market news.

also job opening in 24 hours latest uploaded on any job platfrom for "Devops inter" and "AI automation intern" in india.
```

---

## 🚀 How to Run

1. Create a new workflow in n8n.
2. Add **Schedule Trigger** — set desired daily time.
3. Add **Perplexity** (Message a model) node:

   * Model: `sonar-pro`
   * Paste **system** and **user** prompts above.
4. Add **Gmail** node:

   * Configure Gmail OAuth2.
   * Use Perplexity output in body:

     ```n8n
     {{$json["choices"][0]["message"]["content"]}}
     ```
   * Enable HTML sending.
5. Save & activate workflow.

---

## ✅ Expected Output

* Single HTML email containing:

  * AI headlines (headline + summary + link).
  * Two job tables (DevOps Intern, AI Automation Intern) with 2–3 latest jobs each.

---

## 🛠 Troubleshooting

* If output is empty:

  * Verify Perplexity & Gmail credentials.
  * Check Perplexity node output in execution logs.
  * Ensure Gmail node is set to send HTML.

---

## 📜 Notes

* Exact setup: **Schedule Trigger → Perplexity → Gmail**
* No other nodes or services.
* HTML template enforced by **system prompt**.

---


Do you want me to also create a **JSON export** of this exact three-node n8n workflow so it’s instantly importable? That would make it a complete repo package.
```
