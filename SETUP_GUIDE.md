# GitHub Profile README Setup Guide

This repository creates a dynamic GitHub profile README that automatically updates with your GitHub statistics daily using GitHub Actions.

## What It Does
- **Real-time GitHub stats**: Commits, repositories, stars, followers, lines of code
- **Age calculation**: Shows your age from a specified birthday
- **Beautiful SVG display**: Terminal-style layout with ASCII art
- **Dual themes**: Automatic light/dark mode support
- **Daily updates**: GitHub Actions runs automatically every day at 4 AM UTC

## Setup Instructions

### 1. Repository Setup
1. **Fork or clone** this repository to your GitHub account
2. **Rename the repository** to match your GitHub username (e.g., `yourusername/yourusername`)
3. Make sure the repository is **public** (required for GitHub profile README)

### 2. Personal Information Updates

#### Update Birthday (Required)
In `today.py`, line 450:
```python
age_data, age_time = perf_counter(daily_readme, datetime.datetime(1990, 1, 1))  # TODO: Update with your birthday
```
Replace `datetime.datetime(1990, 1, 1)` with your actual birthday.

#### Update Repository URLs (Required)
In `README.md`, replace all instances of:
- `YOUR_USERNAME` with your GitHub username
- `Your Name` with your actual name

#### Customize SVG Files (Optional)
Edit `dark_mode.svg` and `light_mode.svg` to personalize:
- Username (line 47): `your@username`
- Operating systems, IDEs, programming languages
- Contact information (emails, LinkedIn, Discord)
- Hobbies and interests
- Company/organization name

### 3. GitHub Personal Access Token Setup

#### Create Token
1. Go to **GitHub Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
2. Click **"Generate new token (classic)"**
3. Set expiration to **"No expiration"** (or your preferred duration)
4. Select these scopes:
   - `public_repo` (Repository permissions)
   - `read:user` (Account permissions)
   - `user:follow` (Account permissions)

#### Required Permissions
The token needs these specific permissions (as noted in `today.py`):
- **Repository permissions**: read:Commit statuses, read:Contents, read:Issues, read:Metadata, read:Pull Requests
- **Account permissions**: read:Followers, read:Starring, read:Watching

### 4. Repository Secrets Setup
1. Go to your repository **Settings** → **Secrets and variables** → **Actions**
2. Add these repository secrets:
   - **Name**: `ACCESS_TOKEN`, **Value**: Your personal access token
   - **Name**: `USER_NAME`, **Value**: Your GitHub username

### 5. Enable GitHub Actions
1. Go to your repository **Actions** tab
2. If prompted, click **"I understand my workflows, go ahead and enable them"**
3. The workflow will run automatically:
   - **On push** to main branch
   - **Daily at 4 AM UTC** (cron schedule)

### 6. Test Your Setup
1. **Manual trigger**: Go to Actions tab → "README build" → "Run workflow"
2. **Check output**: After the workflow completes, your README should display updated stats
3. **Verify files**: The workflow should update `dark_mode.svg` and `light_mode.svg`

## Customization Options

### ASCII Art
The current ASCII art in the SVG files can be replaced with your own. You can:
- Create custom ASCII art using online generators
- Use different characters or designs
- Adjust the positioning by modifying the `<tspan>` coordinates

### Additional Statistics
You can modify `today.py` to:
- Add more GitHub statistics
- Include different metrics
- Change the display format
- Add archived repository data (see commented section)

### Styling
The SVG files support:
- Custom colors (modify CSS classes)
- Different fonts (change font-family)
- Layout adjustments (modify coordinates)
- Additional sections or information

## Troubleshooting

### Common Issues
1. **Repository not updating**: Check if secrets are set correctly
2. **Permission errors**: Verify your token has the required scopes
3. **Workflow failing**: Check the Actions tab for error details
4. **Stats not showing**: Ensure your GitHub username is correct in secrets

### File Structure
```
├── .github/workflows/build.yaml  # GitHub Actions workflow
├── cache/
│   ├── requirements.txt          # Python dependencies
│   └── [hash].txt               # Generated cache files
├── dark_mode.svg                # Dark theme display
├── light_mode.svg               # Light theme display
├── today.py                     # Main stats generator
└── README.md                    # Repository README
```

## Dependencies
- `python-dateutil`: Date calculations
- `requests`: GitHub API calls
- `lxml`: XML/SVG parsing

## Credits
Forked from [Andrew Grant (Andrew6rant)](https://github.com/Andrew6rant/Andrew6rant), 2022-2025

## License
Feel free to use and modify this code for your own GitHub profile!