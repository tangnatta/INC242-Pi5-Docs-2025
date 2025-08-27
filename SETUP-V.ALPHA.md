# Set up Raspberry Pi 5

- [ ] Raspberry Pi 5
- [ ] MicroSD card (16GB or larger)
- [ ] Power supply
- [ ] MicroSD card reader

## Step-by-step guide

0. Load [Raspberrypi Imager](https://www.raspberrypi.com/software/) and install it on your computer
1. Insert MicroSD card into card reader and connect to computer
2. Open Raspberry Pi Imager
3. Select Raspberry Pi Device as Raspberry Pi 5
4. Select OS as Ubuntu Server 24.04.3 LTS (64-bit) [Other general-purpose OS -> Ubuntu -> Ubuntu Server 24.04.3 LTS (64-bit)]
5. Select your inserted sd card
6. Click "Next"
7. On the popup window, click edit config
   - On General tab
     - Set hostname
     - Set Username and Password (Note: Username and password will be used to connect to your Raspberry Pi 5)
     - Set WiFi SSID and Password (2.4 GHz recommended)
     - Set Local time and keyboard layout
   - On Service tab
     - Enable SSH (Using password authentication)
8. Click "Yes" untill you can write to the sd card
9. After it finished, eject the MicroSD card from your computer and insert it into the Raspberry Pi 5
10. Connect the power supply to the Raspberry Pi 5
11. Wait for the Raspberry Pi 5 to boot up (This may take a few minutes)
12. Find the IP address of your Raspberry Pi 5
    - You can find it from your router's connected devices list
    - Or use a network scanning tool like [Angry IP Scanner](https://angryip.org/) to scan your network for connected devices
13. Open terminal then type command to ssh to raspberry pi 5 `ssh username@ip_address` (replace `username` with the username you set earlier and `ip_address` with the IP address of your Raspberry Pi 5)
14. If prompted, type "yes" to continue connecting
15. Enter the password you set earlier when prompted
16. After successfully logged in to your Raspberry Pi 5, start updating and upgrading the raspberry pi by running the following commands:
    ```
    sudo apt update -y
    sudo apt upgrade -y
    ```
17. You can now use your Raspberry Pi 5 for your projects!

Reference:

- https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview
- https://www.cherryservers.com/blog/install-gui-on-ubuntu-server
- https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-20-04
