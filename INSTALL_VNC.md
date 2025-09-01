# Install and Connect VNC on Raspberry Pi 5 (PI OS)

# Requirements

- [ ] Raspberry Pi 5 with Raspberry Pi OS installed
- [ ] Computer or laptop

## Step-by-step guide

0. Install [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/?lai_vid=63RrdyrWvfXz&lai_sr=0-4&lai_sl=l) on your computer or laptop
1. Open terminal on your Raspberry Pi 5
2. Enable VNC server
   ```
   sudo raspi-config
   ``` 

   1. Select `3 Interface Options`
   2. Select `I3 VNC`
   3. Select `Yes` to enable VNC
   4. Select `OK` to confirm
   5. Select `Finish` to exit the configuration tool

3. Try to connect to the Raspberry Pi 5 using VNC Viewer on your computer.
   1. Open VNC Viewer
   2. Click on the search bar and type in the IP address of your Raspberry Pi 5 or Hostname
   3. Press Enter
   4. Type your username and password when prompted
4. You should now be connected to your Raspberry Pi 5 desktop environment via VNC!

Note 1: If you encounter any issues, make sure that the VNC server is running on your Raspberry Pi 5 and that you are using the correct IP address or hostname.