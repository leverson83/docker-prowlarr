# Prowlarr Docker Setup

Prowlarr is an indexer manager/proxy for PVR apps like Radarr and Sonarr. It centralizes your indexer configuration and provides a single API endpoint for your media management applications.

## Quick Start

1. **Copy the environment file:**
   ```bash
   cp env.example .env
   ```

2. **Customize the `.env` file if needed:**
   - Update `DATA_PATH` if your NAS mount point is different
   - Change `PORT` if you want a different external port
   - Modify `TZ` if you're in a different timezone

3. **Start the service:**
   ```bash
   docker compose up -d
   ```

4. **Access the web interface:**
   - URL: `http://192.168.4.163:30090`
   - Default credentials: First time setup will prompt for admin user

## Configuration

### **Port Configuration**
- **External Port**: 30090 (customizable via `PORT` in `.env`)
- **Internal Port**: 9696 (Prowlarr's default)

### **Data Storage**
- **Config**: `/syno2/proxmox/data/prowlarr/config`
- **All Prowlarr settings, indexer configurations, and logs are stored on your NAS**

### **Environment Variables**
- `TZ`: Timezone (default: Australia/Brisbane)
- `DATA_PATH`: Base path for all data storage
- `PORT`: External port for web interface
- `PUID`: User ID for file permissions
- `PGID`: Group ID for file permissions

## Integration with Other Services

### **Radarr Setup**
1. In Radarr, go to **Settings** → **Indexers**
2. Click **Add** → **Prowlarr**
3. Enter your Prowlarr URL: `http://192.168.4.163:30090`
4. Add your API key from Prowlarr

### **Sonarr Setup**
1. In Sonarr, go to **Settings** → **Indexers**
2. Click **Add** → **Prowlarr**
3. Enter your Prowlarr URL: `http://192.168.4.163:30090`
4. Add your API key from Prowlarr

## Adding Indexers

1. **Access Prowlarr web interface**
2. **Go to Indexers tab**
3. **Click Add Indexer**
4. **Choose your indexer type** (e.g., NZBGeek, NZBPlanet, etc.)
5. **Enter your credentials** and test the connection
6. **Enable the indexer** for Radarr and/or Sonarr

## Troubleshooting

### **Container won't start**
- Check if port 30090 is already in use
- Verify your `.env` file exists and has correct values
- Check Docker logs: `docker compose logs prowlarr`

### **Can't access web interface**
- Verify the container is running: `docker compose ps`
- Check if the port mapping is correct
- Ensure no firewall is blocking the port

### **Indexer connection issues**
- Verify your indexer credentials in Prowlarr
- Check if the indexer service is accessible from your network
- Review Prowlarr logs for specific error messages

## File Structure

```
/syno2/proxmox/data/prowlarr/
├── config/
│   ├── config.xml          # Main configuration
│   ├── logs/               # Application logs
│   └── indexers/           # Indexer configurations
```

## Commands

```bash
# Start the service
docker compose up -d

# Stop the service
docker compose down

# View logs
docker compose logs -f prowlarr

# Restart the service
docker compose restart prowlarr

# Update the image
docker compose pull
docker compose up -d
```

## Notes

- Prowlarr doesn't require access to your media folders - it only manages indexers
- The downloads folder mount was removed as it's not needed for Prowlarr's core functionality
- All configuration is stored on your NAS for easy backup and migration
- Prowlarr will automatically sync indexer configurations with Radarr and Sonarr 