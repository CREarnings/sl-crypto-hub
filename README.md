# CR Earnings – Crypto Airdrop Hub 🇱🇰

Sri Lanka's #1 crypto airdrop tracking site. Built with pure HTML/CSS/JS — no server, no backend, hosted free on GitHub Pages. Uses a **GitHub Gist as a database** so all visitors worldwide see the same articles in real time.

---

## 🗂️ Files

```
cr-earnings/
├── assets/           # Site logo - visitors see favicon from here
|   └── icon.ico      # Site icon
├── index.html        # Public site – visitors see articles here
├── admin.html        # Admin panel – only for authorized admins
├── site-config.json  # Auto-generated on setup – stores Gist ID (DO NOT edit manually)
└── README.md
```

---

## 🚀 First Time Setup

### Step 1 – Create a GitHub Gist (the database)

1. Go to [gist.github.com](https://gist.github.com)
2. Create a **New secret gist**
3. Filename: `cr-data.json` — Content: `{}`
4. Click **Create secret gist**
5. Copy the **Gist ID** from the URL — it's the long alphanumeric code after your username:
   ```
   https://gist.github.com/yourusername/THIS-IS-THE-GIST-ID
   ```

### Step 2 – Create a GitHub Personal Access Token

1. Go to [GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Give it a name (e.g. `cr-earnings`)
4. Check these two scopes: ✅ **gist** and ✅ **repo**
5. Click **Generate token** and copy it — you won't see it again!

### Step 3 – Run Setup

1. Push all files to your GitHub repo and enable GitHub Pages
2. Open `admin.html` in your browser
3. Fill in the setup form:
   - **GitHub Gist ID** – from Step 1
   - **GitHub Personal Access Token** – from Step 2
   - **Your GitHub Username** – e.g. `johndoe`
   - **Your Repo Name** – e.g. `cr-earnings`
   - **Admin Username** – your superadmin login name
   - **Admin Password** – choose a strong password
4. Click **Complete Setup**

> ✅ Setup automatically writes `site-config.json` to your repo so every visitor can find the database — no extra steps needed.

---

## 🔐 Admin Panel

Access the admin panel at `/admin.html`. It is **not linked anywhere on the public site** — only people who know the URL can access it.

### Logging in from the same device (after setup)
Just go to `admin.html` and log in with your username and password.

### Logging in from a new device
1. Go to `admin.html`
2. Click **"New device? Enter token"** below the login button
3. Enter your GitHub token along with your username and password
4. Your token is saved locally on that browser — you only need to do this once per device

### Admin roles

| Role | Can Do |
|------|--------|
| **Super Admin** | Add/edit/delete articles, ads, and other admins |
| **Admin** | Add/edit/delete articles and ads only |

> Only the **Super Admin** can add or remove other admins. Regular admins cannot access the Admins tab.

---

## 📰 Managing Articles (Airdrops)

From the admin panel → **Articles** tab:

- **Add Airdrop** – fill in title, description, cover image URL, optional YouTube video, and status
- **Edit** – update any existing article
- **Del** – permanently delete an article
- **Status options:**
  - `Published` — visible to all visitors immediately
  - `Draft` — hidden from public, only visible in admin panel
  - `Scheduled` — auto-publishes at a set date and time

All changes sync to the Gist database instantly and appear on the public site for all visitors.

---

## 📢 Managing Ads

From the admin panel → **Ads** tab:

- **Left Sidebar** – rotates every 10 seconds, recommended size 140×300px
- **Right Sidebar** – same as left
- **Bottom Bar** – fixed bar at the bottom, max 4 ads, recommended size 50×50px

Each ad has a title, subtitle, image URL, and link URL.

---

## ⚙️ Settings

From the admin panel → **Settings** tab, any admin can change their own username and password. Current password is required to confirm changes.

---

## 🌐 How the Public Site Works

```
Visitor opens index.html
       ↓
Fetches site-config.json from the repo (contains Gist ID)
       ↓
Fetches cr-data.json from GitHub Gist API (public read, no token needed)
       ↓
Renders all published articles as cards
```

The public site auto-refreshes every 5 minutes so scheduled articles appear on time.

---

## 🛠️ Tech Stack

- **Frontend:** Pure HTML, CSS, JavaScript (no frameworks)
- **Styling:** Tailwind CSS (CDN) + custom CSS variables
- **Fonts:** Orbitron + Exo 2 (Google Fonts)
- **Database:** GitHub Gist (free, no server needed)
- **Config:** `site-config.json` in the repo (auto-written on setup)
- **Hosting:** GitHub Pages (free)

---

## 🔄 How Data Syncs to All Visitors

The key file is `site-config.json` — it's written to the repo during setup and contains just:

```json
{ "gistId": "your-gist-id-here" }
```

Every browser fetches this file to discover the Gist ID, then reads the Gist directly. Since the Gist is public-readable, **any visitor on any device worldwide** sees the same data without needing any account or login.

The GitHub token is **only stored locally** on the admin's browser — it is never exposed to visitors or stored in the repo.

---

## ❓ Troubleshooting

**Articles not showing on the public site**
- Make sure setup completed successfully and `site-config.json` exists in your repo
- Check that your GitHub token had both `gist` and `repo` scopes during setup
- Wait 1–2 minutes after setup for GitHub Pages to update

**"Cannot reach database" on login**
- Your Gist ID is correct but the Gist file (`cr-data.json`) may have been deleted — create a new Gist and re-run setup
- Check your internet connection

**Admin from another device can't write articles**
- They need to enter the GitHub token when logging in — click "New device? Enter token" on the login screen

**Setup says "This Gist already has admins"**
- The Gist is already configured. Go to the login screen instead of running setup again.

---

## 📄 License

MIT — free to use and modify.
