# Weekly AI Cybersecurity Report

A GitHub Actions workflow that uses **Google Gemini AI** to generate a weekly
cybersecurity briefing and email it to you every Monday morning.

---

## Setup

### 1. Repo structure

```
your-repo/
├── .github/
│   └── workflows/
│       └── weekly-report.yml
├── generate_report.py
└── README.md
```

### 2. Get a Gemini API key

1. Go to https://aistudio.google.com/app/apikey
2. Click **Create API key**
3. Copy the key

### 3. Configure your email (SMTP)

You need an SMTP server to send the email. Two easy options:

**Gmail (recommended):**
- Enable 2FA on your Google account
- Go to https://myaccount.google.com/apppasswords
- Create an app password for "Mail"
- Use these settings:
  - `SMTP_HOST` = `smtp.gmail.com`
  - `SMTP_PORT` = `587`
  - `SMTP_USER` = your Gmail address
  - `SMTP_PASS` = the app password (not your regular password)

**SendGrid (free tier available):**
- Sign up at https://sendgrid.com
- `SMTP_HOST` = `smtp.sendgrid.net`
- `SMTP_PORT` = `587`
- `SMTP_USER` = `apikey`
- `SMTP_PASS` = your SendGrid API key

### 4. Add GitHub Secrets

Go to your repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

Add these 6 secrets:

| Secret name     | Value                          |
|-----------------|--------------------------------|
| `GEMINI_API_KEY` | Your Gemini API key           |
| `SMTP_HOST`     | e.g. `smtp.gmail.com`          |
| `SMTP_PORT`     | e.g. `587`                     |
| `SMTP_USER`     | Your sender email address      |
| `SMTP_PASS`     | Your email password/app password |
| `EMAIL_TO`      | Address to receive the report  |

### 5. Push to GitHub

Commit and push all three files. The workflow will run automatically every
Monday at 8:00 AM UTC.

**To test immediately:** go to Actions → Weekly Cybersecurity Report →
Run workflow → Run workflow.

---

## Customisation

- **Schedule:** edit the `cron` line in `weekly-report.yml`
  - `'0 8 * * 1'` = Monday 8am UTC
  - `'0 8 * * 5'` = Friday 8am UTC
  - Use https://crontab.guru to build custom schedules

- **Report content:** edit the `PROMPT` variable in `generate_report.py`
  to focus on specific industries, threat types, or regions

- **Gemini model:** change `gemini-1.5-flash` to `gemini-1.5-pro` for
  a more detailed report (uses more quota)
