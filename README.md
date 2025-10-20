# Invoice Genie — AI Invoice Data Extractor

This repository contains a client UI (Invoice Genie) that allows users to upload invoice images, request an extraction prompt, and receive structured data. The client saves extracted results to Firestore.

---

## 🚀 Launch Steps

1. **Configure Firestore and Firebase Authentication**
   - Provide a Firebase config object to the client environment (see `index.html` placeholders).
   - Ensure Firestore Security Rules are set to only allow expected reads/writes.
   - Prefer using custom tokens for authenticated access where required.

2. **Deploy or run a serverless proxy for Gemini**
   - Create a serverless function (see `functions/gemini-proxy/`) and set the following environment variable:
     - `GEMINI_API_KEY=your_real_gemini_api_key`
   - Deploy to your provider (Google Cloud Functions, Cloud Run, Vercel, Netlify Functions, etc.)

3. **Update client configuration**
   - Remove hard-coded API keys from `index.html`.
   - Point client calls to your serverless endpoint (e.g., `/api/extract`).

---

## Security checklist

- Ensure firebase project uses secure Firestore rules (limit writes to authenticated users and require validation of data shape).
- Keep `GEMINI_API_KEY` out of client bundles and source control; use environment variables in server deployments.
- Monitor usage and set quotas or rate-limits on the proxy endpoint.

---

## Features

- Upload invoice images (PNG/JPEG)
- Extract vendor, date, total, and more using Gemini AI
- Save data to Firestore for each user
- Export results as JSON and CSV

---

## Proxy server (functions/gemini-proxy/index.js)

A serverless Express API that proxies requests to Gemini, keeping your API key safe.

---

## Suggested improvements

- Harden JSON and CSV extraction logic (support nested objects/arrays)
- Add automated tests for CSV and JSON conversion logic
- Add accessibility improvements and keyboard support for the UI
- Add CI and linting

---

**When ready, merge this branch and deploy your proxy for a secure launch!**
