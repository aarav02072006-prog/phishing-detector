# 🛡️ Phishing Detector

A browser extension that detects phishing websites in real time, especially fake copies of popular or government websites that are built to steal user data.

## Why this project?

Fraudsters create look-alike websites (like `sbii.co.in` instead of `sbi.co.in`) to trick people into entering passwords, OTPs, and banking details. Phishing Detector checks every page you visit and warns you *before* you share anything sensitive.

## Features

- 🔍 **Phishing probability score:** every website gets a risk score from 0 to 100
- 🎭 **Look-alike domain detection:** catches typosquatting and character tricks (`g00gle.com`, `rn` vs `m`) using edit distance against a list of trusted domains
- 📄 **Page content analysis:** flags password forms that submit data to a different domain
- 🚨 **Alarming notifications:** desktop alerts, a red badge on the extension icon, and a full-page warning screen for dangerous sites
- ✅ **Whitelist:** mark sites you trust so they are never flagged
- 🌐 **Cross-browser:** works on Chrome, Edge, Brave, and Firefox

## How it works

| Score | Level | Action |
|---|---|---|
| 0-30 | 🟢 Safe | No action |
| 30-70 | 🟡 Suspicious | Yellow badge + popup details |
| 70-100 | 🔴 Dangerous | Notification + warning page |

The score is calculated from multiple signals:

- No HTTPS, IP address used as domain, `@` in URL, very long URLs
- Too many subdomains, punycode (`xn--`) characters
- Suspicious keywords (`login`, `verify`, `secure`)
- Similarity to trusted domains (Levenshtein distance)
- Password fields posting to external domains

## Tech Stack

- **Extension:** JavaScript, HTML, CSS, Chrome Extension Manifest V3
- **Planned:** Python, FastAPI, and scikit-learn for an ML-based detection layer

## Project Structure

```
phishing-detector/
├── extension/    # Browser extension source
│   ├── manifest.json
│   ├── background.js
│   ├── content.js
│   ├── popup/
│   ├── warning/
│   └── lib/      # rules, similarity, scorer, trusted domains
├── backend/      # (planned) ML API
├── ml/           # (planned) model training
└── tests/
```

## Installation (Developer Mode)

1. Clone the repository
   ```bash
   git clone https://github.com/<your-username>/phishing-detector.git
   ```
2. Open `chrome://extensions` (or `edge://extensions`)
3. Turn on **Developer mode**
4. Click **Load unpacked** and select the `extension/` folder

## Roadmap

- [x] Project setup
- [ ] Rule-based URL analysis
- [ ] Look-alike domain detection
- [ ] Page content analysis
- [ ] Notifications and warning page
- [ ] Firefox support
- [ ] ML model (Random Forest / XGBoost)
- [ ] Backend API

## Privacy

The extension analyzes URLs locally in your browser. No browsing history is collected or stored.

## Disclaimer

This tool reduces risk but cannot guarantee 100% detection. Always verify website addresses before entering sensitive information.

## Author

Built by **Aarav** — BTech CSE student.

## License

MIT
