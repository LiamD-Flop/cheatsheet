# Linux - Backups

A short method of creating automatic backups

Create a little backup script
```bash
#!/bin/bash
DESTINATION=/tmp/backup # Where you want the backups to go
SOURCE=/home            # Folder that needs to be backed up

tar -cpzf $DESTINATION $SOURCE
```

Now that we have a backup script lets make a cronjob

```bash
crontab -e

# In here create a new line to execute the backup script
m h d m wd /bin/bash /path/to/script/backup.sh

# So if we'd want it to run every day
0 0 * * * /bin/bash /path/to/script/backup.sh
```