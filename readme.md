# ⚡ PulseSpend — Zero-Cost AI Expense, Debt & Loan Command Center

A **100% free, zero-server-maintenance** personal finance operating system built around a **Telegram Bot**, **Google Sheets**, **Google Apps Script**, **Gemini AI (Free Tier)**, and a **GitHub Pages Web App**.

🔗 **Live Master Google Sheet Database:** [Expense, Debt & Loan Tracker — Mandar](https://docs.google.com/spreadsheets/d/1Bq0bAoPOx3mBjfX2VavyvVGFmWC4p8b00D_TsqHEjLM/edit)

---

## 🧠 1. Why We Built It This Way (Architecture & Design Decisions)

Most expense trackers fail for one of three reasons: **logging takes too many taps**, **categories are rigid dropdowns**, or **hosting a backend database costs money/sleeps on free tiers**. Here is how we solved all three:

| Decision | What We Chose | Why We Did It |
| :--- | :--- | :--- |
| **Input Friction** | [Telegram Bot API](https://core.telegram.org/bots/api) | Sending a 2-word message (`180 coffee` or `850 petrol cc`) takes 2 seconds right after a UPI or card payment—zero app loading screens. |
| **Daily Habit Loop** | **11:00 AM IST Morning Check-In** | Nighttime reminders often get ignored when you're tired or out for dinner. An **11:00 AM reminder** the next morning lets you review and log **yesterday's** missed expenses in one 30-second batch using **Yesterday Mode**. |
| **24/7 Backend & Cron** | [Google Apps Script](https://developers.google.com/apps-script/overview) | Runs 24/7 on Google's cloud for **₹0 forever**. Unlike free cloud containers (Render/Fly) that cold-start or expire, Apps Script webhooks never sleep and include native time-driven triggers. |
| **Database** | [Google Sheets](https://developers.google.com/apps-script/guides/sheets) | Gives you a transparent, editable 5-tab ledger (`Dashboard`, `Expenses`, `Debt_IOUs`, `Loans_EMIs`, `Categories_Config`) stored on your own Google Drive. |
| **Categorization Engine** | [Google AI Studio (Gemini API)](https://aistudio.google.com/docs/api-key) | Instead of fixed dropdowns, Gemini maps natural English to `Main Category › Sub-Category` and **automatically creates new sub-categories** inside `Categories_Config` whenever you spend on something new. |
| **Debt & Loan Isolation** | Dedicated `Debt_IOUs` & `Loans_EMIs` Tabs | Mixing friend IOUs (`owe Chirag 600`) or repayments (`paid 500 back to Rashi`) into regular expenses distorts your monthly burn rate. Isolating them keeps lifestyle burn accurate while tracking net counterparty balances. |
| **Frontend Web UI** | Vanilla JS + Tailwind on [GitHub Pages](https://pages.github.com/) | A single-file, zero-build-step JavaScript app (`index.html`) with smooth physics animations and dark studio aesthetics (`#0C0C0A` Obsidian, `#77E7FE` Glacier Blue, `#F15412` Blaze Orange) that deploys for free on GitHub Pages and works on both mobile and desktop browsers. |

---

## 🏗️ 2. Repository Structure & Files

* **`index.html`** — The standalone JavaScript Web App UI. Hosts directly on [GitHub Pages](https://docs.github.com/en/pages/quickstart) and works smoothly on mobile (with a bottom navigation dock) and desktop browsers.
* **`telegram_expense_bot_apps_script.js` (`Code.gs`)** — The complete [Google Apps Script](https://developers.google.com/apps-script/overview) backend pasted into your Google Sheet (**Extensions → Apps Script**). Pre-configured with your Spreadsheet ID (`1Bq0bAoPOx3mBjfX2VavyvVGFmWC4p8b00D_TsqHEjLM`).
* **`README.md`** — Full documentation, architecture rationale, deployment checklist, and Telegram command cheat sheet.

---

## 🚀 3. Step-by-Step Setup & Activation Guide

### Step 1: Create Your Telegram Bot Token (1 Min)
1. Open [@BotFather](https://t.me/botfather) in Telegram and send `/newbot`.
2. Enter a display name (e.g., `PulseSpend Tracker`) and a username ending in `bot`.
3. Copy the HTTP API token (`TELEGRAM_BOT_TOKEN`).

### Step 2: Get Your Free Gemini API Key (1 Min)
1. Open [Google AI Studio API Keys](https://aistudio.google.com/docs/api-key).
2. Click **Create API Key** on the free tier (no credit card or billing required).
3. Copy the key (`GEMINI_API_KEY`).

### Step 3: Paste the Script into Your Google Sheet (2 Mins)
1. Open your Google Sheet: [Expense, Debt & Loan Tracker — Mandar](https://docs.google.com/spreadsheets/d/1Bq0bAoPOx3mBjfX2VavyvVGFmWC4p8b00D_TsqHEjLM/edit).
2. Click **Extensions → Apps Script** in the top menu bar.
3. Replace any starter code in `Code.gs` with the contents of `telegram_expense_bot_apps_script.js`.
4. At the top of `Code.gs` inside `CONFIG`, paste your `TELEGRAM_BOT_TOKEN` and `GEMINI_API_KEY` (your `SPREADSHEET_ID` is already pre-filled).

### Step 4: Deploy Web App & Activate the 11:00 AM Reminder Trigger (1 Min)
1. In the Apps Script editor, click **Deploy → New deployment**.
2. Choose **Web app**, set **Execute as: Me**, and set **Who has access: Anyone**.
3. Click **Deploy**, authorize access once, and copy the resulting `https://script.google.com/macros/s/.../exec` Web App URL.
4. Paste that URL into `WEB_APP_URL` inside the `setupEverything()` function in `Code.gs`.
5. In the Apps Script top toolbar, select `setupEverything` from the function dropdown and click **Run**.
   * **What this does automatically:** Links your Telegram Bot webhook to your Google Sheet AND installs a daily time-driven trigger at **11:00 AM IST** (`sendMorning11AMReminder`).
6. Open your bot in Telegram and send `/start` once so it saves your `TELEGRAM_CHAT_ID`.

### Step 5: Host the Web Dashboard on GitHub Pages (2 Mins)
1. Create a new repository on GitHub (e.g., `expense-tracker`) and upload `index.html` and `README.md` to the root of the `main` branch.
2. Go to **Settings → Pages** in your GitHub repository ([GitHub Pages Quickstart](https://docs.github.com/en/pages/quickstart)).
3. Under **Build and deployment**, select **Deploy from a branch** → Branch: `main` / `/ (root)` and click **Save**.
4. Open your live URL (`https://<your-username>.github.io/expense-tracker/`), click **Live API Sync** in the top bar, and paste your Apps Script Web App URL.

---

## 💬 4. How the Daily Process Works (Telegram Cheat Sheet)

### A. Logging Regular Expenses
| What You Text the Bot | What Happens in Google Sheets & Dashboard |
| :--- | :--- |
| `180 filter coffee` | Logs `₹180` under **Today**, `Food & Dining › Cafes & Snacks`, Payment Mode: `UPI`. |
| `850 petrol cc` | Appending `cc` or `card` logs `₹850` under `Transit & Vehicle › Fuel & Petrol` with Payment Mode: `Credit Card`. |
| `60 chai, 140 auto, 520 groceries` | Splits comma-separated items and logs all 3 rows at once with their respective categories. |
| `950 helmet anti-fog visor` | If no sub-category fits, Gemini **coins a new sub-category** (`Riding Gear`), saves it to `Categories_Config`, and tags the row. |

### B. The 11:00 AM Yesterday Check-In Workflow
* Every day at **11:00 AM IST**, your bot sends:
  > *"☀️ 11:00 AM Daily Expense Check-In! For Yesterday (YYYY-MM-DD), you logged X item(s) totaling ₹Y. Did you have any other spends, split bills, or IOUs yesterday?"*
* Tap **[📅 Log Yesterday's Spends Now]** in the message: for the next 30 minutes, every message you send automatically records under **Yesterday's Date**.
* You can also log under yesterday anytime without tapping the button by adding `yest` or `yesterday` to your text (e.g., `yest 450 dinner`).
* Every logged expense also has a 1-tap **[📅 Move to Yesterday]** button right underneath the confirmation message.

### C. Managing "Debt I Owe", Bill Splits & Loan EMIs
| What You Text the Bot | How the Ledger Updates |
| :--- | :--- |
| `owe Chirag 600 for dinner` | Logs `₹600` in `Expenses` (`Food & Dining › Dining Out`) **AND** adds `+₹600` (`I_OWE`) under Chirag in `Debt_IOUs`. |
| `borrowed 2000 from Rashi` | Adds `+₹2,000` (`I_OWE`) under Rashi in `Debt_IOUs` without inflating food/shopping spend. |
| `paid 500 back to Rashi` | Logs `-₹500` (`I_PAID_BACK`) in `Debt_IOUs`, reducing your net debt to Rashi without double-counting as a new expense. |
| `paid 900 badminton, Aman owes 450` | Logs only your `₹450` share in `Expenses` and records `+₹450` (`OWED_TO_ME`) under Aman in `Debt_IOUs`. |
| `paid home loan EMI` | Increments `Months_Paid` by `+1` in `Loans_EMIs`, updates remaining tenure, and logs the EMI outflow. |

### D. Slash Commands on Telegram
* `/summary` — Instant Month-to-Date spend breakdown by category.
* `/yesterday` — Turn on Yesterday Mode for 30 minutes.
* `/today` — Switch back to Today Mode immediately.
* `/debts` — Live person-by-person tally of **Who You Owe** and **Who Owes You**.
* `/loans` — Active loan EMIs, installments paid, and remaining months.
* `/categories` — View all Main and Sub-Categories (including ✨ AI-created ones).

---

## 🎨 5. Design System & Color Psychology (`@lnunesdesigns` Palettes)

Following the **85% neutral canvas / 15% surgical accent** principle:
* **Obsidian Black (`#0C0C0A`) & Matte Glass (`#141413`):** Eliminates visual clutter and eye strain on both OLED mobile screens and desktop monitors.
* **Glacier Blue (`#77E7FE`):** Used strictly for primary interactive pills, positive cashflow, UPI transactions, money owed to you, and ✨ AI-generated sub-categories.
* **Blaze Orange (`#F15412`):** Used for high-energy velocity indicators—Monthly Spend Burn, Credit Card milestone outflows, and the 11:00 AM Yesterday Mode banner.
* **Scarlet / Burnt Red (`#E62726`):** Reserved strictly for liabilities (`Debt I Owe`).
* **Stone Blue (`#6497B1`) & Egyptian Blue (`#081B33`):** Used for structured long-term Loan EMI amortization and optional theme switching.
