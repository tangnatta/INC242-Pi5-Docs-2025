# Install and Connect VNC on Raspberry Pi 5 (PI OS)

# Requirements

- [ ] Raspberry Pi 5 with Raspberry Pi OS installed
- [ ] Computer or laptop

## Step-by-step guide

0. Install [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/?lai_vid=63RrdyrWvfXz&lai_sr=0-4&lai_sl=l) on your computer or laptop
1. Open terminal on your Raspberry Pi 5
2. Enable VNC server
   ````
   sudo raspi-config
   ``` -> Select 3 Interface Options -> I3 VNC -> The continue to enable VNC
   ````
3. Try to connect to the Raspberry Pi 5 using VNC Viewer on your computer.
   - Open VNC Viewer
   - Click on the search bar and type in the IP address of your Raspberry Pi 5 or Hostname
   - Press Enter
   - Type your username and password when prompted
4. You should now be connected to your Raspberry Pi 5 desktop environment via VNC!

Note1: If you encounter any issues, make sure that the VNC server is running on your Raspberry Pi 5 and that you are using the correct IP address or hostname.