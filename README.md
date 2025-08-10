# Prowlarr

Indexer manager and proxy for PVR applications like Radarr and Sonarr.

## Quick Start

1. **Clone this repository:**
   ```bash
   git clone git@github.com:leverson83/docker-prowlarr.git
   cd docker-prowlarr
   ```

2. **Edit environment file:**
   ```bash
   cp env.example .env
   nano .env
   # Edit .env with your settings
   ```

3. **Start the service:**
   ```bash
   docker compose up -d
   ```

4. **Access the web interface:**
   - URL: http://your-server:30090
   - Default credentials: First time setup will prompt for admin user

## Configuration

- **Port:** 30090
- **Config directory:** `${DATA_PATH}/prowlarr/config`
- **Database:** SQLite (included)

## Environment Variables

- `TZ` - Timezone (default: Australia/Brisbane)
- `DATA_PATH` - Application data storage path
- `PORT` - Web interface port (default: 30090)
- `PUID` - User ID for file permissions (default: 1000)
- `PGID` - Group ID for file permissions (default: 1000)

## Integration with Other Services

### Radarr Setup
1. In Radarr, go to **Settings** → **Indexers**
2. Click **Add** → **Prowlarr**
3. Enter your Prowlarr URL: `http://your-server:30090`
4. Add your API key from Prowlarr

### Sonarr Setup
1. In Sonarr, go to **Settings** → **Indexers**
2. Click **Add** → **Prowlarr**
3. Enter your Prowlarr URL: `http://your-server:30090`
4. Add your API key from Prowlarr

## Adding Indexers

1. **Access Prowlarr web interface**
2. **Go to Indexers tab**
3. **Click Add Indexer**
4. **Choose your indexer type** (e.g., NZBGeek, NZBPlanet, etc.)
5. **Enter your credentials** and test the connection
6. **Enable the indexer** for Radarr and/or Sonarr

## Notes

- Prowlarr doesn't require access to your media folders - it only manages indexers
- All configuration is stored on your NAS for easy backup and migration
- Prowlarr will automatically sync indexer configurations with Radarr and Sonarr 