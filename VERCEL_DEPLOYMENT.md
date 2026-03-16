# Vercel Deployment Guide for Mood Detection App

## Prerequisites
- GitHub account (to push your code)
- PostgreSQL database (recommended: Render.com free tier)
- Vercel account (free tier available)
- Spotify API credentials

## Step-by-Step Deployment

### 1. Push Code to GitHub
```bash
git init
git add .
git commit -m "Initial commit for Vercel deployment"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/mood-detection-app.git
git push -u origin main
```

### 2. Set Up PostgreSQL Database

**Option A: Using Render.com (Free)**
- Go to https://render.com
- Create a new PostgreSQL database (free tier)
- Copy the PostgreSQL connection string

**Option B: Using AWS RDS, Supabase, or other providers**

### 3. Create Vercel Project
- Go to https://vercel.com/new
- Import your GitHub repository
- Click "Deploy"

### 4. Configure Environment Variables in Vercel

After importing the repo, click on "Settings" → "Environment Variables" and add:

| Variable | Value |
|----------|-------|
| FLASK_SECRET_KEY | Generate a random hex string (32+ chars) |
| JWT_SECRET_KEY | Generate a random hex string (32+ chars) |
| DATABASE_URL | PostgreSQL connection URL from Step 2 |
| SPOTIFY_CLIENT_ID | Your Spotify API client ID |
| SPOTIFY_CLIENT_SECRET | Your Spotify API client secret |
| FLASK_ENV | production |

**To generate secret keys in PowerShell:**
```powershell
[System.Security.Cryptography.RandomNumberGenerator]::GetBytes(32) | ForEach-Object { '{0:x2}' -f $_ }
```

### 5. Deploy
Vercel will automatically deploy when you push to GitHub. Monitor deployment in the Vercel dashboard.

## Important Notes

- **First deployment may take 2-3 minutes** due to dependencies
- **Email verification in Spotify**: Make sure your Spotify app is not in "development mode"
- **Database needs migration**: Run `flask db upgrade` if using Flask-Migrate
- **Static files**: Already configured in the project
- **Cold starts**: Serverless functions may have ~5-10s cold start times initially

## Troubleshooting

### Build fails with TensorFlow error
- We've switched to `tensorflow-lite-runtime` which is much lighter
- Check logs in Vercel dashboard

### Database connection errors
- Verify DATABASE_URL format: `postgresql://user:password@host:port/dbname`
- Ensure database allows connections from Vercel IPs (typically allow all)

### Model file not found
- Ensure `emotion_model.tflite` is committed to GitHub (not in .gitignore)

### Spotify authentication fails
- Verify SPOTIFY_CLIENT_ID and SPOTIFY_CLIENT_SECRET are set
- Check Spotify app is in "production" mode, not development

## Performance Optimization

For better performance with large models:
- Consider upgrading to Vercel Pro ($20/mo) for more memory (3GB)
- Or use a serverless function with higher memory allocation
- Cache model in memory on first load

## Database URL Format Examples

**PostgreSQL:**
```
postgresql://user:password@host:port/dbname
```

**Render.com (auto-formatted):**
```
postgresql://username:password@dpg-xxxxx.render.com:5432/dbname
```

Need help with any step? Check the Vercel docs: https://vercel.com/docs
