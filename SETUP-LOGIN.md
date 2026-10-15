# Turn on sign-in (about 10 minutes, free)

The site has a built-in email-and-password sign-in. Sign in with the same email on any phone and your progress follows you. It uses Google's free Firebase service to store the accounts and progress. You set it up once; nobody needs a credit card.

Until you do this, the site works exactly as before and saves progress on each phone only.

## 1. Create the Firebase project

1. Open **console.firebase.google.com** and sign in with any Google account.
2. Tap **Create a project** (or *Add project*). Name it, for example, `midterm-mastery`. You can switch Google Analytics **off**. Finish creating it.

## 2. Switch on email sign-in

1. In the left menu: **Build → Authentication → Get started**.
2. Open the **Sign-in method** tab, choose **Email/Password**, switch on the first toggle, and **Save**.

## 3. Create the database

1. Left menu: **Build → Firestore Database → Create database**.
2. Pick any location near you, choose **Start in production mode**, then **Create**.
3. Open the **Rules** tab, replace everything with the rules below, and tap **Publish**. These rules let each person read and write only their own progress.

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

## 4. Get your web config

1. Tap the **gear icon → Project settings**.
2. Under **Your apps**, tap the **web icon `</>`**, give it a nickname, and tap **Register app** (skip Firebase Hosting).
3. Firebase shows a block like `const firebaseConfig = { apiKey: "…", authDomain: "…", projectId: "…", … };`. Copy the part from `{` to `}`.

## 5. Put it in your site

1. In your GitHub repo, open **firebase-config.js** and tap the **pencil (edit)** icon.
2. Replace `null` with what you copied, so it looks like:

```js
window.FIREBASE_CONFIG = {
  apiKey: "AIza…",
  authDomain: "midterm-mastery.firebaseapp.com",
  projectId: "midterm-mastery",
  storageBucket: "midterm-mastery.appspot.com",
  messagingSenderId: "123…",
  appId: "1:123…:web:abc…"
};
```

3. **Commit changes**, wait 1–2 minutes, and reload the site. A **Sign in to sync your progress** card appears near the top of the dashboard.

This config is meant to be public; it is not a password. Your data is protected by the rules from step 3.

## Using it

- First time: tap **Create account**, enter your email and a password (6+ characters). Progress already on that phone is uploaded.
- On another phone: open the site, tap **Sign in** with the same email and password. Answers from both phones are combined; for any question answered on both, the most recent answer wins.
- Progress uploads a couple of seconds after each answer, and the site checks for updates whenever you come back to the tab.
- **Forgot password?** sends a reset link to your email (check spam).
- **Sign out** keeps the progress on that phone but stops syncing.
- **Reset progress** while signed in clears it on every phone that syncs with that account.

## If something goes wrong

| Message | Fix |
|---|---|
| "Email sign-in is not switched on in the Firebase project yet." | Redo step 2. |
| "Sync blocked: check the Firestore rules" | Redo step 3 and make sure you tapped **Publish**. |
| No sign-in card appears | Check that `firebase-config.js` was saved with your config (not `null`), then reload. Make sure the file is in the same folder as `index.html`. |
| "Sign-in could not load" | The phone is offline, or a content blocker is blocking `gstatic.com`. |
