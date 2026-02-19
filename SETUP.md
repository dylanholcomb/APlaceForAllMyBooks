# Setup Guide — A Place for All My Books Scorecard

Two files: `scorecard.html` (one per player) and `leaderboard.html` (shared view).
Both need Firebase configured and then deployed to GitHub Pages.

---

## Step 1 — Firebase (5 minutes)

1. Go to **console.firebase.google.com** and sign in with a Google account
2. Click **Add project** → name it (e.g. `apfamb-scorecard`) → Create
3. In the left sidebar click **Build → Realtime Database**
4. Click **Create Database** → choose a region → start in **test mode** → Enable
5. In the left sidebar click the **⚙️ gear icon → Project settings**
6. Scroll to **Your apps** → click the **`</>`** (web) icon → register the app
7. Copy the `firebaseConfig` object that appears — it looks like:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "apfamb-scorecard.firebaseapp.com",
  databaseURL: "https://apfamb-scorecard-default-rtdb.firebaseio.com",
  projectId: "apfamb-scorecard",
  storageBucket: "apfamb-scorecard.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

8. Paste those values into the `FIREBASE_CONFIG` block near the bottom of **both**
   `scorecard.html` and `leaderboard.html` — replace the `PASTE_YOUR_...` placeholders.

### Security Rules (optional but recommended)

In the Firebase console → Realtime Database → Rules tab, paste:

```json
{
  "rules": {
    "games": {
      "$roomCode": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

This keeps it open (fine for a friend group). You can tighten later.

---

## Step 2 — GitHub Pages (3 minutes)

1. Go to **github.com** → sign in → click **New repository**
2. Name it `apfamb-scorecard` → Public → Create repository
3. Upload both files: `scorecard.html` and `leaderboard.html`
   (drag & drop onto the repo page, or use the "Add file" button)
4. Go to **Settings → Pages**
5. Under "Branch" select `main` → `/ (root)` → Save
6. After ~60 seconds your site is live at:
   `https://YOUR-USERNAME.github.io/apfamb-scorecard/scorecard.html`

Share that URL with players before a game session!

---

## How It Works In Play

1. **One player** opens `scorecard.html`, taps **Generate Room Code** → gets e.g. `KFP-283`
2. They share that code with everyone (read it aloud or text it)
3. **Other players** open `scorecard.html` on their own phones, tap **Join** and enter the code
4. Everyone scores normally on their own phone — syncs automatically
5. Any player can tap **🏅 Standings** to open `leaderboard.html` with the room pre-filled
6. The leaderboard updates live as scores change

---

## Updating Files Later

Just re-upload the updated HTML files to your GitHub repo — Pages deploys automatically within ~60 seconds.
