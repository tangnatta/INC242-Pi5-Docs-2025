
# A Guide to Visual Studio Code Remote - SSH

The **Visual Studio Code Remote - SSH** extension allows you to open a folder on any remote machine, virtual machine, or container with a running SSH server and take full advantage of VS Code's feature set. Once connected, you can interact with files and folders anywhere on the remote filesystem.

A key advantage is that **no source code needs to be on your local machine** to gain these benefits, as the extension runs commands and other extensions directly on the remote machine. This setup provides a **local-quality development experience**, including full IntelliSense, code navigation, and debugging, **regardless of where your code is hosted**.

## 1. Prerequisites

### 1.1 System Requirements

**Local Machine (Your computer):**
*   A supported OpenSSH compatible SSH client must be installed.

**Remote Host (The server):**
*   A running SSH server on one of the following operating systems:
    *   x86_64: Debian 8+, Ubuntu 16.04+, CentOS / RHEL 7+
    *   ARMv7l (32-bit): Raspberry Pi OS (formerly Raspbian) Stretch/9+
    *   ARMv8l (64-bit): Ubuntu 18.04+
    *   Windows: Windows 10 / Server 2016/2019 (version 1803+) using the official OpenSSH Server
    *   macOS: macOS 10.14+ (Mojave) with Remote Login enabled
*   **A minimum of 1 GB RAM is required**, but at least **2 GB RAM and a 2-core CPU is recommended** for the best performance.

### 1.2 Installation

To get started, you need to perform the following steps:

1.  **Install an SSH Client:** If you don't already have one, [install an OpenSSH.](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client)
2.  **Install VS Code:** [Install Visual Studio Code](https://code.visualstudio.com/)
3.  **Install the Extension:** Install the [**Remote - SSH**](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) extension. It is also recommended to install the **Remote Development** extension pack if you plan to use other remote capabilities, as it includes all necessary extensions.

## 2. Connecting to the Server

1.  **Verify SSH Connection:** First, open a terminal (or PowerShell on Windows) and confirm you can connect to your remote host using the standard SSH command:
    ```bash
    ssh user@hostname
    ```
2.  **Connect from VS Code:**
    *   In VS Code, open the Command Palette using `F1` (or `Ctrl+Shift+P`).
    *   Type and select the command **Remote-SSH: Connect to Host...**.
    *   Enter your connection information in the same `user@hostname` format.
3.  **Select Server OS:** If VS Code cannot automatically detect the operating system of the remote server, it will prompt you to select the platform (Linux, Windows, or macOS) manually.
4.  **Wait for Setup:** VS Code will then connect and automatically set itself up on the remote host. You can monitor the progress in the `Remote - SSH` output channel.
5.  **Check Connection Status:** Once the connection is successful, you will see the name of the remote host in the Status bar at the bottom-left corner of the window.

> **Recommendation:** While password authentication is supported, it is highly recommended to set up **key-based authentication** for better convenience and security.

## 3. Basic Usage

### 3.1 Opening a Folder

After connecting, you will be in an empty window. You can open any folder or workspace on the remote machine just as you would locally by navigating to **File > Open...** or **File > Open Workspace...**.

### 3.2 Using the Terminal

Once you are connected to a remote host, **any terminal window you open in VS Code (`Terminal > New Terminal`) will automatically run on the remote host**, not your local machine.

### 3.3 Managing Extensions

VS Code manages extensions in two locations: locally for UI-related extensions (like themes) and remotely on the SSH host for most other extensions. When you install an extension from the Extensions view, it will automatically be installed in the correct location. You can see where each extension is installed, as they will be grouped into categories like **Local - Installed** and a category for your specific SSH host.

## 4. Advanced Features

### 4.1 Debugging

You can use VS Code's debugger on the remote host just as you would locally. Simply configure your `launch.json` file, and press `F5` to start debugging. The application will launch on the remote host, and the debugger will attach to it automatically.

### 4.2 Port Forwarding (SSH Tunneling)

If you need to access a port on the remote machine that isn't publicly available (e.g., a web server running on `localhost:3000`), you can forward it to your local machine.

1.  Open the Command Palette (`F1`) and select the **Forward a Port** command.
2.  Enter the port number on the remote machine you wish to forward.
3.  A notification will inform you which local port has been mapped to the remote port (e.g., `localhost:4123`). You can use this local address to access the service.
4.  You can view all active forwarded ports in the **Ports view** or the **Remote Explorer**.

## 5. Disconnecting

When you are finished, you can close the connection by selecting **File > Close Remote Connection** from the menu or by simply exiting VS Code.

```
