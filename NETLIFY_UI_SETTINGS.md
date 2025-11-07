# Netlify UI Settings for docs.ansai.dev

## Current Issue

Netlify is trying to run `npm run build` which is configured in the Netlify UI.

## Fix Option 1: Update Netlify UI (Recommended)

Go to: **https://app.netlify.com/sites/[your-site-name]/settings/deploys**

**Build settings:**
- Build command: (leave empty or remove)
- Publish directory: `.` (root directory)

Then click **Save** and **Trigger deploy**

## Fix Option 2: Use package.json (Already Done)

We've added a `package.json` with a no-op build script that just exits successfully:
```json
{
  "scripts": {
    "build": "echo 'Documentation is pre-built - no build needed' && exit 0"
  }
}
```

This should make the build succeed.

---

## How It Should Work

1. **Local build**: Run `mkdocs build` on your machine
2. **Push to GitHub**: Pre-built HTML files
3. **Netlify**: Just serves the static files (no build)

---

## If Builds Still Fail

Remove the build command from the Netlify UI:
1. Go to Site settings → Build & deploy → Build settings
2. Click "Edit settings"
3. Clear the "Build command" field
4. Set "Publish directory" to `.`
5. Save and redeploy

