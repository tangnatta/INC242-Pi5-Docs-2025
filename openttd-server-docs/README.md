Since there is no official arm64 OpenTTD Server release or community build available for the latest version (v14.1), this documentation relies on our own prebuilt snap package compiled from source code using this [GitHub repository](https://github.com/tangnatta/openttd-server/).

Special thanks to previous community contributors who built earlier versions and shared them on [GitHub](https://github.com/zoltantamasvajda/openttd-server).

# Step by step Guide

0. Login to your Raspberry Pi 5 via SSH or VNC
1. Download our prebuilt snap package from the `assets` directory in this repository. You can use `wget` or `curl` command to download it directly to your Raspberry Pi 5.
   For example:
   ```
   wget https://raw.githubusercontent.com/tangnatta/INC242-Pi5-Docs-2025/refs/heads/main/openttd-server-docs/assets/openttd-server_14.1_arm64.snap
   ```
2. Install the snap package using the `snap` command:
   ```
   sudo snap install --dangerous openttd-server_14.1_arm64.snap
   ```
3. After installation, you can start the OpenTTD server using the following command:
   ```
   sudo snap start openttd-server
   ```
4. Connect to the OpenTTD server from your OpenTTD client on your computer using the IP address of your Raspberry Pi 5 and the default port (`3979`).

## FYI

- To stop the OpenTTD server, use the following command:
  ```
  sudo snap stop openttd-server
  ```
- To get the logs of the OpenTTD server, use the following command:
  ```
  sudo snap logs openttd-server -n='all'
  ```
