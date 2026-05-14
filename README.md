# ⚔️ Campaign Calendar

A GitHub-hosted fantasy calendar for tabletop RPG campaigns. Players can view the calendar, log past events, mark future plans, and calculate time passage — all saved live to the repo via GitHub's API.

---

## 📁 File Structure

```
/
├── index.html        ← Player-facing calendar (share this URL)
├── admin.html        ← DM config editor (keep this URL private)
└── data/
    ├── config.json   ← Calendar structure & current campaign date
    └── events.json   ← All campaign events
```

---

## 🚀 Setup Guide

### 1. Create the GitHub Repository

1. Go to [github.com/new](https://github.com/new)
2. Name it (e.g. `campaign-calendar`)
3. Set to **Public** (required for GitHub Pages on free accounts)
4. Create the repo

### 2. Upload the Files

Upload all four files maintaining the folder structure:
- `index.html` → root
- `admin.html` → root
- `data/config.json` → `data/` folder
- `data/events.json` → `data/` folder

You can drag-and-drop in the GitHub web UI, use the GitHub CLI, or push via Git.

### 3. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Under *Source*, select **Deploy from a branch**
3. Choose **main** branch, **/ (root)** folder
4. Click **Save**
5. Your site will be live at:
   `https://YOUR-USERNAME.github.io/campaign-calendar/`

It may take 1–2 minutes to deploy the first time.

### 4. Create a Personal Access Token (PAT)

This allows the calendar to save changes back to the repo.

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Give it a name like `Campaign Calendar`
4. Set expiration as needed (or "No expiration" for convenience)
5. Under *Scopes*, check **`repo`** (full repository access)
6. Click **Generate token** and copy it immediately

> **Share this PAT with your players** if you want them to be able to save events. Each player can also create their own PAT — they just need `repo` scope on the same repository (they'll need write access to your repo, so add them as collaborators under Settings → Collaborators).

### 5. Configure the Calendar

1. Open `https://YOUR-USERNAME.github.io/campaign-calendar/admin.html`
2. Click **GitHub Settings** in the top right
3. Enter your PAT, repo owner (your GitHub username), repo name, and branch (`main`)
4. Click **Save** — it will load your config
5. Fill in your campaign name, month names, week names, and current date
6. Click **Save All Changes**

### 6. Share with Players

Give players the URL to `index.html`. On first load, they'll see a Settings prompt where they enter:
- **PAT** — their own, or the shared one you created
- **Repo owner** — your GitHub username
- **Repo name** — e.g. `campaign-calendar`
- **Branch** — `main`

These are stored only in their browser's localStorage.

---

## 🗓 Calendar Features

### Player View (`index.html`)
- **Monthly calendar grid** — Navigate between months and years with arrow buttons
- **Current Campaign Time** — Always-visible sidebar showing the current in-world date and time
- **Click any day** — See all events on that day; add new ones
- **Event types:**
  - 🔴 **Past** — Things that already happened
  - 🔵 **Future** — Planned events or deadlines
  - 🟣 **Note** — Lore notes, reminders, observations
  - 🟡 **Milestone** — Major story moments (appears in both Recent & Upcoming sidebars)
- **Time Passage calculator** — Enter years/months/weeks/days/hours/minutes → see the resulting date; "Advance Time" commits it to the repo

### DM Admin (`admin.html`)
- Set the calendar name, all structural values (months/year, weeks/month, days/week, hours/day)
- Name every month, every week, and optionally every day
- Set the current campaign date and time
- All saved directly to `data/config.json` in the repo

---

## ⚙️ Customization

### Changing Calendar Structure

The calendar is fully configurable. In `admin.html` you can change:

| Setting | Default | Notes |
|---|---|---|
| Months per year | 8 | Any positive integer |
| Weeks per month | 5 | Any positive integer |
| Days per week | 10 | Any positive integer |
| Hours per day | 24 | Any positive integer |

After changing structure values, the name input grids regenerate automatically. Enter your names and save.

### Adding Day Names

By default, days within a week are labeled "Day 1" through "Day N". In `admin.html`, you can fill in names for each day. Leave fields blank to keep the default numbering. You can name some days and leave others blank — blank days fall back to "Day N".

---

## 🔐 Security Notes

- **PATs are stored in `localStorage`** in each player's browser — they never touch your server
- **`admin.html` is not linked** from `index.html` — keep its URL private
- For extra security, you can rename `admin.html` to something obscure
- Consider setting PAT expiration dates and rotating them seasonally
- If a player should lose access, remove them as a collaborator and rotate the PAT

---

## 🐛 Troubleshooting

**"GitHub 401" error when saving**
→ Your PAT has expired or lacks `repo` scope. Generate a new one.

**"GitHub 409" error**
→ A SHA conflict — the file was updated by someone else. Click "↺ Reload" in admin, or refresh the player page, then try again.

**Calendar shows defaults instead of my names**
→ Check that `data/config.json` exists in your repo and is valid JSON. Open it in GitHub and verify.

**Changes not appearing after save**
→ GitHub Pages can take 30–60 seconds to rebuild. Hard-refresh the page (Ctrl+Shift+R).

**Players can view but not save**
→ They need to be added as collaborators in your repo's Settings → Collaborators, AND have a PAT with `repo` scope.
