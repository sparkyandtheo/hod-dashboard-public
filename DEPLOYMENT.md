# Deployment Guide — HOD Dashboard on Netlify

## Setup

### 1. Create GitHub Repository

```bash
# If not already created
# Go to https://github.com/sparkyandtheo/
# New repository → hod-dashboard-public
# Make it PUBLIC (password-protected frontend)
```

### 2. Push to GitHub

```bash
cd /home/clone-williamc/hod-dashboard-public
git remote add origin git@github.com:sparkyandtheo/hod-dashboard-public.git
git push -u origin main
```

### 3. Deploy to Netlify

1. Go to https://app.netlify.com/
2. Click "New site from Git"
3. Select "GitHub" → "sparkyandtheo" → "hod-dashboard-public"
4. Build settings:
   - Build command: (leave blank)
   - Publish directory: `.`
5. Advanced → Environment variables (optional):
   - None required for this deployment
6. Deploy

### 4. Get Site ID & Auth Token

After deployment:

```bash
# Site ID: Find in Netlify dashboard → Site settings → General → Site ID
# Auth Token: Go to https://app.netlify.com/user/applications/personal-access-tokens
#   → Create new → Copy token
```

### 5. Add GitHub Secrets

```bash
# Go to GitHub repo → Settings → Secrets and variables → Actions
# Add two secrets:
# - NETLIFY_AUTH_TOKEN = <your-netlify-auth-token>
# - NETLIFY_SITE_ID = <your-netlify-site-id>
```

### 6. Test CI/CD

```bash
# Make a small change and push
git commit --allow-empty -m "Test CI/CD trigger"
git push origin main
# Watch GitHub Actions → GitHub should trigger Netlify deploy
# Check Netlify dashboard for deployment status
```

## Security

### Password Protection

The dashboard is password-protected via `auth.html`:

**Default password:** `HOD2024Secure!`

**To change:**
1. Edit `auth.html`
2. Find: `const CORRECT_PASSWORD = 'HOD2024Secure!';`
3. Replace with new password
4. Push to GitHub → Netlify auto-deploys

### Session Management

- Password is stored in browser `sessionStorage`
- Clears when browser closes
- No cookies, no external auth service needed
- Client-side only (good for static hosting)

### Future Improvements

For production, consider:
- Server-side authentication (auth0, Firebase, etc.)
- API key protection for dashboard endpoint
- HTTPS-only (Netlify provides this by default)
- Rate limiting on deployments
- Access logs

## Updating Dashboard

### Option 1: Auto-sync (Recommended)

Create a cron job in the main workspace:

```bash
0 9,13,17 * * 1-5 /home/clone-williamc/scripts/sync-dashboard.sh
```

The script:
```bash
#!/bin/bash
cp /home/clone-williamc/hod_share/Jen/Dashboard/index.html /home/clone-williamc/hod-dashboard-public/dashboard.html
cd /home/clone-williamc/hod-dashboard-public
git add dashboard.html
git commit -m "Auto-sync dashboard from main workspace"
git push origin main
```

### Option 2: Manual Update

```bash
cp /home/clone-williamc/hod_share/Jen/Dashboard/index.html /home/clone-williamc/hod-dashboard-public/dashboard.html
cd /home/clone-williamc/hod-dashboard-public
git add dashboard.html
git commit -m "Update dashboard metrics"
git push origin main
# Netlify auto-deploys
```

## Troubleshooting

### Dashboard shows blank page

Check browser console (F12 → Console):
- If "Invalid access key" error → auth not working
- If other error → check GitHub Actions logs

### Netlify deploy failed

Check:
1. GitHub Actions logs → "Deploy to Netlify" workflow
2. Netlify dashboard → Deploy logs
3. Make sure `NETLIFY_AUTH_TOKEN` and `NETLIFY_SITE_ID` are set

### Password not working

1. Check `auth.html` has correct password
2. Clear browser cache
3. Try incognito window (fresh sessionStorage)
4. Check browser console for errors

## Public URL

After deployment:

```
https://hod-dashboard.netlify.app/
(or custom domain if configured)
```

Bookmark this URL and share with team. Password required on first access.

## Monitoring

GitHub Actions will log:
- Push event → automatic deploy
- Deploy status → success/failure
- Netlify deployment logs → available in dashboard

---

**Questions?** Check GitHub Actions logs or Netlify deploy logs for detailed error messages.
