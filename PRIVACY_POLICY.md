# Privacy Policy — GarminWO Chrome Extension

**Last updated: April 15, 2026**
**Version: 1.4.2**

---

## Overview

GarminWO is a free Chrome extension that imports running workouts into Garmin Connect by analysing workout photos or text using AI (Google Gemini or Anthropic Claude). This policy explains what data is collected, how it is used, and what your rights are.

**Summary: GarminWO collects no personal data, has no backend server, and never sells or shares your information.**

---

## 1. Data Collected and How It Is Used

### 1.1 API Keys
- **What:** Your Gemini (Google) or Claude (Anthropic) API key, entered voluntarily in the extension popup.
- **Where stored:** Locally on your device only, via Chrome's `chrome.storage.local` API.
- **Never:** Transmitted to any GarminWO server (there is none), shared with third parties, or stored outside your browser.

### 1.2 Images
- **What:** Photos or screenshots you provide for workout analysis, including images captured via right-click on any web page.
- **How used:** Converted to Base64 and sent directly from your browser to the AI API you have selected (Gemini or Claude), solely for workout analysis.
- **Never:** Stored locally beyond the duration of the analysis, retained by GarminWO, or sent to any GarminWO server.
- **Third-party processing:** Images are processed by Google (Gemini) or Anthropic (Claude) according to their respective privacy policies.

### 1.3 Selected Text
- **What:** Text you select on any web page and send to GarminWO via the right-click context menu.
- **How used:** Sent directly to the selected AI API (Gemini or Claude) for workout plan analysis.
- **Never:** Stored, logged, or transmitted anywhere other than the AI API.

### 1.4 Garmin Connect Session
- **What:** GarminWO uses your existing Garmin Connect browser session (cookies) to authenticate API calls for importing and deleting workouts.
- **How used:** Cookies are read directly from the Garmin Connect page context to authenticate requests to the Garmin Connect API.
- **Never:** Cookies or credentials are stored by GarminWO or transmitted outside of Garmin Connect's own API endpoints.

---

## 2. Permissions Used

| Permission | Purpose |
|---|---|
| `storage` | Store your API key and engine preference locally |
| `contextMenus` | Add "Send to GarminWO" to the right-click menu on images and selected text |
| `tabs` | Detect open Garmin Connect tabs to activate them after a right-click action |
| `host_permissions: *://*/*` | Fetch images from any web page when using the right-click image feature |
| `host_permissions: connect.garmin.com` | Import and delete workouts via the Garmin Connect API |
| `host_permissions: api.anthropic.com` | Send images/text to Claude API (only if Claude engine selected) |
| `host_permissions: generativelanguage.googleapis.com` | Send images/text to Gemini API (only if Gemini engine selected) |

---

## 3. Third-Party Services

GarminWO integrates with the following third-party services. Your use of these services is governed by their own privacy policies:

- **Google Gemini API** — [https://policies.google.com/privacy](https://policies.google.com/privacy)
- **Anthropic Claude API** — [https://www.anthropic.com/privacy](https://www.anthropic.com/privacy)
- **Garmin Connect** — [https://www.garmin.com/en-US/privacy/connect/policy/](https://www.garmin.com/en-US/privacy/connect/policy/)

---

## 4. Data Retention

- **API keys:** Stored locally until you clear them manually or uninstall the extension.
- **Images and text:** Not stored. Processed in memory only, discarded immediately after analysis.
- **Pending image/text (right-click feature):** Stored temporarily in `chrome.storage.local` and deleted immediately after being retrieved by the content script (single use).

---

## 5. No Backend Server

GarminWO has no backend server, no database, no analytics, and no telemetry. The extension code runs entirely in your browser. The developer has no access to any data you process with GarminWO.

---

## 6. Advertising

GarminWO contains no advertising and no tracking of any kind.

---

## 7. Children's Privacy

GarminWO does not knowingly collect any information from children under 13. The extension is intended for use by adults managing their own fitness data.

---

## 8. Changes to This Policy

If this policy is updated, the "Last updated" date at the top of this document will be revised. Significant changes will be noted in the extension's changelog on GitHub.

---

## 9. Contact

If you have questions about this privacy policy, please open an issue on the GitHub repository.

---

## 10. Open Source

GarminWO is open source. You can review all extension code on GitHub to verify these claims independently.
