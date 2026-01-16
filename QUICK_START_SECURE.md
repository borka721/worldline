# 🚀 Quick Start: Secure Token Setup

## Option 1: SSH (Recommended - No Token Needed!)

```bash
# 1. Check if you have SSH key
ls -la ~/.ssh/id_*.pub

# 2. If no key exists, generate one
ssh-keygen -t ed25519 -C "borka721@github"
# Press Enter to accept default location
# Press Enter twice for no passphrase (or set one for extra security)

# 3. Display your public key
cat ~/.ssh/id_ed25519.pub

# 4. Copy the output and add it to GitHub:
#    Visit: https://github.com/settings/keys
#    Click "New SSH key"
#    Paste your public key

# 5. Change remote to SSH
git remote set-url origin git@github.com:borka721/worldline.git

# 6. Test connection
ssh -T git@github.com
# Should say: "Hi borka721! You've successfully authenticated..."

# 7. Push (no token needed!)
git push -u origin main
```

## Option 2: HTTPS with Credential Helper (One-time Token Entry)

```bash
# 1. Configure Git to remember credentials
git config --global credential.helper store

# 2. Push (will ask for credentials once)
git push -u origin main
# Username: borka721
# Password: [paste your Personal Access Token here]

# 3. Done! Future pushes won't ask for credentials
# Token is stored securely in ~/.git-credentials
```

## 🔑 Getting Your Personal Access Token

1. Go to: https://github.com/settings/tokens/new
2. Name: `worldline-project`
3. Expiration: Choose (90 days recommended)
4. Scopes: Check `repo` (full control)
5. Click "Generate token"
6. **Copy immediately** - you won't see it again!

## ✅ Verify It's Working

```bash
# Check remote URL
git remote -v

# Try pushing
git push

# Should work without asking for credentials!
```

## 🛡️ Security Checklist

- ✅ `.env` is in `.gitignore` (already done)
- ✅ Token stored in credential helper (not in code)
- ✅ SSH key added to GitHub (if using SSH)
- ✅ Token has minimal required scopes

**Your token is now hidden and secure!** 🔒

For more details, see `SECURITY_TOKEN_GUIDE.md`
