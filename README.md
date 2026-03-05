# GitHub to GitLab Repository Mirror

This repository provides an automated GitHub Actions workflow to mirror all your repositories from GitHub to GitLab as private projects.

## What this repo does
- Runs daily (2 AM UTC) to sync all repositories.
- Automatically creates private repositories on GitLab if they don't exist.
- Performs a full `--mirror` push (branches, tags, history).
- Handles pagination for accounts with many repositories.
- Skips the `repo_mirror` repository itself.

## Setup: Adding Secrets
1. Go to your repository settings on GitHub: **Settings -> Secrets and variables -> Actions**.
2. Add the following **Repository secrets**:
   - `GH_PAT`: GitHub Personal Access Token (classic with `repo` scope).
   - `GL_PAT`: GitLab Personal Access Token (with `api` and `write_repository` scopes).
   - `GH_USERNAME`: Your GitHub username (e.g., `sohamxda7`).
   - `GL_USERNAME`: Your GitLab username.

## How to Trigger a Manual Run
1. Go to the **Actions** tab in this repository.
2. Select the **Mirror GitHub to GitLab** workflow.
3. Click the **Run workflow** button.

## How to Change the Sync Schedule
The sync schedule is defined in `.github/workflows/mirror.yml` using a cron expression:
```yaml
on:
  schedule:
    - cron: '0 2 * * *' # Current: 2 AM UTC daily
```
You can modify this cron expression to change how often the sync runs.
- [Crontab.guru](https://crontab.guru/) can help you generate a custom schedule.

## Security
- Tokens are used only during the workflow and are not stored in the repository.
- GitHub Actions redacts secrets from logs.
- All repositories are created as **private** on GitLab.
