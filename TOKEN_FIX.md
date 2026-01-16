# ⚠️ Token Scope Issue - Quick Fix

Your token needs the `workflow` scope to push GitHub Actions files.

## Solution: Update Your Token

1. **Go to GitHub Token Settings:**
   https://github.com/settings/tokens

2. **Find your token** (or create a new one)

3. **Edit the token** and make sure these scopes are checked:
   - ✅ `repo` (Full control of private repositories)
   - ✅ `workflow` (Update GitHub Action workflows) ← **This one is missing!**

4. **Save the token**

5. **Update stored credentials:**
   ```bash
   rm ~/.git-credentials
   git push -u origin main
   # Enter new token when prompted
   ```

## Alternative: Create New Token with Correct Scopes

1. Go to: https://github.com/settings/tokens/new
2. Name: `worldline-project`
3. Expiration: 90 days (or your preference)
4. **Check these scopes:**
   - ✅ `repo` (Full control)
   - ✅ `workflow` (Update GitHub Action workflows)
5. Generate and copy the new token
6. Update credentials:
   ```bash
   rm ~/.git-credentials
   git push -u origin main
   # Username: borka721
   # Password: [paste new token]
   ```
