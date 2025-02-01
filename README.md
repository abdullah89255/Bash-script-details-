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

# Got it! Here are **specific, practical Bash script examples** for different tasks.  

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

# **🔥 Need More Custom Scripts?**
Let me know what specific task you need automated! 🚀😊
