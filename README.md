# Orbitly
 
**Bring your tasks and notes into orbit.**
 
Orbitly is a small, single-file web app for planning your day. Track tasks by date and status, tag them with flags, and keep titled notes alongside them. Everything is saved locally in your browser, with no backend or account.
 
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
Orbitly uses **IndexedDB** (database `daily-tasks`, stores `tasks` and `notes`). Data is saved per browser and per site address.
 
- Data does not sync across devices or browsers.
- Clearing site data in your browser deletes your tasks and notes.
- Moving the app to a different URL starts with empty data.
If IndexedDB is unavailable (for example in some private modes), the app still works for the session and shows a notice that data won't persist.
 
## Tech
- Plain HTML, CSS and JavaScript in one file (`index.html`).
- No build step and no dependencies.
- Manrope from Google Fonts, with a system font fallback.
## Run locally
Open `index.html` in a browser. No server is needed.
 
## Deploy to GitHub Pages
1. Create a public repository, for example `orbitly`.
2. Add `index.html` (and this README) to the repository root.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, and save.
5. Your site will be live at `https://<your-username>.github.io/orbitly/`.
Other static hosts work too: Netlify Drop, Cloudflare Pages and Vercel.
 
## Project structure
```
orbitly/
├── index.html   # the entire app
└── README.md
```
 
## Customizing
- **Flags:** edit the `FLAGS` array near the top of the script in `index.html`, and the `--f-*` colour variables in the CSS.
- **Accent colour:** change the `--green` variable (default `#27A33E`).
 
