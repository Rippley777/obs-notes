```
#!/bin/bash

# ================================
# Backup Script for Docker + Traefik Setup
# ================================

# Directories
BACKUP_DIR="$HOME/docker-backups"
DATE=$(date +"%Y-%m-%d")
CONFIG_BACKUP_DIR="$BACKUP_DIR/config"
VOLUME_BACKUP_DIR="$BACKUP_DIR/volumes"
LOG_FILE="$BACKUP_DIR/backup.log"

# Create backup directories
mkdir -p "$CONFIG_BACKUP_DIR"
mkdir -p "$VOLUME_BACKUP_DIR"

# Log function
log() {
  echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

log "Starting backup process..."

# Backup Docker Volumes
log "Backing up Docker volumes..."
VOLUMES=$(docker volume ls -q)

if [ -z "$VOLUMES" ]; then
  log "No volumes found to back up."
else
  for VOLUME in $VOLUMES; do
    log "Backing up volume: $VOLUME"
    docker run --rm -v "$VOLUME:/data" -v "$VOLUME_BACKUP_DIR:/backup" alpine tar czf "/backup/$VOLUME-$DATE.tar.gz" /data || log "Failed to back up volume: $VOLUME"
  done
fi

# Backup Configuration Files
log "Backing up configuration files..."
DOCKER_COMPOSE_DIRS=(
  "$HOME/traefik"
  "$HOME/multi-apps"
)

for DIR in "${DOCKER_COMPOSE_DIRS[@]}"; do
  if [ -d "$DIR" ]; then
    log "Backing up configuration in: $DIR"
    tar czf "$CONFIG_BACKUP_DIR/$(basename $DIR)-config-$DATE.tar.gz" -C "$DIR" . || log "Failed to back up configuration: $DIR"
  else
    log "Directory not found: $DIR"
  fi

done

# Cleanup old backups (optional, keep last 7 days)
log "Cleaning up old backups..."
find "$BACKUP_DIR" -type f -mtime +7 -exec rm -f {} \;

# Verify Backups
log "Verifying backups..."
if [ "$(ls -A $CONFIG_BACKUP_DIR)" ]; then
  log "Configuration files backed up successfully."
else
  log "No configuration backups found!"
fi

if [ "$(ls -A $VOLUME_BACKUP_DIR)" ]; then
  log "Volumes backed up successfully."
else
  log "No volume backups found!"
fi

log "Backup process completed."

# Summary of backup location
log "Backups are stored in: $BACKUP_DIR"

```