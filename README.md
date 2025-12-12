# S3 Backup Automation Script

A lightweight automation tool that backs up a local folder to an Amazon S3 bucket using AWS CLI.
The script creates timestamped backup folders, logs results, and performs safety checks before running.

This project demonstrates practical DevOps and Cloud Engineering skills including automation, S3 operations, logging, and scripting.

---

## ⚡ Features

* Automated backup from local folder to S3
* Timestamped backup directories
* Validates that the source folder exists
* Logs success or failure to a local file
* Works on Git Bash, Linux, macOS
* Simple to schedule (cron or Windows Task Scheduler)

---

## 📦 Requirements

Make sure you have the following installed and configured:

* **AWS CLI**
* **Configured AWS credentials**

  ```bash
  aws configure
  ```
* An existing **S3 bucket**
* Git Bash (Windows) or any Linux-like terminal

---

## 📁 Project Structure

```
s3-backup-project/
│
├── README.md             # Documentation
|__ backup.log            

     
```

---

## 🚀 How to Use

### 1. Make the script executable

```bash
chmod +x s3-backup.sh
```

### 2. Run the backup

```bash
./s3-backup.sh
```

### 3. Check your S3 bucket

```bash
aws s3 ls s3://ice-2025
```

You will see folders like:

```
backup-2025-12-12_22-15-41
```

### 4. Check the log file

```
backup.log
```

Example entry:

```
2025-12-12_22-15-41 - SUCCESS: Backup completed.
```

---

## 🔧 Configuration

Edit the top of `s3-backup.sh` to match your folder and bucket:

```bash
LOCAL_FOLDER="/c/Users/USER/Documents/s3-backup-project"
S3_BUCKET="s3://ice-2025"
LOG_FILE="/c/Users/USER/Documents/s3-backup-project/backup.log"
```

---

## 📜 Full Script (for reference)

```bash
#!/bin/bash
# s3-backup.sh

# Configuration
LOCAL_FOLDER="/c/Users/USER/Documents/s3-backup-project"
S3_BUCKET="s3://ice-2025"
LOG_FILE="/c/Users/USER/Documents/s3-backup-project/backup.log"

# Timestamp
TIMESTAMP=$(date +"%Y-%m-%d_%H-%M-%S")

# Check if local folder exists
if [ ! -d "$LOCAL_FOLDER" ]; then
    echo "$TIMESTAMP - ERROR: Local folder $LOCAL_FOLDER does not exist." >> "$LOG_FILE"
    exit 1
fi

# Backup to S3 with timestamped folder
aws s3 sync "$LOCAL_FOLDER" "$S3_BUCKET/backup-$TIMESTAMP"

# Log result
if [ $? -eq 0 ]; then
    echo "$TIMESTAMP - SUCCESS: Backup completed." >> "$LOG_FILE"
else
    echo "$TIMESTAMP - ERROR: Backup failed." >> "$LOG_FILE"
fi
```

---

## 📸 Screenshots (Optional)

Place any screenshots inside the `examples/` folder and reference them here:

```
![Backup Screenshot](examples/screenshot.png)
```

---

## 🧪 Real-World Use Cases

This script is suitable for:

* Daily or weekly automated backups
* Offsite storage for projects, logs, configs
* A small DevOps automation task
* Demonstrating AWS CLI + scripting knowledge
* Cloud Engineering practice projects

---

## 🔮 Future Improvements

These are planned or optional enhancements:

* Email notifications via AWS SNS or SES
* Slack or Telegram alerts
* Auto-delete old backups (retention policy)
* Add color-coded terminal output
* Progress bar mode
* Backup compression (zip/tar) before upload
* Cron or Windows Task Scheduler examples
* Multi-folder backup support

---

## 🧑‍💻 Author

**Haneef Olajobi**
Cloud Engineering Practice Project
2025
