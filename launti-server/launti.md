# Minetest server on Raspberry Pi — Step-by-step guide

> Purpose: manual (non-systemd) instructions to install and run a Minetest (Luanti) server on a Raspberry Pi. Copy‑paste commands and follow the order.

---

## Prerequisites

* A Raspberry Pi with an account that has `sudo` privileges (we'll use the currently-logged-in user).
* Internet access on the Pi.
* If you want friends from outside your LAN to join, you need access to your router to set up port forwarding (UDP 30000).

---

## 0. Notes about user & paths

* The original commands use `/home/pi/...`. If your Pi account is **not** `pi` (for example your prompt is `mk@...`), replace `pi` with your username or use `~` / `$USER`.
* To use the currently-logged-in user in commands, use `$USER` or `$(whoami)`.

Examples:

```bash
# If you are user mk, prefer:
/home/mk/minetest_world
# or use a variable that adapts automatically:
/home/$USER/minetest_world
# or simply:
~/minetest_world
```

---

## 1. Update the system

```bash
sudo apt update
sudo apt upgrade -y
```

---

## 2. Install Minetest (headless server)

```bash
sudo apt install minetest-server -y
```

> This installs a headless Minetest server package (no GUI). On some distributions the server binary may be `minetestserver` or located under `/usr/lib/minetest/minetestserver`.

Check the binary path:

```bash
command -v minetestserver || command -v minetest
```

---

## 3. Create a world directory (adjust username as needed)

```bash
# recommended (uses current user automatically):
mkdir -p /home/$USER/minetest_world
# ensure ownership (only needed if root created the folder earlier):
sudo chown -R $USER:$USER /home/$USER/minetest_world
```

If you still want `/home/pi/minetest_world` but your account is different, either use the `pi` account or replace `pi` with your username.

---

## 4. Start the server manually (recommended: set logfile into your home)

Run the server from the shell when you want it up. This example writes log to your home directory to avoid permission errors:

```bash
minetestserver --world /home/$USER/minetest_world --gameid minetest --port 30000 --logfile /home/$USER/minetest.log
```

### Common logging permission issue

If you see the error `Failed to open log file /var/log/minetest/minetest.log: Permission denied`, it means the server tried to write to `/var/log/minetest/`. Fix by either:

* specifying `--logfile /home/$USER/minetest.log` (recommended for manual runs), or
* creating the folder and changing owner:

```bash
sudo mkdir -p /var/log/minetest
sudo chown $USER:$USER /var/log/minetest
```

---

## 5. Run server in background (optional)

If you want the server to continue after closing the terminal:

**Using `nohup`**

```bash
nohup minetestserver --world /home/$USER/minetest_world --gameid minetest --port 30000 --logfile /home/$USER/minetest.log &
```

* Output will be appended to `nohup.out` unless `--logfile` is used.

**Using `tmux` or `screen`** (recommended if you want to reattach later)

```bash
sudo apt install tmux -y    # if tmux not installed
tmux new -s minetest
# inside tmux session run the same minetestserver command
# detach with Ctrl-B then D, reattach with `tmux attach -t minetest`
```

To stop the server:

```bash
pkill minetestserver
# or find PID and kill
ps aux | grep minetestserver
kill <PID>
```

---

## 6. Verify server is listening on UDP port 30000

```bash
sudo ss -ulnp | grep 30000
```

If nothing is returned, the server is not running or listening on a different interface/port.

---

## 7. Find your Pi's IP address (give this to friends)

```bash
hostname -I
# or show public IP (for friends outside your LAN):
curl ifconfig.me
```

* For friends on the **same LAN**, share the private IP (e.g. `10.168.0.100:30000`).
* For friends over the **Internet**, share your public IP or DDNS domain and ensure router port forwarding is configured (see next step).

---

## 8. Router: Port forwarding (for Internet players)

* Open your router admin UI and add a port-forward / virtual-server rule:

  * External port: `30000` (UDP)
  * Internal port: `30000` (UDP)
  * Internal IP: the Pi's LAN IP (e.g. `10.168.0.100`)
* Save and apply. Test from outside your network (ask a friend to connect using your public IP).

Tip: use a Dynamic DNS service (DuckDNS / No-IP) if your public IP changes.

---

## 9. How friends connect (client side)

In Minetest/Luanti client → Multiplayer → Join:

* **Address**: `10.168.0.100` (LAN) or `your.public.ip` / `your.ddns.domain` (Internet)
* **Port**: `30000`
* **Name**: their player name
* **Password**: (if your server requires one)

---

## 10. View who joined — logs & auth DB

**Realtime:**

```bash
# live server logs (if you started server directly you'll see logs in the terminal)
# if you used a logfile, tail it:
tail -f /home/$USER/minetest.log
# if you used systemd service earlier, use:
journalctl -u minetest-server -f
```

**Registered users (auth DB)**
World auth DB is usually an sqlite file under the worlds folder. Example path:

```
/var/games/minetest/worlds/<world_name>/auth.sqlite
```

List players stored in DB:

```bash
sqlite3 /var/games/minetest/worlds/<world_name>/auth.sqlite "SELECT name FROM auth;"
```

---

## 11. Quick troubleshooting

* `Permission denied` writing `/var/log/minetest/*` → use `--logfile` to home or change owner of `/var/log/minetest`.
* `command not found` for `minetestserver` → ensure `minetest-server` package installed and check `command -v minetestserver`.
* Server crashes on start → check `--logfile` output or terminal error for missing gameid, missing world, or other errors.

---

## 12. Handy start/stop scripts (place in your world folder)

**start.sh**

```bash
#!/usr/bin/env bash
set -e
WORLD_DIR="/home/$USER/minetest_world"
LOGFILE="/home/$USER/minetest.log"
minetestserver --world "$WORLD_DIR" --gameid minetest --port 30000 --logfile "$LOGFILE"
```

**start_bg.sh** (background)

```bash
#!/usr/bin/env bash
WORLD_DIR="/home/$USER/minetest_world"
LOGFILE="/home/$USER/minetest.log"
nohup minetestserver --world "$WORLD_DIR" --gameid minetest --port 30000 --logfile "$LOGFILE" > /dev/null 2>&1 &
```

**stop.sh**

```bash
#!/usr/bin/env bash
pkill minetestserver || echo "minetestserver not running"
```

Make them executable:

```bash
chmod +x start.sh start_bg.sh stop.sh
```

---

## 13. Backup world (recommended)

```bash
# stop server first if running
pkill minetestserver || true
# create backup tarball
tar -czvf ~/minetest_world_backup_$(date +%F).tar.gz /home/$USER/minetest_world
# start server again if you want
nohup minetestserver --world /home/$USER/minetest_world --gameid minetest --port 30000 --logfile /home/$USER/minetest.log &
```

---

## 14. Summary — the exact commands you provided (adapted)

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install minetest-server -y
mkdir -p /home/$USER/minetest_world
# if needed (fix ownership):
sudo chown -R $USER:$USER /home/$USER/minetest_world
cd /home/$USER/minetest
minetestserver --world /home/$USER/minetest_world --gameid minetest --port 30000 --logfile /home/$USER/minetest.log
```

---

If you'd like, I can:

* generate the `start.sh` / `stop.sh` files for you and put them in your world folder, or
* convert this `.md` into a downloadable file, or
* produce a `systemd` unit (if you later decide to auto-start).

Tell me which one and I'll create it for you.
