# Setting Up Credentials for Vercel Deployment

## 1. Generate Secret Keys (Do This First)

Run this in PowerShell to generate random secure keys:

```powershell
# Generate FLASK_SECRET_KEY
$bytes = [System.Security.Cryptography.RandomNumberGenerator]::GetBytes(32)
$key1 = -join ($bytes | ForEach-Object { '{0:x2}' -f $_ })
Write-Host "FLASK_SECRET_KEY: $key1"

# Generate JWT_SECRET_KEY
$bytes = [System.Security.Cryptography.RandomNumberGenerator]::GetBytes(32)
$key2 = -join ($bytes | ForEach-Object { '{0:x2}' -f $_ })
Write-Host "JWT_SECRET_KEY: $key2"
```

**Save both keys somewhere safe!**

---

## 2. Create PostgreSQL Database

### Option A: Render.com (Recommended - Easy & Free)

1. Go to **https://render.com**
2. Click **"Sign Up"** (use GitHub for quick signup)
3. Click **"New +"** in top right
4. Select **"PostgreSQL"**
5. Fill in:
   - **Name**: `mood-detection-db`
   - **Database**: `mooddb`
   - **User**: `postgres`
   - **Region**: Choose closest to you
6. Click **"Create Database"**
7. Wait 2-3 minutes for creation
8. Scroll down to see **"Internal Database URL"** (this is your DATABASE_URL)

**Copy the full URL** - it looks like:
```
postgresql://username:password@dpg-xxxxx-xxxx.us-east-1.render.com:5432/dbname
```

---

### Option B: Supabase (Alternative - Also Free)

1. Go to **https://supabase.com**
2. Sign up with GitHub
3. Click **"Create new project"**
4. Fill in project name: `mood-detection`
5. Create secure password (save it!)
6. Click **"Create new project"**
7. Go to **Settings → Database** (left sidebar)
8. Copy the **"Connection string"** (PostgreSQL section)

---

### Option C: Railway.app (Another Alternative)

1. Go to **https://railway.app**
2. Click **"Start Project"** → Select **"PostgreSQL"**
3. Click **"Add Plugin"**
4. Go to **"Variables"** tab
5. Copy the **DATABASE_URL** value

---

## 3. Get Spotify API Credentials

1. Go to **https://developer.spotify.com/dashboard**
2. Click **"Sign Up"** or **"Log In"** (create Spotify account if needed - free)
3. Agree to terms
4. Click **"Create an App"**
5. Name: `Mood Detection App`
6. Accept terms and create
7. You'll see:
   - **Client ID** ← Copy this
   - **Client Secret** ← Click "Show" and copy this

**Save both!**

---

## 4. Environment Variables Summary

Once you have everything, your Vercel environment variables should be:

| Variable | Value | Where From |
|----------|-------|-----------|
| `DATABASE_URL` | `postgresql://user:pass@host:5432/db` | PostgreSQL provider (Step 2) |
| `FLASK_SECRET_KEY` | 64-character hex string | Generated (Step 1) |
| `JWT_SECRET_KEY` | 64-character hex string | Generated (Step 1) |
| `SPOTIFY_CLIENT_ID` | Your client ID | Spotify Dashboard |
| `SPOTIFY_CLIENT_SECRET` | Your client secret | Spotify Dashboard |
| `FLASK_ENV` | `production` | Hardcoded |

---

## 5. Add to Vercel

1. Go to **https://vercel.com/dashboard**
2. Click on your deployed project
3. Go to **Settings → Environment Variables**
4. Click **"Add New"** for each variable above
5. Paste the values
6. Click **"Save"**
7. Vercel will automatically redeploy with the new variables ✅

---

## Quick Checklist

- [ ] Generate FLASK_SECRET_KEY
- [ ] Generate JWT_SECRET_KEY
- [ ] Create PostgreSQL database
- [ ] Copy DATABASE_URL
- [ ] Create Spotify app
- [ ] Copy SPOTIFY_CLIENT_ID
- [ ] Copy SPOTIFY_CLIENT_SECRET
- [ ] Add all 6 variables to Vercel
- [ ] Verify deployment succeeds

---

## Need Help?

- **PostgreSQL URL format wrong?** → Make sure it starts with `postgresql://` (not `postgres://`)
- **Spotify auth failing?** → Check your Client ID/Secret are correct (don't share them!)
- **Still asking for credentials on deploy?** → Make sure app is in production mode in `.env`
