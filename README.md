# Kharcha – Expense Tracker PWA
## Setup Instructions

---

## Files in This Package
- `index.html` — Main app (all CSS + JS included)
- `manifest.json` — PWA metadata
- `sw.js` — Service Worker for offline support
- `icon-192.png` / `icon-512.png` — You need to add app icons (see below)

---

## Step 1: Add Your Firebase Config

Open `index.html` and find this section near the bottom (around line 380):

```js
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT.firebaseapp.com",
  projectId:         "YOUR_PROJECT_ID",
  storageBucket:     "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId:             "YOUR_APP_ID"
};
```

Replace with your actual Firebase project values from:
**Firebase Console → Project Settings → Your Apps → Web App → SDK setup**

---

## Step 2: Firestore Setup

In Firebase Console → Firestore Database:

1. Create a database (Start in **production mode**)
2. Add this security rule (allows authenticated users):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /expenses/{doc} {
      allow read, write: if request.auth != null;
    }
  }
}
```

---

## Step 3: Add App Icons

Create or use any image and save as:
- `icon-192.png` (192×192 px)
- `icon-512.png` (512×512 px)

Place them in the same folder as `index.html`.

You can generate icons at: https://realfavicongenerator.net

---

## Step 4: Deploy

Host all files on any static hosting:

### Option A – Firebase Hosting (Recommended)
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### Option B – Netlify
Drag and drop the folder at https://app.netlify.com

### Option C – Vercel
```bash
npx vercel
```

> ⚠️ Service Workers require HTTPS. The app must be served over HTTPS to work as a PWA (Firebase Hosting, Netlify, Vercel all provide this automatically).

---

## Profile Passwords (already configured in app)

| Profile    | Password        | Access         |
|------------|-----------------|----------------|
| Kabir      | @9172481808Kk   | Full Admin     |
| View-User  | 1234567         | Read Only      |

Both profiles use the **same Firebase email/password** to sign in, then a separate profile password to choose the access level.

---

## Features

- ✅ Firebase Authentication
- ✅ Real-time Firestore sync
- ✅ Admin: Add, Edit, Delete expenses
- ✅ Viewer: Read-only access
- ✅ Monthly view with navigation
- ✅ Category breakdown chart
- ✅ Search & filter
- ✅ PWA installable on phone
- ✅ Offline support via Service Worker
- ✅ 9 expense categories
- ✅ Indian Rupee (₹) formatting
