---

# AI News & Job Aggregator – Verified HTML Email Generator

## 📌 Overview

This project automates the process of collecting, validating, and sending **latest AI developments** and **job postings** in India for:

* **DevOps Intern**
* **AI Automation Intern**

It uses:

* **Perplexity AI** → Fetches fresh AI news & job postings from approved job platforms
* **Validation & Filtering Node** (n8n Function / Code) → Checks job links for 404 or broken pages
* **Fallback Search AI** (optional) → If data is missing, searches for valid replacements
* **n8n Gmail Node** → Sends the final HTML email

The final result is a **styled HTML email** with:

* Only **verified, working job postings**
* Only **AI news within the last 24 hours**
* Inline CSS for email client compatibility

---

## ⚙️ Workflow

1. **Perplexity AI Node**
   Queries:

   * Latest AI news in the last 24 hours
   * DevOps Intern & AI Automation Intern jobs (India, posted in the last 24 hours)
     Searches only **LinkedIn, Internshala, Naukri, Indeed India**.

2. **Validation Node (n8n Function)**

   * Parses the job links
   * Checks if they return **HTTP 200 OK**
   * Removes expired, broken, or 404 links

3. **Fallback Search AI (optional)**

   * If any job table is empty after validation,
     searches again online and fills missing entries

4. **HTML Formatter Node**

   * Generates a styled HTML email with:

     * AI News section (cards)
     * DevOps Intern jobs (table)
     * AI Automation Intern jobs (table)

5. **Gmail Node**

   * Sends the HTML email to the recipient

---

## 📜 System Prompt (Validation AI)

```plaintext
You are a job and news post-processor. 
You will receive raw data from Perplexity AI containing AI news and job postings.

Rules:
1. Check each job link:
   - If the link is broken, expired, or 404, remove it.
   - Only keep jobs from LinkedIn, Internshala, Naukri, or Indeed India.
2. All jobs must be posted within the last 24 hours.
3. If the final list has missing jobs, search online and replace them with valid postings.
4. AI News:
   - Keep only credible, verified AI developments from the last 24 hours.
   - Each must have a headline, short summary, and clickable source link.
5. Final output:
   - Section 1: AI news in styled HTML cards.
   - Section 2: DevOps Intern jobs in an HTML table.
   - Section 3: AI Automation Intern jobs in an HTML table.
6. Use inline CSS for email formatting.
7. If no valid jobs are found after retries, leave the table empty and insert:
   `<p style="color: #b94a48;">No valid jobs found.</p>`
8. Return **only HTML**, no JSON, no debug notes.
```

---

## 🖥 Example Usage in n8n

1. **HTTP Request / Perplexity Node** → Run the initial search query
2. **Function Node** → Validate & filter URLs
3. **Validation AI Node** → Apply the system prompt above
4. **Gmail Node** → Send final HTML email

---

## 📌 Example Perplexity Query Prompt

```plaintext
Get the latest AI news headlines and summaries from the last 24 hours 
and the most recent job postings in India for “DevOps Intern” and “AI Automation Intern” 
posted within the last 24 hours on LinkedIn, Internshala, Naukri, and Indeed India. 
Include job title, company name, location, posting time, and application link.
```

---

## 📂 Repository Structure

```
.
├── README.md           # Documentation
├── prompts/
│   ├── system_prompt.txt    # System prompt for validation
│   ├── perplexity_prompt.txt # Query for Perplexity
├── n8n_workflow.json   # Ready-to-import n8n workflow
├── examples/
│   ├── sample_email.html    # Example of final HTML output
```

---

## 🚀 Benefits

* Removes **broken or expired job links**
* Ensures only **fresh news and postings** are included
* Fully **automated daily update**
* Email-friendly **HTML output**

---

Do you want me to also include an **n8n Function Node JavaScript code** in this README that will automatically check for **404/broken job links** before it even reaches the AI? That would make your pipeline much more reliable.
