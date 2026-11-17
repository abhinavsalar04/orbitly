# Orbitly
 
**Bring your tasks and notes into orbit.**
 
Orbitly is a small web app for planning your day. Track tasks by date and status, tag them with flags, and keep titled notes alongside them. Sign in with an email account and the same lists stay in sync on your phone and computer.
 
## Features
 
### Tasks
- Date-wise tasks: browse days with the previous/next arrows, the date picker, or **Today**.
- Three columns per day: **To do**, **Pending**, **Completed**.
- Flags: Backend, Frontend, Swag store, Certificate, hello.h2s, with a filter bar to view one flag at a time.
- Multi-line task text with bullets and numbering (`- ` or `1. ` at the start of a line; Enter continues the list).
- Icon buttons on each card, with a title on hover: mark pending, mark completed, move to To do, move to today, edit, delete.
- **Move to today** appears on tasks from other days, so unfinished work is easy to carry over.
- Clear all completed tasks for a day.
### Notes
- Notes with a title and body, with the same bullet and numbering support.
- Search notes by title or content.
- Inline edit and delete, with the last-edited date on each note.
### General
- Switch between **Tasks** and **Notes** with the tabs at the top.
- Light and dark mode follow your system setting.
- Responsive layout for desktop and mobile.
## Keyboard shortcuts
| Shortcut | Action |
| --- | --- |
| Enter | New line (continues a bullet or numbered list) |
| Enter on an empty list item | Ends the list |
| Ctrl/Cmd + Enter | Add or save the task or note |
 
## Data storage
Tasks and notes live in **Cloud Firestore**, one set per signed-in account:

- `users/{uid}/tasks/{id}`
- `users/{uid}/notes/{id}`

Devices signed in with the same email share that list. Firestore keeps a local cache, so the last data still shows while offline and uploads when the connection returns.

The first time an account signs in on a browser that still has the old IndexedDB database (`daily-tasks`) and the cloud lists are empty, those local tasks and notes are uploaded once. Later sign-ins do not upload them again.

## Firebase setup
The page does not ship with a project of its own. Create one on the free Spark plan, then paste the web config into `firebase-config.js`.

1. In the [Firebase console](https://console.firebase.google.com/), create a project and add a Web app.
2. Enable **Authentication → Email/Password** and **Google**.
3. Under **Authentication → Settings → Authorized domains**, add `orbitly.bytemelabs.in` and `localhost`.
4. Create a **Cloud Firestore** database.
5. Paste these rules so each person can only read and write their own tasks and notes:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{collection}/{docId} {
      allow read, write: if request.auth != null && request.auth.uid == uid
        && collection in ['tasks', 'notes'];
    }
  }
}
```

6. Copy the web app config into `firebase-config.js` (`apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`).

The web API key is public. The rules above are what keep accounts private.

## Tech
- Plain HTML, CSS and JavaScript in `index.html`.
- Firebase Authentication and Cloud Firestore, loaded from the Firebase compat CDN.
- No build step.
- Manrope from Google Fonts, with a system font fallback.
## Run locally
Serve the folder over HTTP (Firebase Auth does not run from a `file://` address). For example:

```
python3 -m http.server 8765
```

Then open `http://localhost:8765/`. `localhost` must be an authorized domain in the Firebase project.
 
## Deploy to GitHub Pages
1. Create a public repository, for example `orbitly`.
2. Add `index.html`, `firebase-config.js` (and this README) to the repository root.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, and save.
5. Your site will be live at `https://<your-username>.github.io/orbitly/`.
Other static hosts work too: Netlify Drop, Cloudflare Pages and Vercel.
 
## Project structure
```
orbitly/
├── index.html           # the app
├── firebase-config.js   # Firebase web config (paste yours here)
├── CNAME
└── README.md
```
 
## Customizing
- **Flags:** edit the `FLAGS` array near the top of the script in `index.html`, and the `--f-*` colour variables in the CSS.
- **Accent colour:** change the `--green` variable (default `#27A33E`).
 
