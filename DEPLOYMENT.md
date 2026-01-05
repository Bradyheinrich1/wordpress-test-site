# Deployment Configuration

## Deployment Methods

Cloudways supports two methods for automated deployment from GitHub:

### Method 1: GitHub Actions (Current Setup)

This repository is configured to use GitHub Actions with the Cloudways API. When you push to the `main` branch, GitHub Actions automatically triggers deployment.

**Setup Required:**
1. Get your Cloudways API credentials:
   - Log in to Cloudways dashboard
   - Go to API & Git section
   - Generate API key
   - Note your Application ID

2. Add GitHub Secrets:
   - Go to: https://github.com/Bradyheinrich1/wordpress-test-site/settings/secrets/actions
   - Add these secrets:
     - `CLOUDWAYS_EMAIL`: Your Cloudways account email
     - `CLOUDWAYS_API_KEY`: Your Cloudways API key  
     - `CLOUDWAYS_APP_ID`: Your Cloudways Application ID

**How it works:**
- Push to `main` branch → GitHub Actions triggers → Deploys to Cloudways via API

### Method 2: Webhook-Based Deployment (Alternative)

If you prefer webhook-based deployment instead:

1. **Set up Git deployment in Cloudways:**
   - Log in to Cloudways dashboard
   - Navigate to your application
   - Go to **Application Management** > **Deployment via Git**
   - Click **Generate SSH Keys** and download the public key
   - In GitHub, go to **Settings** > **Deploy Keys** > **Add Deploy Key**
   - Paste the Cloudways public key and enable **Allow write access**
   - Back in Cloudways, enter your repository SSH URL
   - Select branch and deployment path
   - Click **Start Deployment**

2. **Set up Webhook:**
   - Cloudways will provide a webhook URL after Git setup
   - In GitHub, go to **Settings** > **Webhooks** > **Add webhook**
   - Paste the Cloudways webhook URL
   - Content type: `application/json`
   - Events: Select **Push**
   - Save

**How it works:**
- Push to GitHub → Webhook triggers → Cloudways pulls from Git → Deploys

## Which Method to Use?

- **GitHub Actions (Method 1)**: More control, visible in GitHub Actions tab, can add custom steps
- **Webhook (Method 2)**: Simpler setup, directly integrated with Cloudways Git deployment

Both methods work well. The current setup uses Method 1 (GitHub Actions).

## Testing Deployment

1. Make a small change (e.g., create a test file)
2. Commit and push:
   ```bash
   git add .
   git commit -m "Test deployment"
   git push origin main
   ```
3. Check deployment:
   - **Method 1**: Go to GitHub Actions tab to see workflow status
   - **Method 2**: Check Cloudways deployment logs
4. Verify changes on your live site

## Important Notes

- Only file changes are deployed (not database content)
- WordPress core files should be managed separately on Cloudways
- User uploads are not automatically synced
- Custom themes and plugins will be deployed

