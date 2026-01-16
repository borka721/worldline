# 🔒 How to Securely Hide and Store Your Personal Access Token

## ⚠️ Important Security Rules

1. **NEVER commit tokens to Git** - Your `.gitignore` already protects `.env` files
2. **NEVER share tokens publicly** - Treat them like passwords
3. **NEVER hardcode tokens in code** - Always use environment variables or secure storage

## ✅ Secure Methods to Store Your Token

### Method 1: Git Credential Helper (Recommended for Local Development)

This stores your token securely in your system's credential store:

```bash
# Configure Git to store credentials
git config --global credential.helper store

# Or use cache (temporary, more secure)
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'  # 1 hour
```

**How it works:**
- First time you push: Enter username and token
- Git saves it securely in `~/.git-credentials` (store) or memory (cache)
- Future pushes won't ask for credentials

**Location of stored credentials:**
- Store mode: `~/.git-credentials` (encrypted by your OS)
- Cache mode: Memory only (cleared after timeout)

### Method 2: SSH Keys (Most Secure - Recommended)

Use SSH instead of HTTPS to avoid tokens entirely:

```bash
# 1. Generate SSH key (if you don't have one)
ssh-keygen -t ed25519 -C "your_email@example.com"

# 2. Start SSH agent
eval "$(ssh-agent -s)"

# 3. Add your SSH key
ssh-add ~/.ssh/id_ed25519

# 4. Copy public key to clipboard
cat ~/.ssh/id_ed25519.pub

# 5. Add to GitHub:
#    - Go to: https://github.com/settings/keys
#    - Click "New SSH key"
#    - Paste your public key

# 6. Change remote to SSH
git remote set-url origin git@github.com:borka721/worldline.git

# 7. Test connection
ssh -T git@github.com

# 8. Push (no token needed!)
git push -u origin main
```

### Method 3: Environment Variable (For CI/CD)

For GitHub Actions, use **Secrets** (not environment variables in your code):

1. Go to your repository: https://github.com/borka721/worldline
2. Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Name: `GITHUB_TOKEN`
5. Value: Your personal access token
6. Use in workflow: `${{ secrets.GITHUB_TOKEN }}`

### Method 4: Git Credential Manager (Cross-platform)

Install Git Credential Manager for secure token storage:

**Linux:**
```bash
# Install Git Credential Manager
wget https://github.com/git-ecosystem/git-credential-manager/releases/latest/download/gcm-linux_amd64.2.4.1.deb
sudo dpkg -i gcm-linux_amd64.2.4.1.deb
git config --global credential.credentialStore secretservice
```

## 🛡️ Security Best Practices

### ✅ DO:
- Use SSH keys when possible
- Use Git credential helper for HTTPS
- Rotate tokens regularly (every 90 days)
- Use tokens with minimal required scopes
- Revoke tokens if compromised
- Use different tokens for different projects

### ❌ DON'T:
- Commit tokens to Git (even in comments!)
- Share tokens in chat/email
- Use tokens in public repositories
- Hardcode tokens in source code
- Use your GitHub password for Git operations

## 🔍 Check if Your Token is Exposed

If you accidentally committed a token:

1. **Check Git history:**
   ```bash
   git log --all --full-history --source -- "*" | grep -i "token"
   ```

2. **If found, immediately:**
   - Revoke the token on GitHub
   - Create a new token
   - Remove from Git history (if needed, use `git filter-branch` or BFG Repo-Cleaner)

## 🔄 Rotating Your Token

1. Generate new token on GitHub
2. Update stored credentials:
   ```bash
   # Remove old credentials
   git config --global --unset credential.helper
   rm ~/.git-credentials  # If using store mode
   
   # Reconfigure
   git config --global credential.helper store
   ```
3. Push again (will prompt for new token)
4. Revoke old token on GitHub

## 📝 Quick Setup for Your Project

**Easiest method (SSH):**
```bash
# Check if you have SSH key
ls -la ~/.ssh/id_*.pub

# If not, generate one
ssh-keygen -t ed25519 -C "borka721@github"

# Add to GitHub and change remote
git remote set-url origin git@github.com:borka721/worldline.git
git push -u origin main
```

**Alternative (HTTPS with credential helper):**
```bash
git config --global credential.helper store
git push -u origin main
# Enter username: borka721
# Enter password: [paste your token]
# Credentials saved securely!
```

## 🔐 Verify Your Setup is Secure

```bash
# Check what's being tracked by Git (should NOT include .env or tokens)
git ls-files | grep -E "(\.env|token|secret|credential)"

# Check remote URL (should be HTTPS or SSH, not with embedded token)
git remote -v
```

Your token is now secure! 🎉
