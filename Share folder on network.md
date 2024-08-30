# Running a Python Script on Startup for Raspberry Pi

To share a folder on a network using a Raspberry Pi, you can set up a Samba server.
Samba is a software suite that allows for file and print services to SMB/CIFS clients,
enabling interoperability between Linux/Unix servers and Windows-based clients.
Here’s a step-by-step guide on how to set up a shared folder on your Raspberry Pi:
---

## Setting Up Samba on Raspberry Pi

1. Update Your Raspberry Pi:
    * Open a terminal and run the following commands to update your package list and upgrade all packages:
       ```bash
       sudo apt update
       sudo apt upgrade
       ```

2. Install Samba:
    * Install Samba and its common binaries by executing:
        ```bash
        sudo apt install samba samba-common-bin
        ```

3. Create a Shared Directory:
    * Choose or create a directory that you want to share.
      For example, to create a new directory named "shared" in your home directory, use:
       ```bash
       mkdir ~/shared
       ```
    * Ensure the directory has the correct permissions for sharing.

4. Configure Samba:
    * Edit the Samba configuration file to add your shared directory:
   ```bash
   sudo nano /etc/samba/smb.conf
   ```
    * Add the following configuration at the end of the file:
   ```text
   [shared]
   Comment = Raspberry Pi Shared Folder
   Path = /home/pi/shared
   Browseable = yes
   Writeable = yes
   only guest = no
   create mask = 0777
   directory mask = 0777
   Public = yes
   Guest ok = yes
   ```
    * Save and exit the editor (usually CTRL + X, then Y, and Enter).

5. Set Up a Samba User:
    * Add a Samba user and set a password (this can be the same as your Raspberry Pi user):
   ```bash
   sudo smbpasswd -a pi
   ```

6. Restart Samba:
    * Restart the Samba service to apply the changes:
   ```bash
   sudo systemctl restart smbd
   ```
* get hostname:
    ```bash
   hostname -I
   ```

---

## Accessing the Shared Folder

* From Windows:
    * Open File Explorer, click on "This PC," and then "Map network drive."
    * Enter the path to your Raspberry Pi, e.g., \\raspberrypi\shared or use the IP address like \\192.168.x.x\shared.
    * Enter the Samba username and password when prompted.

* From Linux:
    * Use a file manager to connect to the server using the network path or mount the share using the command line.

This setup will allow you to share files between your Raspberry Pi and other devices on your network.
Note that this configuration is suitable for a local network and may not be secure for use over
the internet without additional security measures