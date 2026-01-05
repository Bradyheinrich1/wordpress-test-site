# Setup Guide - WordPress Test Site

## Quick Start Checklist

### ✅ Completed
- [x] Docker Compose configuration created
- [x] Git repository initialized
- [x] GitHub repository created: https://github.com/Bradyheinrich1/wordpress-test-site
- [x] GitHub Actions workflow configured
- [x] .gitignore configured

### 🔲 To Complete

#### 1. Local WordPress Setup
```bash
# Create .env file
cat > .env << EOF
MYSQL_DATABASE=wordpress_db
MYSQL_USER=wordpress_user
MYSQL_PASSWORD=wordpress_password
MYSQL_ROOT_PASSWORD=root_password
WORDPRESS_TABLE_PREFIX=wp_
EOF

# Start Docker containers
docker compose up -d

# Wait for containers to be ready (about 30 seconds)
# Then visit http://localhost:8080 to complete WordPress installation
```

#### 2. WordPress Installation
1. Visit http://localhost:8080
2. Select language
3. Fill in:
   - Site Title: "WordPress Test Site"
   - Username: (choose your admin username)
   - Password: (choose a strong password)
   - Email: (your email)
4. Click "Install WordPress"
5. Log in with your credentials

#### 3. Cloudways Setup

**Get Cloudways Credentials:**
1. Log in to Cloudways dashboard
2. Navigate to your WordPress application
3. Go to "API & Git" section
4. Generate API key if you don't have one
5. Note your Application ID

**Configure GitHub Secrets:**
1. Go to: https://github.com/Bradyheinrich1/wordpress-test-site/settings/secrets/actions
2. Click "New repository secret"
3. Add these three secrets:
   - Name: `CLOUDWAYS_EMAIL` → Value: (your Cloudways email)
   - Name: `CLOUDWAYS_API_KEY` → Value: (your API key)
   - Name: `CLOUDWAYS_APP_ID` → Value: (your Application ID)

#### 4. Test Edits Workflow

**Make Test Content:**
1. In WordPress admin, create a new page:
   - Title: "Test Page"
   - Content: "This is a test page created for testing the deployment workflow."
   - Publish

2. Create a new post:
   - Title: "Test Post"
   - Content: "This is a test post to verify the deployment process."
   - Publish

**Commit and Deploy:**
```bash
# Note: Content changes (posts/pages) are in the database, not files
# For file-based changes, you would commit those files
# For this test, we'll create a simple test file to verify deployment

# Create a test file to verify deployment works
echo "Deployment test - $(date)" > test-deployment.txt

# Commit and push
git add test-deployment.txt
git commit -m "Test: Add deployment test file"
git push origin main

# Check GitHub Actions tab to see deployment status
# Visit your Cloudways site to verify changes appear
```

#### 5. Verify Deployment
1. Go to GitHub repository: https://github.com/Bradyheinrich1/wordpress-test-site
2. Click "Actions" tab
3. Verify the workflow runs successfully
4. Check your Cloudways site to confirm deployment

## Important Notes

- **Content vs Files**: WordPress posts and pages are stored in the database, not files. The deployment workflow syncs files, not database content.
- **Database Sync**: To sync content between local and production, you'll need database migration tools or manual export/import.
- **File Changes**: Custom theme files, plugin files, and other code changes will be deployed automatically.
- **Uploads**: Media uploads are not versioned in git and won't be automatically synced.

## Troubleshooting

**Docker Issues:**
- Ensure Docker Desktop is running
- Check ports 8080 and 8081 are not in use
- Try `docker compose ps` to see container status

**GitHub Actions Issues:**
- Verify all three secrets are set correctly
- Check Cloudways API key has proper permissions
- Review workflow logs in GitHub Actions tab

**Deployment Issues:**
- Verify Cloudways application is running
- Check file permissions on Cloudways server
- Review Cloudways deployment logs in dashboard

