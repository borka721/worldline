# 🔀 How to Merge Branches

## Current Status

✅ **main** branch - Pushed to GitHub  
✅ **develop** branch - Pushed to GitHub  
✅ Both branches are in sync

## How to Merge develop into main

```bash
# 1. Make sure you're on main branch
git checkout main

# 2. Pull latest changes (if any)
git pull origin main

# 3. Merge develop into main
git merge develop

# 4. Push to GitHub
git push origin main
```

## How to Merge main into develop

```bash
# 1. Switch to develop branch
git checkout develop

# 2. Pull latest changes
git pull origin develop

# 3. Merge main into develop
git merge main

# 4. Push to GitHub
git push origin develop
```

## Quick Merge Commands

**Merge develop → main:**
```bash
git checkout main && git merge develop && git push origin main
```

**Merge main → develop:**
```bash
git checkout develop && git merge main && git push origin develop
```

## Using Pull Requests (Recommended)

Instead of merging locally, you can use GitHub Pull Requests:

1. Go to: https://github.com/borka721/worldline
2. Click "Pull requests" → "New pull request"
3. Base: `main` ← Compare: `develop`
4. Create pull request
5. Review and merge on GitHub

This is safer and gives you a review process!
