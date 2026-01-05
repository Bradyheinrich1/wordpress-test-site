# WordPress Test Site

A simple WordPress test site with Docker local development and automated deployment to Cloudways via GitHub Actions.

## Prerequisites

- Docker and Docker Compose installed
- Git installed
- Cloudways account with WordPress application set up
- GitHub account

## Local Development Setup

1. **Copy environment file:**
   ```bash
   cp .env.example .env
   ```

2. **Edit `.env` file** with your preferred database credentials (optional, defaults are fine for local dev)

3. **Start Docker containers:**
   ```bash
   docker-compose up -d
   ```

4. **Access WordPress:**
   - WordPress site: http://localhost:8080
   - phpMyAdmin: http://localhost:8081

5. **Complete WordPress installation:**
   - Visit http://localhost:8080
   - Follow the WordPress installation wizard
   - Use the default theme (Twenty Twenty-Four)

## Project Structure

```
WordPress Test Site/
├── docker-compose.yml          # Docker services configuration
├── .env.example                # Environment variables template
├── .gitignore                  # Git ignore rules
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions deployment workflow
└── README.md                   # This file
```

## Git Workflow

1. **Make changes locally** to your WordPress site
2. **Commit changes:**
   ```bash
   git add .
   git commit -m "Description of changes"
   ```
3. **Push to GitHub:**
   ```bash
   git push origin main
   ```
4. **GitHub Actions automatically deploys** to Cloudways

## Deployment

### Cloudways Setup

1. **Get Cloudways API credentials:**
   - Log in to Cloudways dashboard
   - Go to API & Git section
   - Generate API key
   - Note your Application ID

2. **Configure GitHub Secrets:**
   - Go to your GitHub repository
   - Navigate to Settings > Secrets and variables > Actions
   - Add the following secrets:
     - `CLOUDWAYS_EMAIL`: Your Cloudways account email
     - `CLOUDWAYS_API_KEY`: Your Cloudways API key
     - `CLOUDWAYS_APP_ID`: Your Cloudways Application ID

### Deployment Process

When you push to the `main` branch, GitHub Actions will:
1. Checkout the code
2. Deploy to Cloudways using the API
3. Sync files to your live site

## Stopping Local Development

```bash
docker-compose down
```

To remove all data (including database):
```bash
docker-compose down -v
```

## Notes

- WordPress core files are not tracked in git (managed separately on Cloudways)
- User uploads (`wp-content/uploads/`) are not versioned
- Database content (posts, pages) is not automatically synced - use database migration tools if needed
- `wp-config.php` is not tracked for security reasons

## Troubleshooting

- **Port already in use:** Change ports in `docker-compose.yml` (e.g., `8080:80` to `8082:80`)
- **Permission errors:** Ensure Docker has proper permissions
- **Database connection issues:** Check `.env` file has correct credentials

