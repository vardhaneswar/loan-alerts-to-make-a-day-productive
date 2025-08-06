# loan-alerts-to-make-a-day-productive


As an international student, I built a simple solution that works as a daily pill to stay productive and keep priorities from slipping. To leverage my day, I created an email and Telegram alert that shows my current monthly interest, its increase, and total principal accrued. This attention makes me work hard.


# 🎓📊 Daily Education Loan Tracker (Fixed Interest Edition)

This project is a **fully automated, serverless daily loan tracking system** built to help students stay motivated and informed about their education loan. Unlike floating-rate models, this version uses a **fixed annual interest rate**, making it ideal for loans like those from **HDFC Credila**.

It reads disbursement data from a **Google Sheet**, calculates **daily interest**, and sends updates via **Telegram and Email** using **AWS Lambda, EventBridge, SNS**, and a **custom Telegram bot**.

---

## 🗂️ System Architecture

```
1️⃣ EventBridge → 2️⃣ Lambda → 3️⃣ Google Sheets → 4️⃣ SNS → 5️⃣ Telegram & Email
<img width="892" height="632" alt="3 drawio" src="https://github.com/user-attachments/assets/55735ee2-9542-422b-82d8-6acf34d0839a" />

```

> ✅ 100% serverless & automated with fixed interest logic

---

## ⚙️ How It Works

* 📅 Loan disbursement info → stored in **Google Sheets**
* ⏰ **AWS EventBridge** triggers Lambda daily
* 🧠 **Lambda** reads sheet, calculates interest
* 📣 **SNS** sends notifications to Email & Telegram

---

## ✅ Functional Requirements

* 📄 Fetch loan data from Google Sheet
* 🧮 Compute interest using **fixed rate (11.25%)**
* 🔔 Push daily alert to:

  * 📧 Email (via SNS)
  * 💬 Telegram Bot
* 🕓 Run daily via cron schedule

### ⚙️ Non-Functional

* 💡 Reliable, cheap, and serverless
* 🔐 Secure via env vars (tokens, secrets)
* 📈 Scalable to multiple channels
* 🔁 Idempotent – handles retries without duplication

---

## 📊 Capacity Planning

* 👤 Daily Users: 1 (Me)
* 🧠 Lambda: 1 call/day
* 📄 Google Sheet: Few KB
* 🌐 Bandwidth: Minimal (HTTPS + SNS)

---

## 🧩 API Design

* Google Sheets API → read disbursement
* SNS API → push email
* Telegram Bot API → send message

---

## 🏗️ High-Level Design

| Component     | Purpose                 |
| ------------- | ----------------------- |
| EventBridge   | Triggers function daily |
| Lambda        | Core logic & compute    |
| Google Sheets | Acts as DB              |
| SNS           | Sends Email/Telegram    |
| Telegram Bot  | Receives message        |

---

## 🔍 Deep Dive (Fixed Interest Model)

* Interest rate is **fixed** at `11.25%` annually (as per HDFC Credila)
* First EMI shown in loan schedule → ₹10,125 for 20 days = ₹506.25/day
* Lambda uses this rate to calculate:

  * 🔹 `interest_today = ₹506.25`
  * 🔹 `total_interest = ₹506.25 × days_elapsed`
  * 🔹 `total_outstanding = disbursed + total_interest`

---

## 🛡️ Security, Logging & Monitoring

* Secrets stored as Lambda **environment variables**
* Logging via **CloudWatch**
* Monitoring via **SNS failure alerts** or optional CloudWatch Alarms

---

## 📬 Example Alert

```
📢 Credila Loan Update

📌 Loan Disbursed: ₹1,892,313.00
📅 Disbursed On: 22 Dec 2023
💰 Interest Rate: 11.25% per annum (Fixed)

📈 Interest Accrued So Far: ₹298,687.50
💸 Today's Interest: ₹506.25
🧮 Total Outstanding: ₹2,191,000.50
📆 Days Passed: 590 days

🧠 “Stay disciplined — little drops of effort fill the bucket of success.” 💪
```

---

## 📦 Setup Instructions

### 🔐 1. Google Sheets API

* Create GCP project
* Enable **Sheets API** & **Drive API**
* Create **Service Account** → download `service_account.json`
* Share your Google Sheet with that service account email

### ☁️ 2. AWS Setup

* Create SNS topic + subscribe your email
* Create Lambda function:

  * Upload ZIP with code + dependencies
  * Add environment variables:

    * `TELEGRAM_TOKEN`
    * `TELEGRAM_CHAT_ID`
    * `SNS_TOPIC_ARN`
* Setup **EventBridge rule** with daily cron

### 🧪 3. Local Testing

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python index.py
```

---

## 💰 Cost Estimate

| Service    | Usage       | Monthly Cost    |
| ---------- | ----------- | --------------- |
| Lambda     | \~30 runs   | \$0 (free tier) |
| SNS        | \~30 emails | \$0 (free tier) |
| Sheets API | Light       | \$0 (free)      |

> ⚡ Total Monthly Cost: **\$0.00** ✅

---

## 📜 License

Licensed under the **MIT License**. Feel free to fork and improve.

---

## 🚀 Why This Matters

A real-world example of:

* Serverless automation
* Personal finance tracking
* Motivation via daily insights

**Built to help myself (and others) repay student loans — one day at a time.**

---

## 🤝 Connect

Feel free to [connect on LinkedIn](https://www.linkedin.com/in/eswar-vardhan-3624611b6/) or fork this repo if this helps you stay disciplined too!
