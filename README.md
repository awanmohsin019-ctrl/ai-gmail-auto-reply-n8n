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
[AI Email Reply Assistant.json](https://github.com/user-attachments/files/24204657/AI.Email.Reply.Assistant.json)
{
  "name": "AI Email Reply Assistant",
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        128,
        48
      ],
      "id": "27242a9b-d820-4cc7-81f5-f4039504d59d",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "operation": "getAll",
        "limit": 1,
        "simple": false,
        "filters": {
          "readStatus": "unread"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.1,
      "position": [
        560,
        -80
      ],
      "id": "5ae4038c-c7c7-4db4-a685-2776edfad8c2",
      "name": "Get many messages",
      "webhookId": "9b6203cd-00bc-4bf7-8c3e-72926cc34f50",
      "executeOnce": true,
      "alwaysOutputData": false,
      "credentials": {
        "gmailOAuth2": {
          "id": "2hKPNNCWm4s43bgO",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1CzDtf9NdITNu2sJoVb0iut8J0U8XvpEF-rFdkjv7bhQ",
          "mode": "list",
          "cachedResultName": "AI Email Reply Assistant",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1CzDtf9NdITNu2sJoVb0iut8J0U8XvpEF-rFdkjv7bhQ/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": 278418791,
          "mode": "list",
          "cachedResultName": "Sheet2",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1CzDtf9NdITNu2sJoVb0iut8J0U8XvpEF-rFdkjv7bhQ/edit#gid=278418791"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Date": "={{ $json.date }}\n",
            "From": "={{ $json.from && $json.from.text ? $json.from.text : ($json.from && $json.from.value && $json.from.value[0] ? ($json.from.value[0].name ? $json.from.value[0].name + ' <' + $json.from.value[0].address + '>' : $json.from.value[0].address) : '') }}\n",
            "Subject": "={{ $json.subject }}\n",
            "Snippet": "={{ $json.snippet ? $json.snippet : ($json.text ? $json.text.substring(0,200) : '') }}\n",
            "Sender Name": "={{ ($json.from && $json.from.value && $json.from.value[0] && $json.from.value[0].name) ? $json.from.value[0].name : '' }}\n",
            "Sender Email": "={{ ($json.from && $json.from.value && $json.from.value[0] && $json.from.value[0].address) ? $json.from.value[0].address : '' }}\n",
            "Message": "={{ $json.id }}\n",
            "Thread ID": "={{ $json.threadId }}\n"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "Date",
              "displayName": "Date",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "From",
              "displayName": "From",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Sender Name",
              "displayName": "Sender Name",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Sender Email",
              "displayName": "Sender Email",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Subject",
              "displayName": "Subject",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Snippet",
              "displayName": "Snippet",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "Message",
              "displayName": "Message",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Thread ID",
              "displayName": "Thread ID",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        816,
        -48
      ],
      "id": "a12f4671-91c7-4ca6-96ae-8d3861955c05",
      "name": "Append row in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "t15FzVcg0P9aEMKH",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "operation": "markAsRead",
        "messageId": "={{ $node[\"Get many messages\"].json[\"id\"] }}\n"
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.1,
      "position": [
        1408,
        32
      ],
      "id": "cbb29f49-5553-4cbe-8d83-97771e26e982",
      "name": "Mark a message as read",
      "webhookId": "730368b9-5ffa-44d0-80f8-a798c40ba976",
      "credentials": {
        "gmailOAuth2": {
          "id": "2hKPNNCWm4s43bgO",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "eaf7c153-2a54-42ce-882e-f77900dcb7b3",
              "name": "date",
              "value": "={{ ($json.date || '').replace('Date:', '').trim() }}\n",
              "type": "string"
            }
          ]
        },
        "includeOtherFields": true,
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        608,
        128
      ],
      "id": "15c551b8-a75b-4571-bc4c-b52c3f2f73a7",
      "name": "Normalize Date"
    },
    {
      "parameters": {
        "sendTo": "={{ $node[\"Append row in sheet\"].json[\"Sender Email\"] }}",
        "subject": "=Re: {{ $node[\"Append row in sheet\"].json[\"Subject\"] }}",
        "message": "={{ $json.content.parts[0].text }}",
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.1,
      "position": [
        1120,
        160
      ],
      "id": "a57a8770-0d53-4741-9b6d-17edde13595b",
      "name": "Send a message",
      "webhookId": "a33c357d-0868-46fd-b1ba-ee6070134dac",
      "credentials": {
        "gmailOAuth2": {
          "id": "2hKPNNCWm4s43bgO",
          "name": "Gmail account"
        }
      }
    },
    {
      "parameters": {
        "modelId": {
          "__rl": true,
          "value": "models/gemini-2.5-flash",
          "mode": "list",
          "cachedResultName": "models/gemini-2.5-flash"
        },
        "messages": {
          "values": [
            {
              "content": "You are a professional academic assistant.\nWrite polite, concise, human-like email replies. Also write my name at the end of every message Mohsin Awan.\n"
            },
            {
              "content": "=Reply professionally to this email:\n\nFrom: {{ $json[\"Sender Name\"] }} <{{ $json[\"Sender Email\"] }}>\nSubject: {{ $json[\"Subject\"] }}\n\nMessage:\n{{ $json[\"Snippet\"] }}\n"
            }
          ]
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.googleGemini",
      "typeVersion": 1,
      "position": [
        1024,
        -48
      ],
      "id": "03059fb6-62c1-45f0-b147-e422eb53e788",
      "name": "Message a model",
      "credentials": {
        "googlePalmApi": {
          "id": "TJFTMt9ISu9bQTph",
          "name": "Google Gemini(PaLM) Api account 7"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Get many messages",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get many messages": {
      "main": [
        [
          {
            "node": "Normalize Date",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Append row in sheet": {
      "main": [
        [
          {
            "node": "Message a model",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Normalize Date": {
      "main": [
        [
          {
            "node": "Append row in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Mark a message as read": {
      "main": [
        []
      ]
    },
    "Send a message": {
      "main": [
        [
          {
            "node": "Mark a message as read",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Message a model": {
      "main": [
        [
          {
            "node": "Send a message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": true,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "846d7a71-849f-485a-934e-12801759640f",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "2770290754f0310989c17fc8f84e5f2ae32982842da168d913db600669208db7"
  },
  "id": "R2AYwkS1oHeOq2dI",
  "tags": []
}
<img width="1110" height="461" alt="Screenshot 2025-12-17 092259" src="https://github.com/user-attachments/assets/0809aff3-0fc2-4fe6-8653-a0b35e8ed420" />
