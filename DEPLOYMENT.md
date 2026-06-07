# 🚀 Deploying to Vercel

## What Was Missing (Now Fixed!)

Your project was missing critical configuration files needed for Vercel deployment:

1. **`requirements.txt`** - List of Python dependencies
2. **`vercel.json`** - Vercel configuration for serverless deployment
3. **`api/index.py`** - Serverless handler entry point
4. **`.vercelignore`** - Files to exclude from deployment

## Pre-Deployment Checklist

✅ All model files (`model/*.pkl`) are committed to GitHub  
✅ `requirements.txt` is present with all dependencies  
✅ `vercel.json` is configured correctly  
✅ `api/index.py` is set as the entry point  

## Deployment Steps

### Step 1: Ensure Everything is Committed to GitHub

```bash
git add .
git commit -m "Add Vercel deployment configuration"
git push origin main
```

### Step 2: Connect to Vercel

1. Go to [vercel.com](https://vercel.com)
2. Sign up or log in with your GitHub account
3. Click **"Add New..." → "Project"**
4. Select your **`health-level-prediction-system`** repository
5. Vercel will auto-detect it's a Python project

### Step 3: Configure Build Settings (Optional)

- **Framework Preset**: Python
- **Build Command**: (leave empty - Vercel auto-handles this)
- **Output Directory**: (leave empty)
- **Environment Variables**: (none needed for basic deployment)

### Step 4: Deploy!

1. Click **"Deploy"**
2. Wait for the build to complete (first deployment takes ~2-3 minutes)
3. Once complete, you'll get a URL like `https://your-project.vercel.app`

## Post-Deployment

✅ **Test the live app:**
- Open your Vercel URL
- Fill out the health prediction form
- Verify predictions work correctly

## Troubleshooting

### Build Fails: "Module not found"
**Solution**: Ensure all Python packages in `app.py` are listed in `requirements.txt`

### 502 Bad Gateway / 503 Service Unavailable
**Solution**: Check the deployment logs in Vercel dashboard:
1. Go to your project on Vercel
2. Click the failed deployment
3. View the "Logs" tab for detailed error messages

### Static Files Not Loading (CSS/JS)
**Vercel automatically serves files from the `static/` and `templates/` directories**, so this shouldn't be an issue. If it occurs:
- Verify `static/` folder structure is correct
- Ensure file paths in HTML templates use relative URLs

### Model Files Not Found
**Vercel will automatically include the `model/` directory** in the build because it's in your repository. If this fails:
1. Ensure all `.pkl` files are tracked in Git (not in `.gitignore`)
2. Run `git add model/` and commit

```bash
git add model/
git commit -m "Add model files to git"
git push
```

## Production Tips

1. **Change the Flask Secret Key**: In `app.py`, line 38:
   ```python
   app.secret_key = "hrps-secret-key-2024"  # Change this!
   ```
   Generate a new random secret:
   ```python
   import secrets
   secrets.token_hex(16)
   ```

2. **Add a `.env` file for sensitive data** (optional):
   - Create `.env.local` locally (git-ignored)
   - Set environment variables in Vercel dashboard

3. **Monitor Performance**: Use Vercel's Analytics to track function execution time and errors

## Redeployment

After making code changes:

```bash
git add .
git commit -m "Your message"
git push origin main
```

Vercel will automatically redeploy! ✨

---

**Need help?** Check Vercel's [Python documentation](https://vercel.com/docs/functions/python)
