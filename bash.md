Here’s a **comprehensive Bash cheat sheet** to help you master the Linux shell and scripting quickly!

---

# **Bash Cheat Sheet**

Bash (Bourne Again SHell) is a command-line interpreter for Unix/Linux systems. It is widely used for system administration, automation, and scripting.

---

## **1. Basic Commands**

### **Navigation**
- **Current Directory**:
  ```bash
  pwd
  ```

- **Change Directory**:
  ```bash
  cd /path/to/directory  # Go to specific directory
  cd ~                   # Go to home directory
  cd ..                  # Move up one directory
  ```

- **List Files**:
  ```bash
  ls                    # List files in current directory
  ls -l                 # Detailed list (long format)
  ls -a                 # Include hidden files
  ls -lh                # Human-readable file sizes
  ```

---

## **2. File and Directory Operations**

### **Create Files and Directories**
- **Create a File**:
  ```bash
  touch filename.txt
  ```

- **Create a Directory**:
  ```bash
  mkdir new_directory
  mkdir -p parent/child  # Create parent and child directories
  ```

### **Copy Files/Directories**
- **Copy File**:
  ```bash
  cp source.txt destination.txt
  ```

- **Copy Directory**:
  ```bash
  cp -r source_dir/ destination_dir/
  ```

### **Move/Rename Files**
```bash
mv oldname.txt newname.txt
mv file.txt /path/to/destination/
```

### **Remove Files/Directories**
- **Remove Files**:
  ```bash
  rm file.txt
  rm -f file.txt  # Force delete
  ```

- **Remove Directories**:
  ```bash
  rm -r directory/        # Delete directory and contents
  rm -rf directory/       # Force delete
  ```

---

## **3. File Viewing and Searching**

### **View File Contents**
```bash
cat file.txt             # Print entire file
less file.txt            # View file interactively (scroll with 'j' and 'k')
head -n 10 file.txt      # View first 10 lines
tail -n 10 file.txt      # View last 10 lines
tail -f file.txt         # View file as it grows (useful for logs)
```

### **Search in Files**
- **Search with `grep`**:
  ```bash
  grep "search_term" file.txt       # Search for text in file
  grep -i "search_term" file.txt    # Case-insensitive search
  grep -r "search_term" /directory  # Search recursively in directory
  ```

---

## **4. File Permissions**

### **View File Permissions**
```bash
ls -l
```
Output example:
```
-rwxr-xr-- 1 user group 1234 Jan 1 12:00 file.txt
```

### **Change Permissions**
- Syntax: `chmod [options] <permissions> file`

- **Symbolic** (r=read, w=write, x=execute):
  ```bash
  chmod u+x file.txt    # Add execute for user
  chmod g-w file.txt    # Remove write for group
  chmod o+r file.txt    # Add read for others
  ```

- **Numeric** (4=read, 2=write, 1=execute):
  ```bash
  chmod 755 file.txt    # User: rwx, Group: r-x, Others: r-x
  ```

### **Change Ownership**
```bash
chown user:group file.txt  # Change owner and group
```

---

## **5. Process Management**

### **View Running Processes**
```bash
ps                     # List processes
ps aux                 # Detailed list of all processes
top                    # Interactive process viewer
htop                   # Enhanced process viewer (install required)
```

### **Kill Processes**
- **Kill by PID**:
  ```bash
  kill <PID>
  ```

- **Kill by Name**:
  ```bash
  killall process_name
  ```

- **Force Kill**:
  ```bash
  kill -9 <PID>
  ```

### **Background/Foreground Tasks**
- **Run Command in Background**:
  ```bash
  command &
  ```

- **View Background Jobs**:
  ```bash
  jobs
  ```

- **Bring Job to Foreground**:
  ```bash
  fg %1  # Bring job 1 to foreground
  ```

---

## **6. Text Processing**

### **Text Manipulation**
- **`echo`**: Print text to terminal.
  ```bash
  echo "Hello World"
  ```

- **`cut`**: Split text based on delimiter.
  ```bash
  echo "one:two:three" | cut -d: -f2  # Output: two
  ```

- **`sort`**: Sort text.
  ```bash
  sort file.txt
  ```

- **`uniq`**: Remove duplicate lines.
  ```bash
  uniq file.txt
  ```

### **Pipelines (`|`)**
Combine commands:
```bash
cat file.txt | grep "search_term" | sort | uniq
```

---

## **7. Redirection**

### **Redirect Output**
- **Overwrite File**:
  ```bash
  command > file.txt
  ```

- **Append to File**:
  ```bash
  command >> file.txt
  ```

### **Redirect Input**
```bash
command < input.txt
```

---

## **8. Loops**

### **For Loop**
```bash
for i in {1..5}; do
  echo "Number $i"
done
```

### **While Loop**
```bash
count=1
while [ $count -le 5 ]; do
  echo "Count: $count"
  ((count++))
done
```

---

## **9. Conditionals**

### **If Statements**
```bash
if [ condition ]; then
  echo "Condition met"
elif [ other_condition ]; then
  echo "Other condition"
else
  echo "No conditions met"
fi
```

**Conditions**:
- `-e file` → File exists  
- `-d dir` → Directory exists  
- `-f file` → Regular file exists  
- `-z string` → String is empty  
- `-n string` → String is not empty  

### **Test Example**
```bash
if [ -f file.txt ]; then
  echo "File exists"
fi
```

---

## **10. Environment Variables**

### **View Variables**
```bash
echo $PATH
echo $HOME
```

### **Set Variables**
```bash
MY_VAR="Hello"
export MY_VAR
```

---

## **11. Bash Scripting**

### **Script Structure**
Create a script `myscript.sh`:
```bash
#!/bin/bash

echo "Hello, $USER!"
echo "Today is $(date)"
```

### **Make Script Executable**
```bash
chmod +x myscript.sh
./myscript.sh
```

---

## **12. SSH and Networking**

### **SSH to a Remote Server**
```bash
ssh user@remote_host
```

### **Copy Files via SCP**
```bash
scp file.txt user@remote_host:/path/to/destination
scp -r folder user@remote_host:/path/
```

---

## **13. Miscellaneous**

### **History**
- Show command history:
  ```bash
  history
  ```

- Re-run a specific command:
  ```bash
  !<number>
  ```

### **Alias Commands**
Create shortcuts for commands:
```bash
alias ll='ls -lh'
alias gs='git status'
```

Add aliases to `~/.bashrc` for persistence.

---

## **14. System Information**

- **Disk Space**:
  ```bash
  df -h
  ```

- **Memory Usage**:
  ```bash
  free -h
  ```

- **System Uptime**:
  ```bash
  uptime
  ```

---

## **15. Common Debugging Tools**

### **Debugging Scripts**
Run script with debug mode:
```bash
bash -x script.sh
```

---

This **Bash cheat sheet** covers essential commands, scripting basics, and tips for efficient usage.
