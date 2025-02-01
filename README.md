# Bash-script-details-
Got it! Let's go **in-depth** into **Bash scripting**, covering key **concepts, commands, examples, and best practices**.  

---

# **📌 1. What is Bash Scripting?**
A **Bash script** is a **plain text file** that contains a series of commands that the **Bash shell** executes in sequence. It automates **system tasks, file handling, user interactions, and more**.

💡 **Example Use Cases**:  
✅ Automating backups  
✅ Managing system logs  
✅ Monitoring system resources  
✅ Deploying applications  
✅ Renaming/moving multiple files  

---

# **📌 2. How to Create and Run a Bash Script**
### **Step 1: Create a Script File**
Use any text editor like `nano`, `vim`, or `echo`:
```bash
nano myscript.sh
```
Or:
```bash
echo '#!/bin/bash' > myscript.sh
```

### **Step 2: Add Commands**
Edit the file and write:
```bash
#!/bin/bash
echo "Hello, World!"
```

### **Step 3: Make it Executable**
```bash
chmod +x myscript.sh
```

### **Step 4: Run the Script**
```bash
./myscript.sh
```

---

# **📌 3. Bash Scripting Basics**
## **a) Variables**
### **Defining a Variable**
```bash
#!/bin/bash
name="Alice"
echo "Hello, $name!"
```
> 🔹 **Variables are case-sensitive** (e.g., `$NAME` and `$name` are different).  
> 🔹 Use **`$var`** to access variable values.  

### **Reading User Input**
```bash
#!/bin/bash
echo "Enter your name:"
read user_name
echo "Hello, $user_name!"
```

### **Command Substitution**
```bash
#!/bin/bash
current_date=$(date)
echo "Today is: $current_date"
```

---

## **b) Conditional Statements**
### **If-Else Example**
```bash
#!/bin/bash
num=10
if [ $num -gt 5 ]; then
    echo "Number is greater than 5"
else
    echo "Number is 5 or less"
fi
```

#### **Comparison Operators**
| Operator  | Meaning          |
|-----------|-----------------|
| `-eq`     | Equal to        |
| `-ne`     | Not equal to    |
| `-gt`     | Greater than    |
| `-lt`     | Less than       |
| `-ge`     | Greater or equal|
| `-le`     | Less or equal   |

#### **String Comparisons**
| Operator  | Meaning            |
|-----------|--------------------|
| `=`       | Equal to           |
| `!=`      | Not equal to       |
| `-z`      | Empty string check |

💡 **Example with Strings**
```bash
#!/bin/bash
echo "Enter a string:"
read input
if [ "$input" = "hello" ]; then
    echo "You typed hello!"
else
    echo "You typed something else."
fi
```

---

## **c) Loops in Bash**
### **For Loop**
```bash
#!/bin/bash
for i in {1..5}; do
    echo "Loop iteration: $i"
done
```

### **While Loop**
```bash
#!/bin/bash
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

### **Until Loop**
```bash
#!/bin/bash
count=1
until [ $count -gt 5 ]; do
    echo "Until Count: $count"
    ((count++))
done
```

---

## **d) Functions**
### **Defining and Calling a Function**
```bash
#!/bin/bash
greet() {
    echo "Hello, $1!"
}
greet "Alice"
```
> **💡 `$1`, `$2`, `$3`** represent function arguments.

---

# **📌 4. File Handling**
### **Checking if a File Exists**
```bash
#!/bin/bash
file="test.txt"
if [ -f "$file" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

### **Reading a File Line by Line**
```bash
#!/bin/bash
while IFS= read -r line; do
    echo "$line"
done < file.txt
```

### **Appending to a File**
```bash
#!/bin/bash
echo "New line of text" >> file.txt
```

---

# **📌 5. Command-Line Arguments**
```bash
#!/bin/bash
echo "Script Name: $0"
echo "First Argument: $1"
echo "Second Argument: $2"
echo "All Arguments: $@"
```
> **Run**: `./script.sh arg1 arg2`

| Special Variable | Meaning |
|-----------------|---------|
| `$0`           | Script name |
| `$1, $2, $3...` | Arguments passed |
| `$#`           | Number of arguments |
| `$@`           | All arguments |

---

# **📌 6. Process Management**
### **List Running Processes**
```bash
ps aux
```

### **Kill a Process by PID**
```bash
kill 1234  # Replace 1234 with the PID
```

### **Monitor System Usage**
```bash
top
```

---

# **📌 7. Debugging Bash Scripts**
### **Enable Debugging Mode**
Run:
```bash
bash -x script.sh
```
Or add this line inside the script:
```bash
set -x
```

### **Redirect Output to a Log File**
```bash
./script.sh > output.log 2>&1
```

---

# **📌 8. Practical Bash Scripts**
### **1️⃣ Auto Backup Script**
```bash
#!/bin/bash
backup_dir="/backup"
mkdir -p "$backup_dir"
cp -r /home/user/Documents "$backup_dir"
echo "Backup completed!"
```

### **2️⃣ Check Internet Connectivity**
```bash
#!/bin/bash
ping -c 1 google.com &> /dev/null
if [ $? -eq 0 ]; then
    echo "Internet is connected"
else
    echo "No Internet connection"
fi
```

### **3️⃣ Disk Space Monitor**
```bash
#!/bin/bash
df -h | grep "/dev/sda1"
```

---

# **📌 9. Best Practices**
✅ **Use meaningful variable names**  
✅ **Comment your code** (`# This is a comment`)  
✅ **Use indentation** for readability  
✅ **Always handle errors**  
✅ **Make scripts executable (`chmod +x script.sh`)**  

---

# Here are **specific, practical Bash script examples** for different tasks.  

---

## **1️⃣ Automated Backup Script**
This script backs up a directory to another location and appends a timestamp to the backup file.  

```bash
#!/bin/bash
# Define variables
SOURCE_DIR="/home/user/Documents"
BACKUP_DIR="/home/user/Backup"
TIMESTAMP=$(date +%Y-%m-%d_%H-%M-%S)
BACKUP_FILE="backup_$TIMESTAMP.tar.gz"

# Create a backup
mkdir -p "$BACKUP_DIR"
tar -czf "$BACKUP_DIR/$BACKUP_FILE" "$SOURCE_DIR"

# Print success message
echo "Backup completed! File saved as $BACKUP_DIR/$BACKUP_FILE"
```
✅ **Usage**: Run `./backup.sh` to create a compressed backup.  

---

## **2️⃣ Check Internet Connectivity**
This script pings **Google** and checks if the internet is connected.  

```bash
#!/bin/bash
ping -c 1 google.com &> /dev/null

if [ $? -eq 0 ]; then
    echo "Internet is connected ✅"
else
    echo "No Internet connection ❌"
fi
```
✅ **Usage**: Run `./check_internet.sh` to check connectivity.

---

## **3️⃣ Rename Multiple Files**
This script renames all `.txt` files in a folder by adding a prefix (`new_`).  

```bash
#!/bin/bash
for file in *.txt; do
    mv "$file" "new_$file"
done
echo "All text files renamed!"
```
✅ **Usage**: Place it in a folder with `.txt` files and run `./rename_files.sh`.

---

## **4️⃣ Monitor Disk Space**
This script checks if disk usage exceeds 80% and alerts the user.  

```bash
#!/bin/bash
THRESHOLD=80
USAGE=$(df -h / | grep "/" | awk '{print $5}' | sed 's/%//')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
    echo "⚠️ Warning: Disk usage is at $USAGE%!"
else
    echo "✅ Disk usage is under control ($USAGE%)"
fi
```
✅ **Usage**: Run `./disk_monitor.sh` to check disk usage.

---

## **5️⃣ Find Large Files**
This script finds files larger than **100MB** in the current directory.  

```bash
#!/bin/bash
find . -type f -size +100M -exec ls -lh {} \;
```
✅ **Usage**: Run `./find_large_files.sh` to list large files.

---

## **6️⃣ Automated System Update**
This script updates the system (Ubuntu/Debian-based).  

```bash
#!/bin/bash
echo "Updating system..."
sudo apt update && sudo apt upgrade -y
echo "System update complete ✅"
```
✅ **Usage**: Run `./update_system.sh` (requires `sudo`).

---

## **7️⃣ Extract and Count Words in a File**
This script counts occurrences of each word in a given text file.  

```bash
#!/bin/bash
echo "Enter filename:"
read filename

if [ -f "$filename" ]; then
    cat "$filename" | tr -s ' ' '\n' | sort | uniq -c | sort -nr
else
    echo "File not found!"
fi
```
✅ **Usage**: Run `./word_count.sh` and enter a filename.

---

## **8️⃣ CPU Usage Monitor**
This script continuously monitors CPU usage and alerts if it exceeds 75%.  

```bash
#!/bin/bash
while true; do
    CPU_LOAD=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'.' -f1)
    if [ "$CPU_LOAD" -gt 75 ]; then
        echo "⚠️ CPU usage high: $CPU_LOAD%"
    else
        echo "✅ CPU usage normal: $CPU_LOAD%"
    fi
    sleep 5
done
```
✅ **Usage**: Run `./cpu_monitor.sh` to monitor CPU usage.

---

## **9️⃣ Automate File Backup with Cron**
This script automatically backs up a directory every day using **cron jobs**.  

### **Step 1: Create the script**
```bash
#!/bin/bash
tar -czf /home/user/Backup/backup_$(date +%F).tar.gz /home/user/Documents
```
Save it as `daily_backup.sh`, then make it executable:
```bash
chmod +x daily_backup.sh
```

### **Step 2: Schedule with Cron**
Run:
```bash
crontab -e
```
Add this line:
```
0 2 * * * /home/user/daily_backup.sh
```
This runs the script **every day at 2 AM**.

---

## **🔟 Delete Old Log Files (Older than 7 Days)**
```bash
#!/bin/bash
LOG_DIR="/var/log"
find "$LOG_DIR" -type f -name "*.log" -mtime +7 -exec rm {} \;
echo "Deleted log files older than 7 days"
```
✅ **Usage**: Run `./delete_logs.sh` to clean up old logs.

---

# Here are some **advanced, deeply detailed Bash scripts** for different real-world use cases.  

---

# **📌 1️⃣ Automated User Account Management**  
This script **adds users**, sets passwords, and assigns them to a group.  

```bash
#!/bin/bash
# Add a new user and set a password

echo "Enter new username:"
read username

# Check if user exists
if id "$username" &>/dev/null; then
    echo "User '$username' already exists!"
    exit 1
fi

# Create user
sudo useradd -m -s /bin/bash "$username"
echo "User '$username' created!"

# Set password
echo "Enter password for $username:"
read -s password
echo "$username:$password" | sudo chpasswd
echo "Password set successfully!"

# Add user to sudo group
sudo usermod -aG sudo "$username"
echo "User '$username' added to sudo group."
```
✅ **Usage**: Run `./add_user.sh`, enter username & password.  

---

# **📌 2️⃣ Automated Server Health Check**  
This script checks **CPU, memory, and disk usage**, sending alerts if usage is too high.  

```bash
#!/bin/bash
# Monitor system health and send alerts

CPU_THRESHOLD=80
MEM_THRESHOLD=80
DISK_THRESHOLD=90

# CPU Usage
CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'.' -f1)

# Memory Usage
MEM_USAGE=$(free | awk '/Mem/{printf("%.0f"), $3/$2*100}')

# Disk Usage
DISK_USAGE=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

# Check CPU
if [ "$CPU_USAGE" -gt "$CPU_THRESHOLD" ]; then
    echo "⚠️ High CPU Usage: $CPU_USAGE%"
fi

# Check Memory
if [ "$MEM_USAGE" -gt "$MEM_THRESHOLD" ]; then
    echo "⚠️ High Memory Usage: $MEM_USAGE%"
fi

# Check Disk
if [ "$DISK_USAGE" -gt "$DISK_THRESHOLD" ]; then
    echo "⚠️ Low Disk Space: $DISK_USAGE%"
fi
```
✅ **Usage**: Run `./health_check.sh` to check system health.

---

# **📌 3️⃣ Automated MySQL Database Backup**
This script **backs up a MySQL database** and saves it with a timestamp.  

```bash
#!/bin/bash
DB_NAME="my_database"
DB_USER="root"
DB_PASS="yourpassword"
BACKUP_DIR="/backup"

# Create backup directory
mkdir -p "$BACKUP_DIR"

# Generate timestamped backup
BACKUP_FILE="$BACKUP_DIR/$DB_NAME-$(date +%F_%H-%M-%S).sql"
mysqldump -u "$DB_USER" -p"$DB_PASS" "$DB_NAME" > "$BACKUP_FILE"

# Verify success
if [ $? -eq 0 ]; then
    echo "✅ Backup successful: $BACKUP_FILE"
else
    echo "❌ Backup failed!"
fi
```
✅ **Usage**: Run `./mysql_backup.sh`.  

---

# **📌 4️⃣ Securely Transfer Files via SCP**
This script securely **copies files from one server to another** using `scp`.  

```bash
#!/bin/bash
# Secure file transfer

REMOTE_USER="user"
REMOTE_HOST="192.168.1.100"
REMOTE_DIR="/home/user/backup"
LOCAL_FILE="/home/user/data.txt"

# Transfer file
scp "$LOCAL_FILE" "$REMOTE_USER@$REMOTE_HOST:$REMOTE_DIR"

# Check if successful
if [ $? -eq 0 ]; then
    echo "✅ File transferred successfully!"
else
    echo "❌ File transfer failed!"
fi
```
✅ **Usage**: Run `./secure_transfer.sh` to send files securely.

---

# **📌 5️⃣ Auto Delete Old Backups (Older than 30 Days)**
This script **removes old backup files** from the system to free up space.  

```bash
#!/bin/bash
BACKUP_DIR="/backup"
DAYS=30

# Delete backups older than 30 days
find "$BACKUP_DIR" -type f -mtime +$DAYS -exec rm {} \;

echo "✅ Deleted backups older than $DAYS days."
```
✅ **Usage**: Run `./delete_old_backups.sh`.

---

# **📌 6️⃣ Real-Time Log File Monitor**  
This script **monitors a log file** in real-time and **alerts if an error occurs**.  

```bash
#!/bin/bash
LOG_FILE="/var/log/syslog"

echo "Monitoring $LOG_FILE for errors..."
tail -f "$LOG_FILE" | while read line; do
    if [[ "$line" == *"ERROR"* ]]; then
        echo "⚠️ ERROR detected: $line"
    fi
done
```
✅ **Usage**: Run `./log_monitor.sh` to monitor logs.

---

# **📌 7️⃣ Find and Kill High CPU Processes**  
This script finds **high CPU usage processes** and kills them if needed.  

```bash
#!/bin/bash
THRESHOLD=90

echo "Checking for high CPU usage processes..."
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head -n 10

# Kill processes above threshold
echo "Kill processes above $THRESHOLD% CPU? (y/n)"
read answer

if [[ "$answer" == "y" ]]; then
    ps -eo pid,%cpu --sort=-%cpu | awk -v threshold=$THRESHOLD '$2>threshold {print $1}' | xargs kill -9
    echo "Processes killed!"
else
    echo "No processes killed."
fi
```
✅ **Usage**: Run `./kill_high_cpu.sh`.

---

# **📌 8️⃣ Automatic File Synchronization**
This script **syncs files** between two directories using `rsync`.  

```bash
#!/bin/bash
SOURCE_DIR="/home/user/Documents"
DEST_DIR="/home/user/Backup"

# Sync files
rsync -av --delete "$SOURCE_DIR" "$DEST_DIR"

echo "✅ Files synchronized!"
```
✅ **Usage**: Run `./file_sync.sh` to sync files.

---

# **📌 9️⃣ Detect Unauthorized Login Attempts**
This script scans system logs for **failed login attempts**.  

```bash
#!/bin/bash
LOG_FILE="/var/log/auth.log"
echo "Unauthorized login attempts:"
grep "Failed password" "$LOG_FILE" | awk '{print $1, $2, $3, $9, $11}'
```
✅ **Usage**: Run `./check_failed_logins.sh`.

---

# **📌 🔟 Auto Restart a Crashed Service**
This script checks if a service is running and **restarts it if it's down**.  

```bash
#!/bin/bash
SERVICE="nginx"

if systemctl is-active --quiet "$SERVICE"; then
    echo "✅ $SERVICE is running."
else
    echo "❌ $SERVICE is down! Restarting..."
    systemctl restart "$SERVICE"
fi
```
✅ **Usage**: Run `./service_monitor.sh`.

---


Let me know **what task** you want automated! 🚀
