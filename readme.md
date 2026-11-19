⚡ PulseSpend v2 — Open-Source Personal Money Manager

A 100% free, zero-server, privacy-first personal money manager powered by Telegram, Google Sheets, Google Apps Script, Gemini AI, and GitHub Pages.

No subscriptions, no third-party bank aggregators reading your SMS, and no hosting bills. Fork this repo, plug in your own Google Sheet + Telegram Bot, and run your own private money OS forever.

✨ What PulseSpend v2 Does (Phase 1)

Cashflow & Investable Surplus Engine: Tracks Income (Income_Cashflow) − Fixed Loan EMIs (Loans_EMIs) − Lifestyle Spend (Expenses) = Free Surplus / SIP Capacity across any month (‹ Oct 2026 | Nov 2026 | Dec 2026 ›).

2-Second Telegram Logging + Self-Evolving AI Categories: Message your bot 180 filter coffee, 850 petrol cc, or salary 95000. Gemini (gemini-2.5-flash) categorizes every spend into Main Category › Sub-Category and automatically creates new sub-categories inside Categories_Config when you log something new.

11:00 AM Daily Yesterday Check-In: Automated Google Apps Script trigger pings you every morning at 11:00 AM with yesterday's spend total and a 1-tap Yesterday Mode button so you never miss logging previous-day spends.

Personal Debt ("Debt I Owe") & Split Bills: Understands Borrowed 66500 from Mayank, I owe 600 to Chirag for dinner, paid 500 back to Rashi, and paid 800 badminton, Aman owes 450—tracking net balances without inflating lifestyle burn.

Full Loan, Prepayment & Mortgage Studio: Add loans (add loan Education Loan 450000 at 9.5% emi 12500 for 48 months), log lump-sum prepayments (prepaid 100000 on education loan with automatic months & interest saved math), archive paid-off loans (closed education loan), and simulate prepayments with live sliders in the web UI.

True 2-Way Sync: Deleting an expense, flipping UPI ↔ Card, settling a debt, logging an EMI, or applying a loan prepayment on the website syncs straight back to your Google Sheet.

🔒 Open-Source Privacy Architecture

Why it is safe to open-source this repository:

index.html contains zero personal data, zero API keys, and zero hardcoded URLs. Anyone visiting your live GitHub Pages site sees only the clean demo dataset until they paste their own private Apps Script /exec URL into Connect (which is saved strictly in their own browser's localStorage).

All secrets (TELEGRAM_BOT_TOKEN, GEMINI_API_KEY) live only inside your private Google Sheet's Apps Script editor—never commit filled-in tokens to GitHub.

🚀 Deploy Your Own Instance in 5 Minutes

Fork & Enable GitHub Pages: Fork this repository, go to Settings → Pages (GitHub Pages Quickstart), and deploy from main / / (root).

Create Your Google Sheet: Create a Google Sheet with 6 tabs: Dashboard, Expenses, Income_Cashflow, Debt_IOUs, Loans_EMIs, and Categories_Config (or let setupEverything() auto-create them).

Get Your Free Keys:

Telegram Bot Token from @BotFather (/newbot).

Free Gemini API Key from Google AI Studio (no billing card required).

Deploy Apps Script Backend: In your Google Sheet, open Extensions → Apps Script (Google Apps Script Guide), paste telegram_expense_bot_apps_script.js, fill in CONFIG (or Project Settings → Script Properties), click Deploy → New deployment → Web app (Execute as: Me, Who has access: Anyone), paste the /exec URL into CONFIG.WEB_APP_URL, and click Run → setupEverything.

Connect & Verify:

Send /start and /test_ai to your Telegram bot to confirm Gemini is live.

Open your GitHub Pages site, click Connect, and paste your /exec URL.

🗺️ Roadmap (Phase 2 — Wealth & Net Worth)

Portfolio Tab (=GOOGLEFINANCE()): Live Indian & US Stocks + Mutual Fund SIP tracking.

Telegram Investment Commands: sip 15000 ppfas, bought 10 tatapower at 420, and /networth.

Net Worth Milestones: Automated Assets − Liabilities (Loans + Personal Debts) trajectory.

📄 License

Released under the MIT License. Contributions, forks, and PRs are welcome!
