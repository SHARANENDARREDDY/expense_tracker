# 🤖 AI-Powered Telegram Expense Tracker

An AI-powered expense tracking automation built using **n8n, Telegram, Google Sheets, and OpenRouter**. Record expenses using natural language through Telegram, automatically extract expense details with an AI model, and store the data in Google Sheets. A separate scheduled workflow generates monthly expense reports and sends them through Telegram.

## ✨ Features

- 💬 **Natural Language Expense Entry:** Send messages like `Spent ₹500 on groceries` through Telegram.
- 🧠 **AI-Powered Extraction:** Uses an LLM to identify the amount, category, description, and expense date.
- 📊 **Google Sheets Integration:** Automatically stores expense records in a spreadsheet.
- 🔔 **Telegram Notifications:** Receives confirmation after an expense is recorded.
- 📅 **Automated Monthly Reports:** Generates a monthly report containing total spending, number of expenses, and category-wise breakdown.
- ⏰ **Scheduled Automation:** Uses n8n Schedule Trigger to run the monthly reporting workflow automatically.

## 🛠️ Tech Stack

| Technology       | Purpose                                  |
| ---------------- | ---------------------------------------- |
| n8n              | Workflow automation                      |
| Telegram Bot API | Expense entry and notifications          |
| OpenRouter       | AI model access                          |
| Google Sheets    | Expense data storage                     |
| JavaScript       | JSON parsing and report calculations     |
| ngrok            | Public webhook URL for local development |

## ⚙️ How It Works

### Workflow 1: Expense Tracking

1. The Telegram Trigger receives a message.
2. The Edit Fields node extracts the message and chat ID.
3. The AI model interprets the expense details.
4. A JavaScript Code node parses and validates the AI-generated JSON.
5. Google Sheets stores the expense record.
6. Telegram sends a confirmation message.

### Workflow 2: Monthly Expense Report

1. The Schedule Trigger runs daily near the end of the day.
2. An IF node checks whether it is the last day of the month.
3. Google Sheets retrieves expense records.
4. A JavaScript Code node filters the current month's records and calculates totals.
5. The report is sent to Telegram automatically.

## 📋 Example

**Telegram input:**

```text
Spent ₹500 on groceries today
```

**Extracted expense details:**

```json
{
  "amount": 500,
  "category": "Food",
  "description": "groceries",
  "date": "YYYY-MM-DD"
}
```

The AI determines the actual date based on the message and current date.

**Example monthly report:**

```text
📊 MONTHLY EXPENSE REPORT
📅 October 2026

💰 Total Spent: ₹8,500.00
🧾 Number of Expenses: 15

📂 CATEGORY BREAKDOWN
• Food: ₹3,500.00
• Transport: ₹2,000.00
• Shopping: ₹1,500.00
• Bills: ₹1,500.00
```



## 🚀 Setup Requirements

Before setting up the project, you need:

- A running n8n instance.
- A Telegram bot created using BotFather.
- A Google account with Google Sheets access.
- An OpenRouter API key and an available model.
- ngrok or another HTTPS-accessible endpoint when exposing "a locally hosted n8n instance".

## 🔧 Setup Instructions

1. Create a Telegram bot using [BotFather](https://t.me/BotFather).

2. Set up a Google Sheet with these column headers:

   `ID | Amount | Category | Description | Date | Chat ID`

3. Configure your Telegram, Google Sheets, and OpenRouter credentials in n8n.

4. Build the expense tracking workflow and connect the nodes described above.

5. Create the separate monthly reporting workflow.

6. Configure the schedule and set the workflow timezone to `Asia/Kolkata`.

7. Activate both workflows and test them using Telegram.

**Important:** When running n8n locally, keep the n8n process and the HTTPS tunnel running for scheduled workflows and Telegram webhooks to work reliably.

## 🔐 Security

- Never commit API keys, bot tokens, credentials, or `.env` files to GitHub.
- Use n8n credentials to store sensitive authentication information.
- Keep personal expense records and Google Sheets private.
- Use environment variables for sensitive configuration where appropriate.

## 🔮 Future Improvements

- Add `/list` and `/total` Telegram commands.
- Add budget limits and spending alerts.
- Add charts and monthly spending trends.

