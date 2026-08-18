Task 1: Log Rotation Script

Create log_rotate.sh that:

    Takes a log directory as an argument (e.g., /var/log/myapp)
    Compresses .log files older than 7 days using gzip
    Deletes .gz files older than 30 days
    Prints how many files were compressed and deleted
    Exits with an error if the directory doesn't exist

karishma@MyPc:~/practice$ cat log_rotate.sh 
#!/bin/bash

# Usage: ./log_rotate.sh

LOG_DIR="/var/log"

if [ ! -d "$LOG_DIR" ]; then
    echo "Error: directory does not exist: $LOG_DIR" >&2
    exit 1
fi

compressed=$(find "$LOG_DIR" -type f -name "*.log" -mtime +7 -print0 |
    while IFS= read -r -d '' file; do
        gzip "$file"
        echo 1
    done | wc -l)

deleted=$(find "$LOG_DIR" -type f -name "*.gz" -mtime +30 -print0 |
    while IFS= read -r -d '' file; do
        rm -f "$file"
        echo 1
    done | wc -l)

echo "Compressed: $compressed file(s)"
echo "Deleted: $deleted file(s)"
karishma@MyPc:~/practice$ sudo ./log_rotate.sh 
Compressed: 0 file(s)
Deleted: 0 file(s)

***********************************************************************

Task 2: Server Backup Script

Create backup.sh that:

    Takes a source directory and backup destination as arguments
    Creates a timestamped .tar.gz archive (e.g., backup-2026-02-08.tar.gz)
    Verifies the archive was created successfully
    Prints archive name and size
    Deletes backups older than 14 days from the destination
    Handles errors — exit if source doesn't exist
    
    
    #!/bin/bash

# Usage: ./backup.sh <source_directory> <backup_destination>

SOURCE_DIR="$1"
BACKUP_DIR="$2"

if [ -z "$SOURCE_DIR" ] || [ -z "$BACKUP_DIR" ]; then
    echo "Usage: $0 <source_directory> <backup_destination>" >&2
    exit 1
fi

# Check that the source directory exists
if [ ! -d "$SOURCE_DIR" ]; then
    echo "Error: source directory does not exist: $SOURCE_DIR" >&2
    exit 1
fi

# Create backup destination if it doesn't exist
if [ ! -d "$BACKUP_DIR" ]; then
    mkdir -p "$BACKUP_DIR" || {
        echo "Error: could not create backup destination: $BACKUP_DIR" >&2
        exit 1
    }
fi

# Create timestamped archive
TIMESTAMP=$(date +%Y-%m-%d)
ARCHIVE_NAME="backup-${TIMESTAMP}.tar.gz"
ARCHIVE_PATH="${BACKUP_DIR}/${ARCHIVE_NAME}"

if tar -czf "$ARCHIVE_PATH" -C "$(dirname "$SOURCE_DIR")" "$(basename "$SOURCE_DIR")"; then
    echo "Archive created successfully."
else
    echo "Error: failed to create archive." >&2
    exit 1
fi

# Verify the archive exists and is readable
if [ ! -f "$ARCHIVE_PATH" ] || ! tar -tzf "$ARCHIVE_PATH" > /dev/null 2>&1; then
    echo "Error: archive verification failed." >&2
    exit 1
fi

# Print archive name and size
ARCHIVE_SIZE=$(du -h "$ARCHIVE_PATH" | cut -f1)

echo "Archive: $ARCHIVE_NAME"
echo "Size: $ARCHIVE_SIZE"

# Delete backups older than 14 days
find "$BACKUP_DIR" -type f -name "backup-*.tar.gz" -mtime +14 -delete

echo "Old backups older than 14 days have been deleted."


./backup.sh /home/karishma/Documents/ /home/karishma/practice/
Archive created successfully.
Archive: backup-2026-08-18.tar.gz
Size: 44K
Old backups older than 14 days have been deleted.
karishma@MyPc:~/practice$ 


**************************************************************************

Read: crontab -l — what's currently scheduled?
Understand cron syntax:

* * * * *  command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)

Write cron entries (in your markdown, don't apply if unsure) for:

    Run log_rotate.sh every day at 2 AM
    Run backup.sh every Sunday at 3 AM
    Run a health check script every 5 minutes
    
    crontab -l
no crontab for karishma
karishma@MyPc:~$ crontab -e
no crontab for karishma - using an empty one
Select an editor.  To change later, run select-editor again.
  1. /bin/nano        <---- easiest
  2. /usr/bin/vim.basic
  3. /usr/bin/vim.tiny
  4. /usr/bin/code
  5. /bin/ed

Choose 1-5 [1]: 2
crontab: installing new crontab
karishma@MyPc:~$ crontab -l
# Run log_rotate.sh every day at 2:00 AM
0 2 * * * /path/to/log_rotate.sh

# Run backup.sh every Sunday at 3:00 AM
0 3 * * 0 /path/to/backup.sh

# Run health check every 5 minutes
*/5 * * * * /path/to/health_check.sh


****************************************************************

Task 4: Combine — Scheduled Maintenance Script

Create maintenance.sh that:

    Calls your log rotation function
    Calls your backup function
    Logs all output to /var/log/maintenance.log with timestamps
    Write the cron entry to run it daily at 1 AM



crontab: installing new crontab
karishma@MyPc:~$ crontab -l
# Run log_rotate.sh every day at 2:00 AM
0 2 * * * /path/to/log_rotate.sh

# Run backup.sh every Sunday at 3:00 AM
0 3 * * 0 /path/to/backup.sh

# Run health check every 5 minutes
*/5 * * * * /path/to/health_check.sh

0 1 * * * /home/karishma/practice/maintenance.sh
karishma@MyPc:~$ sudo /home/karishma/practice/maintenance.sh


