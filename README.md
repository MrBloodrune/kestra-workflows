# Kestra Workflows Repository

This repository contains Kestra workflows for the timescaledb-ai-toolkit project.

## Structure

- `/flows/dev/` - Development workflows and testing
- `/flows/prod/` - Production workflows
- `/flows/system/` - System workflows (like Git sync)

## Setup Instructions

1. Clone this repository
2. Copy `.env.example` to `.env` and update the values
3. Configure your GitHub credentials:
   - Create a Personal Access Token with `repo` scope
   - Set `GITHUB_USERNAME` and `GITHUB_TOKEN` in your `.env`
   - Set `WEBHOOK_KEY` for manual workflow triggers

## Git Sync Configuration

The repository uses Kestra's Git sync functionality to automatically sync workflows:

1. System workflow `/flows/system/git-sync.yml` handles synchronization
2. Syncs every 15 minutes automatically
3. Manual sync available via webhook
4. All flows under `/flows` are synced to Kestra

## Environment Variables

Key environment variables required:

```bash
# Kestra Git Integration
KESTRA_GIT_URL=https://github.com/MrBloodrune/kestra-workflows
KESTRA_GIT_USERNAME=your-github-username
KESTRA_GIT_TOKEN=your-github-token
GITHUB_USERNAME=your-github-username
GITHUB_TOKEN=your-github-personal-access-token
WEBHOOK_KEY=your-webhook-secret-key
```

## Example Workflows

1. `/flows/dev/sample-flow.yml` - Basic workflow example
2. `/flows/system/git-sync.yml` - Git synchronization workflow

See the individual workflow files for detailed documentation.

## Adding New Workflows

1. Create workflow file in appropriate namespace directory:
   - `/flows/dev/` for development
   - `/flows/prod/` for production
2. Follow the Kestra YAML format
3. Commit and push to repository
4. Automatic sync will deploy to Kestra

## Manual Sync

To trigger manual sync, use the webhook endpoint:
```bash
curl -X POST https://your-kestra-host/api/v1/executions/webhook/system/sync_from_git/your-webhook-key
```