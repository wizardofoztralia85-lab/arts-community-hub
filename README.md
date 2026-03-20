# Art's Studio For Wizard's — Deployment Guide
### Glass Wizard Australia Pty Ltd · Sam & Shan Productions Inc.

---

## Your Project Files

| File | Purpose |
|------|---------|
| `index.html` | The entire app — edit this to make changes |
| `firebase.json` | Tells Firebase CLI how to deploy |
| `.firebaserc` | Links this folder to your Firebase project |
| `firestore.rules` | Firestore security rules — paste into Firebase Console |
| `README.md` | This guide |

---

## STEP 1 — Create Your Firebase Project

1. Go to **console.firebase.google.com**
2. Click **Add Project** → name it (e.g. `gwa-arts-studio`)
3. Enable Google Analytics: optional, but useful
4. Once created, go to **Build** in the left sidebar and enable:
   - **Authentication** → Sign-in method → **Anonymous** → Enable
   - **Firestore Database** → Create database → Start in **test mode** → choose a region (Australia: `australia-southeast1`)
   - **Hosting** → Get started (just click through the wizard for now)

---

## STEP 2 — Get Your Firebase Config

1. In Firebase Console → **Project Settings** (gear icon) → **Your Apps**
2. Click **Add App** → Web (`</>`)
3. Register the app (call it `Arts Studio`)
4. Copy the config object — it looks like:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

5. Open `index.html` in a text editor (Notepad, VS Code, etc.)
6. Find the section labelled `STEP 1 — PASTE YOUR FIREBASE CONFIG HERE`
7. Replace each `PASTE_YOUR_...` value with your actual values

Also update `.firebaserc` — replace `PASTE_YOUR_PROJECT_ID` with your actual project ID.

---

## STEP 3 — Get Your Gemini API Key

1. Go to **aistudio.google.com**
2. Click **Get API Key** → **Create API Key**
3. Copy the key
4. In `index.html`, find `STEP 3 — PASTE YOUR GEMINI API KEY HERE`
5. Replace `PASTE_YOUR_GEMINI_API_KEY_HERE` with your key

> ⚠️ Your API key will be visible in the page source. For a public site, this is low-risk for now. When traffic grows, ask a developer to proxy the call through a Firebase Cloud Function.

---

## STEP 4 — Set Firestore Security Rules

1. Firebase Console → **Firestore Database** → **Rules** tab
2. Delete the existing rules
3. Open `firestore.rules` from this folder and paste the entire contents
4. Click **Publish**

---

## STEP 5 — Deploy

You need Node.js installed. Download from **nodejs.org** if you don't have it.

Open a terminal (on Mac: Terminal app; on Windows: Command Prompt or PowerShell) in this folder and run:

```bash
# Install Firebase tools (first time only)
npm install -g firebase-tools

# Log in with your Google account
firebase login

# Deploy everything
firebase deploy
```

That's it. Firebase will give you a URL like:
`https://gwa-arts-studio.web.app`

---

## Making Updates

Whenever you change `index.html`, redeploy with:

```bash
firebase deploy
```

Takes about 30 seconds. The live site updates instantly.

---

## Connect a Custom Domain (Optional)

1. Firebase Console → **Hosting** → **Add custom domain**
2. Enter your domain (e.g. `artsstudio.glasswizard.com.au`)
3. Follow the DNS instructions — add the TXT and A records at your domain registrar
4. Firebase handles the SSL certificate automatically

Australian domain registrars: VentraIP, Crazy Domains, or Synergy Wholesale.

---

## Monitoring Checklist (Do Weekly)

- [ ] Firebase Console → **Firestore → Usage** — check read/write counts
- [ ] Firebase Console → **Authentication → Users** — see visitor numbers
- [ ] Firebase Console → **Hosting → Release history** — confirm latest deploy is live

## Set a Billing Budget Alert (Do Once)

1. Go to **console.cloud.google.com**
2. Billing → Budgets & Alerts → Create Budget
3. Set amount: **$10 AUD**
4. Add your email for alerts at 50%, 90%, 100%

Firebase free tier covers ~50,000 reads/day which is plenty for community scale.

---

## Backing Up Your Data (Do Monthly)

Firebase Console → **Firestore** → **Import/Export** → **Export** → choose a Cloud Storage bucket.
Or simply export from the console and download the JSON.

---

## Contact

Glass Wizard Australia Pty Ltd  
📧 wizardofoztralia85@gmail.com  
📞 0480 424 216
