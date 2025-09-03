#  A Guide to Visual Studio Code on Linux

This guide is written to help students easily install and use VS Code on Linux systems.

## Quick Installation Methods (Recommended)

### For Ubuntu/Debian

**Method : Download and Install (Easiest)**

1. Go to https://code.visualstudio.com/download
2. Click **Linux .deb (64-bit)** button
3. After download completes, open Terminal and type:

```bash
cd Downloads
sudo apt install ./code_*.deb
```

**Done!** VS Code will be installed and auto-update automatically.

## Opening VS Code

After installation, you can open VS Code in 3 ways:

1. **From Applications Menu**: Search for "Visual Studio Code"
2. **From Terminal**: Type `code`
3. **Open folder directly**: Type `code .` in the desired folder

## Basic Configuration

### Set VS Code as Default Text Editor

```bash
xdg-settings set default-text-editor code.desktop
```

### Change Theme (Optional)

1. Press `Ctrl + Shift + P`
2. Type `theme`
3. Select **Preferences: Color Theme**
4. Choose your preferred theme

## Common Issues and Solutions

### Issue: "Unable to watch for file changes"

**Symptom**: You see "Unable to watch for file changes in this large workspace"

**Solution**:
```bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### Issue: Cannot see Thai/Chinese characters

**Solution**:
1. Open VS Code Settings (`Ctrl + ,`)
2. Search for "font family"
3. Change to: `'Droid Sans Mono', 'Droid Sans Fallback'`

### Issue: Cannot delete files

**Solution**:
```bash
sudo apt install gvfs-bin
```

### Issue: Git not working

**Solution**:
```bash
sudo apt update
sudo apt install git
```

## Recommended Extensions for Students

Open Extensions panel (`Ctrl + Shift + X`) and search for these:

### Important Shortcuts
- `Ctrl + Shift + P` - Command Palette (search all commands)
- `Ctrl + P` - Quick file open
- `Ctrl + ~` - Open/close Terminal
- `Ctrl + /` - Comment/Uncomment lines
- `Alt + Shift + F` - Format code

### Opening Projects
```bash
# Open current folder
code .

# Open specific folder
code /path/to/your/project

# Open specific file
code myfile.py
```
