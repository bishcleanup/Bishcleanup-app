# Bish Cleanup app

Property upkeep and handyman services for Lewis, Cowlitz, Clark and Thurston counties.

`public/index.html` is a single-file web app with admin, team and customer logins, quote and booking requests, a daily team schedule, a time clock with payroll CSV export, alerts and messaging.

## Where it runs

The app runs on Firebase:

- **Firebase Authentication** (email and password) holds logins and passwords.
- **Cloud Firestore** holds the data. `firestore.rules` enforces who can read and change what (admin, team, customer).
- **Firebase Hosting** serves `public/`. On Hosting the page loads its Firebase config from `/__/firebase/init.json`, so no keys are in the code. To host it somewhere else, paste your web app config into `FIREBASE_CONFIG` near the bottom of `public/index.html`.

## Live site

https://bish-cleanup.web.app (Firebase project `bish-cleanup`). To redeploy after changes:

```bash
firebase deploy --only firestore,hosting
```

## First deploy (new project)

1. In the [Firebase console](https://console.firebase.google.com), create a project, add a **Web app**, turn on **Authentication → Sign-in method → Email/Password**, and create a **Firestore database** (production mode).
2. Install the CLI and deploy from this folder:

   ```bash
   npm install -g firebase-tools
   ```

   ```bash
   firebase login
   ```

   ```bash
   firebase use --add
   ```

   ```bash
   firebase deploy --only firestore,hosting
   ```

3. Open the Hosting address right away and create the admin account. **The first person to open a fresh deployment gets the setup form**, and setup closes for good once the admin exists.

## Local testing

```bash
firebase emulators:start --project demo-bish
```

Then open http://localhost:5000. A `demo-*` project on localhost uses the Auth and Firestore emulators.

## Notes

- Account records are stored at `accounts/{email}`. Changing a user's sign-in email isn't supported.
- Signup links (`#join-…`) work until the admin deletes them. Anyone with a link can join with the Team role.
- Reminders and alerts only fire while someone has the app open. Push notifications or SMS when the app is closed need Cloud Functions.
- Data from the old claude.ai artifact version isn't copied over. The new deployment starts empty.
