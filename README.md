# Auto-Sync GitHub Action

Automatically creates pull requests to sync the `master` branch into `dev` when new commits are available.

## Features

- 🔄 **Automatic Sync**: Creates PRs when `dev` is behind `master`
- 🔄 **Smart Updates**: Updates existing sync PRs with new master commits instead of creating duplicates
- ⏰ **Scheduled Checks**: Runs every 6 hours to check for updates
- 🚫 **Duplicate Prevention**: Skips creation if sync PR already exists
- ⚠️ **Conflict Detection**: Creates special PRs when merge conflicts occur
- 📝 **Detailed Information**: Includes commit summaries and sync statistics
- 💬 **Auto Comments**: Notifies when PRs are updated with new changes

## Setup Instructions

### 1. Create GitHub Personal Access Token

1. Go to [GitHub Settings > Personal Access Tokens > Tokens (classic)](https://github.com/settings/tokens)
2. Click **"Generate new token (classic)"**
3. Configure the token:

- **Note**: `Auto-sync workflow token`
- **Expiration**: Choose appropriate duration (recommended: 90 days or 1 year)
- **Scopes**: Select the following permissions:

#### Required Token Permissions

| Scope          | Permission                                      | Description                                           |
| -------------- | ----------------------------------------------- | ----------------------------------------------------- |
| **`repo`**     | Full control of private repositories            | Access to repository content, PRs, and branches       |
| **`workflow`** | Update GitHub Action workflows                  | Allows workflow to interact with GitHub Actions       |
| **`read:org`** | Read org and team membership, read org projects | Required for user assignment and organization context |

⚠️ **Important**: All three scopes are required for full functionality. Without `read:org`, auto-assignment features will fail.

4. Click **"Generate token"**
5. **Copy the token** (you won't see it again!)

### 2. Add Repository Secret

1. Go to your repository **Settings > Secrets and variables > Actions**
2. Click **"New repository secret"**
3. Configure:

- **Name**: `SYNC_TOKEN`
- **Secret**: Paste your GitHub token from step 1

4. Click **"Add secret"**

📚 [GitHub Docs: Creating repository secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository)

### 3. Create PR Labels

Go to your repository **Issues > Labels** and create these labels:

| Label             | Color     | Description                  |
| ----------------- | --------- | ---------------------------- |
| `auto-sync`       | `#0366d6` | Automatic synchronization PR |
| `maintenance`     | `#fbca04` | Repository maintenance task  |
| `conflicts`       | `#d73a49` | Merge conflicts detected     |
| `needs-attention` | `#e99695` | Manual intervention required |

📚 [GitHub Docs: Managing labels](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels)

### 4. Add Workflow File

1. Create the workflow directory: `.github/workflows/`
2. Add the workflow file: `auto-sync-dev.yml`
3. Copy the workflow content from this repository
4. Commit and push to `master` branch

```bash
mkdir -p .github/workflows
# Copy the workflow file content
git add .github/workflows/auto-sync-dev.yml
git commit -m "feat: add auto-sync workflow"
git push origin master
```
