# A Guide to Visual Studio Code on Linux

This guide provides comprehensive instructions for installing, updating, and configuring Visual Studio Code on various Linux distributions, along with solutions to common issues.

## 1. Installation

VS Code can be installed on most major Linux distributions using several methods.

### Debian and Ubuntu based distributions

The easiest method is to download and install the `.deb` package (64-bit).

#### 1. Using the .deb package (Recommended)

Install the package via the command line:

```bash
sudo apt install ./<file>.deb
```

**Note for older distributions:** You may need to run these commands instead:

```bash
sudo dpkg -i <file>.deb
sudo apt-get install -f # Install dependencies
```

Installing the .deb package will automatically add the apt repository and signing key to enable auto-updating through the system's package manager.

#### 2. Manual Repository Installation

To install the repository and key manually, follow these steps:

1. Download and install the Microsoft GPG key:
```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
```

2. Update the package cache and install VS Code:
```bash
sudo apt update
sudo apt install code
```

### RHEL, Fedora, and CentOS based distributions

For these distributions, you can use the yum repository.

1. Run the following script to install the key and repository:
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

2. Update the package cache and install the package:
   - **For Fedora 22 and above:**
   ```bash
   sudo dnf check-update
   sudo dnf install code
   ```
   - **For older versions using yum:**
   ```bash
   sudo yum check-update
   sudo yum install code
   ```

### openSUSE and SLE-based distributions

The same yum repository works for these systems.

1. Install the key and repository:
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
```

2. Update the package cache and install:
```bash
sudo zypper refresh
sudo zypper install code
```

### Snap Package

VS Code is officially distributed as a Snap package in the Snap Store.

- **To install:**
```bash
sudo snap install --classic code
```

- Once installed, the Snap daemon handles automatic updates in the background.
- If snap is not available on your distribution, refer to the [Installing snapd guide](https://snapcraft.io/docs/installing-snapd).

### Other Distributions

- **Arch Linux:** A community-maintained Arch User Repository (AUR) package is available. Consult the [Arch Wiki](https://wiki.archlinux.org/title/Visual_Studio_Code) for installation details.
- **NixOS:** A community-maintained Nix package exists in the nixpkgs repository. To install, set `allowUnfree` to `true` in `config.nix` and run:
```bash
nix-env -i vscode
```

### Manual Installation (.rpm)

You can manually download and install the .rpm package (64-bit), but auto-updating will not work unless you also install the repository.

```bash
sudo dnf install <file>.rpm
```

## 2. Updates

VS Code releases updates monthly.

- If you installed using a repository (`.deb` or `.rpm`), your system's package manager will handle auto-updates.
- For Snap packages, updates are automatic and run in the background.

**Note:** Due to the manual signing process, the apt and yum repositories might lag behind a new release by up to three hours.

## 3. Configuration

### Set as Default Text Editor

- **For xdg-open:**
```bash
xdg-settings set default-text-editor code.desktop
```

- **For Debian-based systems:** Use the alternatives system to set the default editor.
```bash
sudo update-alternatives --set editor /usr/bin/code
```

- If VS Code is not in the list, you must first register it:
```bash
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/code 10
```

### Title Bar Style

On Linux, the custom title bar is not enabled by default because it may look foreign across different desktop environments. However, it is recommended for accessibility improvements.

You can manually change this setting via **Window: Title Bar Style** (`window.titleBarStyle`) to either `custom` or `native`.

## 4. Alternative: Windows Subsystem for Linux (WSL)

For developers on Windows, you can use the Windows Subsystem for Linux (WSL) to install and run Linux distributions. When combined with the WSL extension in VS Code, you get a full editing and debugging experience within the context of your Linux distro.

## 5. Common Questions and Troubleshooting

### Error deleting files on Debian

This may be due to a missing trash implementation. Fix it with:
```bash
sudo apt install gvfs-bin
```

### "Unable to watch for file changes in this large workspace" (ENOSPC)

This means the file watcher has run out of handles.

1. First, try adding large, unnecessary folders (like Python's `.venv`) to the `files.watcherExclude` setting in your VS Code settings.

2. If that doesn't work, you can increase the system limit. Check the current limit:
```bash
cat /proc/sys/fs/inotify/max_user_watches
```

3. Increase the limit by adding the following line to `/etc/sysctl.conf`:
```
fs.inotify.max_user_watches=524288
```

4. Apply the change by running:
```bash
sudo sysctl -p
```
**(Note: Arch-based distros require a different method)**

### Cannot see Chinese characters in Ubuntu

In VS Code settings, find **Text Editor > Font** and set "Font Family" to `Droid Sans Mono, Droid Sans Fallback`.

### Package git is not installed error

This is typically caused by outdated package lists. Run an update and try again:
```bash
sudo apt update
```

### Window resize/move issues with X forwarding

If using X forwarding, switch to the native title bar by setting `window.titleBarStyle` to `native`.

### Repository changed its 'Origin' value

If you see this error during an update, use `apt` instead of `apt-get`, as it will prompt you to accept the change:
```bash
sudo apt update
```
