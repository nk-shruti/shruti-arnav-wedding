# Our Wedding To-Do 💍

A shared, real-time wedding task board for two people. Drag-and-drop Kanban
columns (Ideas → To Do → In Progress → Done), category tags, due dates, an
assignee for each task, a progress bar, and a countdown to the big day.

It works **immediately** in *local mode* (saves to your browser only). To make
edits sync live between you and your partner, do the 5-minute Firebase step below.

---

## Part A — Make it sync (Firebase, free, ~5 min, one time)

1. Go to **https://console.firebase.google.com** and sign in with any Google account.
2. Click **Add project** → give it a name (e.g. `our-wedding`) → you can **disable**
   Google Analytics → **Create project**.
3. In the left sidebar: **Build → Realtime Database** → **Create Database**.
   - Pick a location close to you.
   - Start in **test mode** for now → **Enable**. (We'll lock it down in step 6.)
4. Get your config: click the **gear icon (⚙️) → Project settings**. Scroll to
   **Your apps** → click the **web icon `</>`** → register an app (any nickname,
   you do NOT need Hosting). Firebase shows you a `firebaseConfig = { … }` object.
5. Copy that object and paste it into **`index.html`**, replacing the empty
   `firebaseConfig` near the top of the `<script>` (look for the comment
   *"paste your config object"*). Make sure the `databaseURL` line is present —
   if Firebase didn't include it, it looks like:
   `databaseURL: "https://YOUR-PROJECT-default-rtdb.firebaseio.com"`.
6. **(Recommended) Lock the database** so only people with your link can use it.
   In Realtime Database → **Rules** tab, paste the contents of
   `database.rules.json` from this repo → **Publish**. (Test mode auto-expires
   after 30 days, so this also keeps it working long-term.)

That's it — open `index.html` and the badge in the corner turns green: **Live sync**.
Both of you visiting the same URL now see each other's changes within a second.

> Privacy note: anyone who has both your site URL *and* could guess your Firebase
> project is unlikely, but this board is meant to be lightly private (a hard-to-guess
> link), not bank-grade secure. Don't put sensitive info (full card numbers, etc.) in it.

---

## Part B — Put it online so you can both open it (GitHub Pages, free)

If you want me (Claude) to do this for you, just say so — `gh` is already logged in.

Manual steps:

```bash
cd ~/wedding-todo
git init && git add -A && git commit -m "Wedding to-do board"
gh repo create our-wedding-todo --private --source=. --push
gh api -X POST repos/{owner}/our-wedding-todo/pages -f source.branch=main -f source.path=/
```

Then your site is at: `https://<your-username>.github.io/our-wedding-todo/`
(takes ~1 min to go live the first time). Share that link with your partner.

> Note: a **private** repo can still publish a **public** Pages site on the free
> plan in many cases; if Pages is blocked on private for your account, either make
> the repo public (the URL is unguessable-ish but technically discoverable) or
> deploy to Netlify/Vercel by dragging the folder in. Ask me and I'll handle it.

**Updating later:** whenever you change `index.html`, run
`git commit -am "update" && git push` and Pages redeploys automatically. Your
*tasks* don't live in GitHub though — they live in Firebase, so day-to-day edits
need no git at all.

---

## How to use the board

- **Add a task** — top button, or **＋ Add** at the bottom of any column.
- **Edit** — click a card. **Delete** — hover a card and click ✕.
- **Move** — drag a card between columns (also changes its status).
- **Assign** — set "Who's on it" to either of you / both.
- **Names & date** — click your names in the header to rename; set the date next
  to "The big day" to drive the countdown.
- **Filter** — by category or by who's responsible.

Everything saves automatically. In live mode it syncs to both of you.
