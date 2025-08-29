# Install VNC on Raspberry Pi 5 (Ubuntu LTS)

- [ ] Raspberry Pi 5 with ubuntu desktop installed
- [ ] Computer with VNC Viewer installed

## Step-by-step guide

0. Install [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/?lai_vid=63RrdyrWvfXz&lai_sr=0-4&lai_sl=l) on your computer
1. Open terminal on your Raspberry Pi 5
2. Type `wget https://downloads.realvnc.com/download/file/vnc.files/VNC-Server-7.15.0-Linux-ARM64.deb` in Terminal
3. Type `sudo dpkg -i VNC-Server-7.15.0-Linux-ARM64.deb` in Terminal
4. Type

```
sudo systemctl enable vncserver-virtuald.service
sudo systemctl enable vncserver-x11-serviced.service
sudo systemctl start vncserver-virtuald.service
sudo systemctl start vncserver-x11-serviced.service
```
in terminal

5. Type `sudo reboot` in terminal
6. Open VNC Viewer on your computer and connect to the Raspberry Pi 5
7. Connect the Raspberry pi 5 using IP or hostname in VNC Viewer
8. Type your username and password when prompted.
9. You should now be connected to your Raspberry Pi 5 desktop environment via VNC!

Reference: 
- https://omar2cloud.github.io/rasp/realvnc/
