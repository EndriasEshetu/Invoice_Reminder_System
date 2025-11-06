### 📘 System Overview: Payment Reminder Automation

This automation is built in **Make.com (formerly Integromat)** to automatically identify overdue unpaid invoices from a Google Sheet and send reminder emails via Gmail. It runs on a daily or weekly schedule without manual intervention.

---

### 🧩 Workflow Summary

The system performs the following actions:

1. **Scheduled trigger** – runs automatically each morning (or weekly).
2. **Google Sheets lookup** – finds rows where `Status = "Unpaid"` and the `Due Date` is earlier than today.
3. **Filter and iterate** – checks each row individually to confirm the invoice is overdue.
4. **Email sending (Gmail)** – sends a personalized reminder email to the client.
5. **Sheet update** – logs that a reminder was sent for recordkeeping and to prevent duplicates.

---

### ⚙️ Step-by-Step Breakdown

#### 1. Scheduler (Trigger)

* **Module:** Scheduler → “Every day at 08:00 AM” (Addis Ababa time)
* **Purpose:** Automatically starts the workflow on the selected schedule.
* **Outcome:** Initiates the process daily/weekly without user input.

#### 2. Google Sheets: Search Rows

* **Module:** Google Sheets → “Search Rows”
* **Purpose:** Retrieve all invoice records from the designated spreadsheet.
* **Filter Criteria:**

  * `Status = Unpaid`
* **Outcome:** Produces a list of all clients with unpaid invoices.

#### 3. Iterator (Loop through each row)

* **Module:** Tools → “Iterator”
* **Purpose:** Split the list of rows so each invoice is processed separately.
* **Outcome:** Enables individual handling (email + update) per client.

#### 4. Filter: Check Overdue Invoices

* **Condition:**

  * `Due Date < Today`
* **Purpose:** Ensure reminders are only sent for invoices that are past due.
* **Outcome:** Prevents premature or duplicate reminder emails.

#### 5. Gmail: Send Reminder Email

* **Module:** Gmail → “Send an Email”
* **To:** Client email from the sheet (`Client Email` column)
* **Subject:** “Payment Reminder — Invoice Due {{Due Date}}”
* **Body:** Personalized message referencing the due date and client name.
* **Outcome:** Client receives a reminder directly in their inbox.

#### 6. Google Sheets: Update Row

* **Module:** Google Sheets → “Update Row”
* **Purpose:** Record that a reminder was sent to this client.
* **Action:**

  * Update “Reminder Sent” column with the current date/time.
* **Outcome:** Prevents duplicate reminders and creates a log for tracking.

---

### 🧠 Example Workflow Logic (Simplified)

```
Every day at 8:00 AM →
  Search Google Sheet rows (Status = "Unpaid") →
  For each row:
      If Due Date < Today:
          Send Gmail reminder →
          Update sheet (Reminder Sent = Today)
```

---

### 🧾 Benefits

* Fully **automated**—no manual checking or emailing.
* Ensures **timely follow-up** with clients on overdue invoices.
* Keeps an **accurate audit trail** within Google Sheets.
* Saves administrative time and reduces missed payments.

---

### 🧰 Tech Stack

* **Platform:** Make.com (No-code automation)
* **Data Source:** Google Sheets
* **Email Service:** Gmail API integration
* **Execution Frequency:** Daily (08:00 local time)
* **Logging:** Google Sheet column update (“Reminder Sent”)

---

**Import Instructions**
1. Go to **Make.com → Scenarios → Create Scenario → Import Blueprint( three dot "..." right bottom)**
2. Upload the JSON file above.
3. Reconnect your Google Sheets and Gmail accounts.
4. Run once to test the setup.

---

### 🚀 Future Improvements

* Add Slack/Telegram notifications when reminders are sent.
* Include multi-step logic for second/third reminders.
* Integrate with payment systems (e.g., Stripe or PayPal) for automatic status updates.

---

* **Created by:** Endrias Eshetu
* **Automation Name:** *Invoice Reminder System*
* **Platform:** Make.com
* **Status:** ✅ Operational and verified
