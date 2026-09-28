# QTB Bank

A small demo online bank built as a **test target for AI testing agents**.

QTB Bank looks and behaves like a simple retail banking app, but one of its users has a set of deliberately seeded defects. That makes it a controlled environment for measuring how well an autonomous testing agent finds real bugs, and how often it raises false alarms.

**Live demo:** https://qtb-bank.vercel.app <!-- replace with your Vercel URL -->

> No real money, accounts or personal data. Everything resets when you reload the page.

---

## Demo users

| Username | Password | Behaviour |
|----------|----------|-----------|
| `alex`   | `demo123` | Clean app. Everything works as intended. |
| `sam`    | `demo123` | Same app with seeded defects switched on. |

Running the same tests as both users gives two numbers: **bugs found** (as `sam`) and **false alarms** (as `alex`).

The list of seeded defects is kept private on purpose, so that agents and testers are scored fairly and can't look up the answers.

---

## Features

- **Accounts:** balances for a checking and a savings account, recent transactions, search, and statement download
- **Transfer:** move money between your own accounts, with amount and balance validation
- **Pay bills:** pay a utility bill from checking on a chosen date
- **Loan calculator:** monthly payment and total interest for a loan amount, rate and term
- **Profile:** update email and phone number
- **Help** page and sign-out

Every interactive element has a stable `data-testid`, so the app is easy to automate with Playwright, Selenium or Cypress.

---

## Why this exists

Most AI testing demos run against apps whose bugs are unknown or already documented online, so there's no reliable way to say how good the agent really is. QTB Bank has a **known, private answer key**, which makes it possible to report measurable results, for example:

- detection rate: bugs found out of the total seeded
- false-alarm rate on the clean user
- which kinds of bugs need LLM reasoning versus simple detectors (console errors, failed network calls, broken links, accessibility checks)

It is the target app for an autonomous AI bug-hunting agent built with **Playwright, LangGraph and Groq** (in progress).

---

## Run locally

Requirements: Python 3 (for a simple local web server).

```bash
git clone https://github.com/<your-username>/qtb-bank.git
cd qtb-bank
python -m http.server 8000
```

Then open http://localhost:8000.

Serving the app over HTTP (instead of double-clicking `index.html`) matters, because some behaviour depends on real server responses.

## Deploy

The app is a single static `index.html` with no build step. On Vercel: **Add New → Project →** import this repo **→** Framework Preset **Other → Deploy**. Any static host (Netlify, GitHub Pages, Cloudflare Pages) works the same way.

---

## Tech

- One self-contained HTML file: plain HTML, CSS and JavaScript
- No frameworks, no dependencies, no backend
- In-memory data only (nothing is stored in the browser)

## Usage note

Feel free to point your own testing tools and agents at the live demo. Please keep automated runs reasonable in volume.

---

Built by **Nancy Bhardwaj**, Lead QA Engineer and Test Automation Architect, as part of a portfolio on AI-augmented testing.
