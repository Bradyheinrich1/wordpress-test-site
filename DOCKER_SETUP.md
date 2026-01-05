# Docker Setup Instructions

## Installing Docker Desktop on macOS

### Method 1: Homebrew (Recommended)
```bash
brew install --cask docker
```

### Method 2: Direct Download
1. Visit: https://www.docker.com/products/docker-desktop/
2. Download Docker Desktop for Mac (Apple Silicon or Intel)
3. Open the `.dmg` file
4. Drag Docker.app to Applications folder
5. Open Docker Desktop from Applications

## Starting Docker

1. **Launch Docker Desktop:**
   - Open Applications folder
   - Double-click Docker.app
   - Or use Spotlight: Press `Cmd + Space`, type "Docker", press Enter

2. **Wait for Docker to start:**
   - Look for the Docker whale icon in your menu bar
   - Wait until it shows "Docker Desktop is running"
   - This may take 1-2 minutes on first launch

3. **Verify Docker is running:**
   ```bash
   docker --version
   docker compose version
   ```

## Starting WordPress

Once Docker is running:

```bash
cd "/Users/bradyheinrich/Desktop/WordPress Test Site"

# Create .env file if you haven't already
cat > .env << EOF
MYSQL_DATABASE=wordpress_db
MYSQL_USER=wordpress_user
MYSQL_PASSWORD=wordpress_password
MYSQL_ROOT_PASSWORD=root_password
WORDPRESS_TABLE_PREFIX=wp_
EOF

# Start containers
docker compose up -d

# Check status
docker compose ps
```

## Accessing WordPress

- **WordPress Site:** http://localhost:8080
- **phpMyAdmin:** http://localhost:8081

## Troubleshooting

**"command not found: docker"**
- Docker Desktop is not running
- Start Docker Desktop from Applications

**Port already in use:**
- Change ports in `docker-compose.yml` (e.g., `8080:80` to `8082:80`)

**Docker daemon not running:**
- Make sure Docker Desktop is fully started (check menu bar icon)

## Stopping WordPress

```bash
docker compose down
```

To remove all data:
```bash
docker compose down -v
```

