# How to Create and Manage GitHub Labels

This repository uses a label configuration file to manage GitHub labels as code.

## Label Configuration

The labels are defined in `.github/labels.yml`. This file contains all the labels used in this repository, including:

- **Pages**: Related to GitHub Pages deployment and website functionality

## Creating the "Pages" Label

### Option 1: Using GitHub Web Interface (Easiest)

1. Go to your repository on GitHub
2. Click on the "Issues" tab
3. Click on "Labels" button
4. Click "New label"
5. Enter the following details:
   - **Name**: `Pages`
   - **Description**: `Related to GitHub Pages deployment and website functionality`
   - **Color**: `#0075ca` (blue)
6. Click "Create label"

### Option 2: Using GitHub CLI

If you have the [GitHub CLI](https://cli.github.com/) installed:

```bash
gh label create "Pages" \
  --description "Related to GitHub Pages deployment and website functionality" \
  --color "0075ca" \
  --repo banyan-foundry/banyan-foundry.github.io
```

### Option 3: Using github-label-sync (Automated)

To automatically sync all labels defined in `.github/labels.yml`:

1. Install [github-label-sync](https://github.com/Financial-Times/github-label-sync):
   ```bash
   npm install -g github-label-sync
   ```

2. Run the sync command:
   ```bash
   github-label-sync --access-token YOUR_GITHUB_TOKEN banyan-foundry/banyan-foundry.github.io
   ```

   Or if `.github/labels.yml` is in a different location:
   ```bash
   github-label-sync --access-token YOUR_GITHUB_TOKEN --labels .github/labels.yml banyan-foundry/banyan-foundry.github.io
   ```

### Option 4: Using GitHub API

Using curl:

```bash
curl -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer YOUR_GITHUB_TOKEN" \
  https://api.github.com/repos/banyan-foundry/banyan-foundry.github.io/labels \
  -d '{
    "name":"Pages",
    "description":"Related to GitHub Pages deployment and website functionality",
    "color":"0075ca"
  }'
```

## Managing Labels

### Adding New Labels

1. Edit `.github/labels.yml`
2. Add your new label following the existing format:
   ```yaml
   - name: "Your Label Name"
     color: "HEXCOLOR"
     description: "Description of the label"
   ```
3. Sync using one of the methods above

### Updating Labels

Update the `.github/labels.yml` file and re-sync using your preferred method.

### Deleting Labels

Remove the label from `.github/labels.yml` and use `github-label-sync` with the `--allow-added-labels` flag to keep any labels not in the config file.

## Best Practices

- Keep label names clear and concise
- Use consistent color schemes (e.g., blue for feature-related, red for bugs)
- Provide meaningful descriptions
- Document your label conventions in this file
