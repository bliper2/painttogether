# 🎨 PaintTogether — Setup Guide

A real-time multiplayer painting canvas.  
Everyone who visits the page **shares the same canvas and sees each other paint live.**

---

## Step 1 — Create a Firebase Project (free)

1. Go to **https://console.firebase.google.com**
2. Click **"Add project"** → give it a name (e.g. `painttogether`) → Create
3. In the left sidebar → **Build → Realtime Database**
4. Click **"Create Database"**
5. Choose any location → Select **"Start in test mode"** → Enable
6. Go to **Project Settings** (gear icon top-left) → **"Your apps"** section
7. Click the **`</>`** (web) icon → Register app → copy the `firebaseConfig` object

---

## Step 2 — Paste Config into index.html

Open `index.html` and find this block near the bottom:

```js
const FIREBASE_CONFIG = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT.firebaseapp.com",
  databaseURL:       "https://YOUR_PROJECT-default-rtdb.firebaseio.com",
  ...
};
```

Replace **all the placeholder values** with your actual Firebase config.

Example of what it looks like after:
```js
const FIREBASE_CONFIG = {
  apiKey:            "AIzaSyAbc123...",
  authDomain:        "painttogether-abc.firebaseapp.com",
  databaseURL:       "https://painttogether-abc-default-rtdb.firebaseio.com",
  projectId:         "painttogether-abc",
  storageBucket:     "painttogether-abc.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc123"
};
```

---

## Step 3 — Deploy to Netlify (free)

### Option A — Drag and Drop (easiest)
1. Go to **https://app.netlify.com**
2. Sign up / log in
3. Drag the **`painttogether` folder** onto the Netlify dashboard
4. Done! Your site is live at a `.netlify.app` URL

### Option B — Netlify CLI
```bash
npm install -g netlify-cli
cd painttogether
netlify deploy --prod --dir .
```

---

## Firebase Security Rules (recommended)

After testing, go to Firebase → Realtime Database → Rules and set:

```json
{
  "rules": {
    "strokes": {
      ".read":  true,
      ".write": true
    },
    "users": {
      ".read":  true,
      ".write": true
    },
    "cursors": {
      ".read":  true,
      ".write": true
    },
    "clearEvent": {
      ".read":  true,
      ".write": true
    }
  }
}
```

---

## Controls

| Action         | Shortcut        |
|----------------|-----------------|
| Pen tool       | `P`             |
| Eraser tool    | `E`             |
| Brush smaller  | `[`             |
| Brush bigger   | `]`             |
| Save as PNG    | Right panel button |
| Clear canvas   | Right panel button (clears for everyone) |

---

## How it works

- Strokes are pushed to **Firebase Realtime Database** as you draw
- All connected clients receive new strokes instantly via WebSocket
- Remote cursors show where other painters are moving
- Online users list updates automatically when people join/leave
- Canvas persists between sessions (clears only when someone presses Clear)

---

## Files

```
painttogether/
  index.html    ← The entire app (single file, deploy as-is)
  README.md     ← This file
```
