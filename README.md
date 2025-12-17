# ai-gmail-auto-reply-n8n # 🤖 AI Gmail Auto-Reply Assistant (n8n + Google Gemini)

This project is an AI-powered email automation workflow built using **n8n** and **Google Gemini AI**.  
It automatically reads incoming Gmail messages, generates professional replies using AI, sends responses, and logs all interactions into Google Sheets.

## 🚀 Features

- 📥 Detects new incoming Gmail messages
- 🧠 Uses Google Gemini AI to generate human-like replies
- 📧 Sends automated email responses via Gmail
- 📊 Logs incoming emails and AI replies to Google Sheets
- 🛡 Prevents infinite reply loops using labels
- 🆓 Uses Gemini Free Tier (no paid AI required)

## 🧱 Tech Stack

- **n8n** (self-hosted, local)
- **Google Gemini AI**
- **Gmail API**
- **Google Sheets API**

## 🔄 Workflow Overview
Gmail Trigger
↓
Google Sheets (Log Incoming Email)
↓
Gemini AI (Generate Reply)
↓
Gmail Send (Auto Reply)
↓
Gmail Update (Mark as Read / Label)


---

## 🛠 How It Works

1. The workflow listens for new unread Gmail messages.
2. Email details (sender, subject, content) are logged in Google Sheets.
3. The email content is sent to Gemini AI with instructions to generate a professional reply.
4. The AI-generated reply is automatically sent back to the sender.
5. The email is marked as read and labeled to avoid duplicate replies.

---

## 📄 Sample AI Prompt

```text
You are a professional academic assistant.
Write polite, concise, human-like email replies.

Reply professionally to this email:

From: {{Sender Name}} <{{Sender Email}}>
Subject: {{Subject}}

Message:
{{Snippet}}
