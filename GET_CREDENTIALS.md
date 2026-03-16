# GENERATE YOUR CREDENTIALS HERE

## Step 1: Generate Secret Keys

Since PowerShell generation had issues, use one of these methods:

### Method 1: Online (Quickest)
Go to: https://randomkeygen.com/
- Copy the entire "Fort Knox Passwords" value (64 chars)
- Use this for FLASK_SECRET_KEY
- Generate another one for JWT_SECRET_KEY

### Method 2: Windows Command (copy-paste this)
Open Command Prompt (not PowerShell) and run:
```
certutil -genkey -exportable 32 temp.key >nul && certutil -dump temp.key | find "Public Key" && del temp.key
```

### Method 3: Use an online UUID/random generator
Visit: https://www.uuidgenerator.net/
And generate a UUID v4, repeat 2-3 times and concatenate them

---

## Your Template

Copy this and fill in your values:

```json
{
  "DATABASE_URL": "postgresql://YOUR_USER:YOUR_PASSWORD@YOUR_HOST:5432/YOUR_DB",
  "FLASK_SECRET_KEY": "YOUR_64_CHAR_HEX_STRING_HERE",
  "JWT_SECRET_KEY": "YOUR_64_CHAR_HEX_STRING_HERE",
  "SPOTIFY_CLIENT_ID": "YOUR_SPOTIFY_CLIENT_ID_HERE",
  "SPOTIFY_CLIENT_SECRET": "YOUR_SPOTIFY_CLIENT_SECRET_HERE",
  "FLASK_ENV": "production"
}
```

---

## Getting Each Credential:

### 1. DATABASE_URL
- Sign up: https://render.com (FREE tier)
- Create PostgreSQL database
- Copy "Internal Database URL" from the dashboard
- Format: `postgresql://user:password@dpg-xxxxx.render.com:5432/dbname`

### 2. FLASK_SECRET_KEY & JWT_SECRET_KEY
- Go to: https://randomkeygen.com/
- Copy "Fort Knox Passwords" (64 chars)
- Generate 2 different ones

### 3. SPOTIFY_CLIENT_ID & SPOTIFY_CLIENT_SECRET
- Go to: https://developer.spotify.com/dashboard
- Login/signup (FREE)
- Create App
- Copy "Client ID"
- Click "Show Client Secret" to see it
- Copy both values

---

## Save Your Credentials (NEVER SHARE THESE!)

Create a `.env.vercel` file locally (for reference only):
```
DATABASE_URL=postgresql://your_actual_user:your_actual_pass@host:5432/mooddb
FLASK_SECRET_KEY=abc123def456...
JWT_SECRET_KEY=xyz789abc123...
SPOTIFY_CLIENT_ID=1a2b3c4d5e6f...
SPOTIFY_CLIENT_SECRET=secret_key_here...
FLASK_ENV=production
```

**DO NOT COMMIT THIS FILE TO GITHUB!** It's only for your reference.

---

## Add to Vercel in 3 Steps:

1. Go to: https://vercel.com/dashboard
2. Select your project
3. Click Settings → Environment Variables
4. Add each variable one by one
5. Click Redeploy

✅ Your app will automatically redeploy with the credentials!

---

## Verification

Once deployed:
1. Visit your Vercel app URL
2. Try logging in
3. Check if database is working
4. Test Spotify integration

If it fails, check Vercel logs in the dashboard.
