# Linux Command 101 

## Introduction to Linux Commands

This guide covers essential Linux commands for beginners. Commands are typed in the terminal and executed by pressing Enter.

## Basic Navigation

### `pwd` - Print Working Directory
Shows your current location in the file system.
```bash
pwd
```

### `ls` - List Files and Directories
Lists contents of the current directory.
```bash
ls          # Basic listing
ls -l       # Detailed listing
ls -la      # Include hidden files
```

### `cd` - Change Directory
Navigate between directories.
```bash
cd /home/user    # Go to specific directory
cd ..           # Go up one level
cd ~            # Go to home directory
cd -            # Go to previous directory
```

## File Operations

### `mkdir` - Create Directory
Creates new folders.
```bash
mkdir myfolder
mkdir -p path/to/nested/folder  # Create nested directories
```

### `touch` - Create Empty File
Creates new empty files.
```bash
touch myfile.txt
```

### `cp` - Copy Files
Copies files or directories.
```bash
cp file1.txt file2.txt      # Copy file
cp -r folder1 folder2       # Copy directory
```

### `mv` - Move/Rename Files
Moves or renames files and directories.
```bash
mv oldname.txt newname.txt  # Rename file
mv file.txt /home/user/     # Move file
```

### `rm` - Remove Files
Deletes files and directories.
```bash
rm file.txt        # Delete file
rm -r folder       # Delete directory
rm -rf folder      # Force delete (be careful!)
```

## Viewing File Contents

### `cat` - Display File Contents
Shows entire file content.
```bash
cat filename.txt
```

### `less` - View File Page by Page
Navigate through large files.
```bash
less filename.txt
# Use arrow keys to navigate, 'q' to quit
```

### `head` - Show First Lines
Displays first 10 lines of a file.
```bash
head filename.txt
head -n 20 filename.txt  # Show first 20 lines
```

### `tail` - Show Last Lines
Displays last 10 lines of a file.
```bash
tail filename.txt
tail -f filename.txt     # Follow file changes
```

## File Permissions

### `chmod` - Change Permissions
Modifies file permissions.
```bash
chmod 755 filename.txt   # rwx for owner, rx for group/others
chmod +x script.sh       # Add execute permission
```

### `chown` - Change Ownership
Changes file owner.
```bash
sudo chown user:group filename.txt
```

## System Information

### `whoami` - Current User
Shows your username.
```bash
whoami
```

### `ps` - Running Processes
Lists running processes.
```bash
ps aux    # Show all processes
```

### `df` - Disk Space
Shows disk usage.
```bash
df -h     # Human-readable format
```

### `free` - Memory Usage
Displays memory information.
```bash
free -h   # Human-readable format
```

## Getting Help

### `man` - Manual Pages
Shows detailed help for commands.
```bash
man ls    # Show manual for 'ls' command
```

### `--help` Flag
Quick help for most commands.
```bash
ls --help
```

## Tips for Beginners

1. **Tab Completion**: Press Tab to auto-complete file/directory names
2. **Command History**: Use up/down arrows to navigate previous commands
3. **Clear Screen**: Type `clear` or press Ctrl+L
4. **Stop Command**: Press Ctrl+C to stop a running command
5. **Case Sensitive**: Linux is case-sensitive (`File.txt` ≠ `file.txt`)

## Practice Exercises

1. Create a directory called `practice`
2. Navigate into it and create a file called `test.txt`
3. Copy the file to `backup.txt`
4. List all files in the directory
5. Remove the original `test.txt` file

Remember: Always be careful with commands like `rm`, especially with the `-rf` flags!

Note: Claude generated content