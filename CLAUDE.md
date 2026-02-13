# CLAUDE.md - AI Assistant Guide for Umbrel Community App Store

## Repository Overview

This is a **Marcias Umbrel Community App Store** - a custom app store for [Umbrel](https://umbrel.com), a self-hosted personal server platform. The store provides Docker-based applications that can be installed via the Umbrel interface.

**App Store ID:** `marcias`
**App Store Name:** `marcias`

## Directory Structure

```
umbrel/
├── CLAUDE.md                    # This file
├── README.md                    # Project documentation (Polish)
├── umbrel-app-store.yml         # App store configuration
└── marcias-<app-name>/          # Individual app directories
    ├── umbrel-app.yml           # App manifest
    ├── docker-compose.yml       # Docker service definitions
    └── [optional files]         # Additional documentation/configs
```

## Current Applications

| App ID | Name | Port | Description |
|--------|------|------|-------------|
| marcias-aiptv | Aiptv | 51976 | IPTV M3U Proxy Server |
| marcias-calculator | Kalkulator | 3080 | React calculator with glass-morphism UI |
| marcias-dumbdrop | Upload | 7608 | File upload system |
| marcias-dumbpad | Notes | 7676 | Simple notepad |
| marcias-hello-world | Hello World | 4000 | Template app |
| marcias-it-tools | IT Tools | 8080 | IT utility tools |
| marcias-mongodb | MongoDB | 27017 | NoSQL database |
| marcias-nginx | Nginx | 580 | Web server |
| marcias-pgadmin | pgAdmin | 5051 | PostgreSQL admin tool |
| marcias-postgres | PostgreSQL | 5432 | SQL database |

## App Naming Convention

All app IDs **MUST** be prefixed with the store ID:
- Format: `marcias-<app-name>`
- Directory name must match the app ID exactly
- Use lowercase letters and hyphens only

## File Specifications

### umbrel-app.yml (App Manifest)

Required fields:
```yaml
manifestVersion: 1                    # Always 1
id: marcias-<app-name>               # Must match directory name
name: "App Display Name"             # Human-readable name
tagline: "Short description"         # One-line summary
icon: https://url/to/icon.png        # App icon URL
category: marciasmedia               # Or "Development" for dev tools
version: "1.0.0"                     # Semantic version or "free"
port: <number>                       # External port for the app
description: >-                      # Multi-line description
  Full description text.
developer: "Developer Name"
website: https://developer.site
submitter: "Submitter Name"
submission: https://submission.url
repo: https://github.com/repo
support: https://support.url
gallery:                             # Screenshot URLs (typically 3)
  - https://url/screenshot1.jpg
  - https://url/screenshot2.jpg
  - https://url/screenshot3.jpg
releaseNotes: >-
  What's new in this version.
dependencies: []                     # App dependencies (usually empty)
path: ""                             # URL path (usually empty)
defaultUsername: ""                  # Default login credentials
defaultPassword: ""                  # Leave empty if not applicable
```

### docker-compose.yml

Two patterns are used:

**Pattern 1: Direct port mapping (most common)**
```yaml
version: '3.9'
services:
  <service-name>:
    image: <docker-image>:<tag>
    restart: always
    ports:
      - "<external-port>:<internal-port>"
    volumes:
      - "${APP_DATA_DIR}/<data-dir>:/container/path"
    environment:
      VAR_NAME: value
```

**Pattern 2: Using app_proxy (for internal routing)**
```yaml
version: "3.7"
services:
  app_proxy:
    environment:
      APP_HOST: marcias-<app-name>_<service>_1
      APP_PORT: <internal-port>

  <service>:
    image: <docker-image>:<tag>
    volumes:
      - "${APP_DATA_DIR}/<data-dir>:/container/path"
```

### Key Environment Variables

- `${APP_DATA_DIR}` - Persistent data directory (REQUIRED for data persistence)
- `${PUID}` / `${PGID}` - User/Group IDs for file permissions

## Development Workflow

### Adding a New Application

1. Create directory: `mkdir marcias-<app-name>`
2. Create `umbrel-app.yml` with all required fields
3. Create `docker-compose.yml` with service definitions
4. Ensure port doesn't conflict with existing apps
5. Test locally before committing

### Port Allocation

Current ports in use: 580, 3080, 4000, 5051, 5432, 7608, 7676, 8080, 27017, 51976

When adding new apps, check existing ports to avoid conflicts.

### Testing

Add the app store to Umbrel:
```bash
sudo ~/umbrel/scripts/repo add https://github.com/<user>/umbrel.git
sudo ~/umbrel/scripts/repo update
```

Install an app:
```bash
sudo ~/umbrel/scripts/app install marcias-<app-name>
```

Remove the app store:
```bash
sudo ~/umbrel/scripts/repo remove https://github.com/<user>/umbrel.git
```

## Code Style & Conventions

### YAML Files
- Use 2-space indentation
- Multi-line strings use `>-` for folded scalar
- Keep quotes consistent (prefer double quotes for strings with special chars)
- docker-compose version typically `'3.7'` to `'3.9'`

### Language
- App descriptions are primarily in Polish (Polish locale)
- Technical identifiers (IDs, names in configs) use English

### Docker Best Practices
- Always specify `restart: always` or `restart: unless-stopped`
- Use `${APP_DATA_DIR}` for all persistent data
- Prefer `:latest` tag for images that auto-update, specific versions for stability
- Map external ports to avoid conflicts (format: `"external:internal"`)

## Common Tasks for AI Assistants

### When asked to add a new app:
1. Ask for: app name, Docker image, port requirements, description
2. Create directory with proper naming
3. Generate `umbrel-app.yml` following the template
4. Generate `docker-compose.yml` with appropriate configuration
5. Verify port doesn't conflict with existing apps

### When asked to modify an app:
1. Read both `umbrel-app.yml` and `docker-compose.yml`
2. Make targeted changes
3. Ensure port consistency between files
4. Maintain existing formatting conventions

### When asked to list apps:
- Reference the table above or scan `marcias-*/umbrel-app.yml` files

## Git Workflow

- Main development happens on feature branches (`claude/*`)
- Commit messages should be descriptive
- Push changes with: `git push -u origin <branch-name>`

## Important Notes

1. **Port Consistency**: The `port` in `umbrel-app.yml` should match the external port in `docker-compose.yml`
2. **Data Persistence**: Always use `${APP_DATA_DIR}` for volumes to ensure data survives container restarts
3. **Icon URLs**: Must be publicly accessible HTTPS URLs
4. **Gallery Images**: Typically 3 screenshots showing the app interface
5. **Dependencies**: Most apps have empty dependencies `[]`; only add if app requires another marcias app
