Since there is no official arm64 OpenTTD Server release or community build available for the latest version (v14.1), this documentation relies on our own prebuilt snap package compiled from source code using this [GitHub repository](https://github.com/tangnatta/openttd-server/).

Special thanks to previous community contributors who built earlier versions and shared them on [GitHub](https://github.com/zoltantamasvajda/openttd-server).

# Step by step Guide

0. Login to your Raspberry Pi 5 via SSH or VNC
1. Install snap and snapd if not already installed:
   ```
   sudo apt update
   sudo apt install snapd
   sudo snap install snapd
   ```
2. Install options (choose one):

   - **Option A** — Install the community OpenTTD Server V14.1 snap from the edge channel (recommended):

     Thanks to the upstream repository merged a PR that provides an official edge snap build (see https://github.com/zoltantamasvajda/openttd-server/pull/6).

     ```
     sudo snap install openttd-server --edge
     ```

   - **Option B** — Install our prebuilt local snap pakage:

   1. Download the prebuilt snap package from the `assets` directory in this repository and install it locally. You can use `wget` or `curl` to download it directly to your Raspberry Pi 5.

      For example:

      ```
      wget https://raw.githubusercontent.com/tangnatta/INC242-Pi5-Docs-2025/refs/heads/main/openttd-server-docs/assets/openttd-server_14.1_arm64.snap
      ```

   2. Install the downloaded snap locally. Because this is a local package, you must use the `--dangerous` flag with `snap install`:

      ```
      sudo snap install --dangerous openttd-server_14.1_arm64.snap
      ```

3. After installation, start the OpenTTD server:

```
sudo snap start openttd-server
```

5. Connect to the OpenTTD server from your OpenTTD client on your computer using the IP address of your Raspberry Pi 5 and the default port (`3979`).

   **Caution**: Make sure your Raspberry Pi 5 and your computer are on the same local network.

## FYI

- To stop the OpenTTD server, use the following command:
  ```
  sudo snap stop openttd-server
  ```
- To get the logs of the OpenTTD server, use the following command:
  ```
  sudo snap logs openttd-server -n='all'
  ```
- To find your raspberry pi 5 IP address, you can use the following command:
  ```
  hostname -I
  ```
  Or
  ```
  ifconfig
  ```
  Or
  ```
  ip addr show
  ```
- To find opening ports on your raspberry pi 5, you can use the following command:
  ```
  sudo netstat -tulnp
  ```
