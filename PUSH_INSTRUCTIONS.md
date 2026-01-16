# Push to GitHub - Authentication Required

Your code is ready to push, but you need to authenticate with GitHub first. Choose one of these methods:

## Option 1: Personal Access Token (Recommended for HTTPS)

1. **Create a Personal Access Token:**
   - Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - Give it a name (e.g., "worldline-project")
   - Select scopes: `repo` (full control of private repositories)
   - Click "Generate token"
   - **Copy the token immediately** (you won't see it again!)

2. **Push using the token:**
   ```bash
   git push -u origin main
   ```
   When prompted:
   - Username: `borka721`
   - Password: **paste your personal access token** (not your GitHub password)

## Option 2: Configure Git Credential Helper (One-time setup)

After the first push with token, you can cache credentials:

```bash
git config --global credential.helper store
git push -u origin main
```

Then enter your username and token once, and it will be saved.

## Option 3: Use SSH (If you have SSH keys set up)

If you have SSH keys configured with GitHub:

```bash
git remote set-url origin git@github.com:borka721/worldline.git
git push -u origin main
```

## Quick Push Command

Once authenticated, simply run:

```bash
git push -u origin main
```

## Verify Push

After pushing, visit: https://github.com/borka721/worldline

You should see:
- ✅ All your files
- ✅ README.md
- ✅ CI/CD workflow in the Actions tab
