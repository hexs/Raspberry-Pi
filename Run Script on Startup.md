# Running a Python Script on Startup for Raspberry Pi

To run a Python script automatically on startup for a Raspberry Pi, you can use several methods. Here are three common
approaches:
---

## Method 1: Using `crontab`

`crontab` is a time-based job scheduler in Unix-like operating systems. You can use it to schedule scripts to run at
startup.

1. Open the terminal on your Raspberry Pi.
2. Edit the `crontab` file with the command:
   ```bash
   crontab -e
   ```
3. If prompted, choose an editor (nano is a simple choice).
4. Add the following line to the file to run your script at boot:
   ```bash
   @reboot python3 /path/to/your/script.py
   ```
   Replace /path/to/your/script.py with the full path to your Python script.

5. Save and exit the editor. The script will now run at every reboot.

---

## Method 2: Using `systemd`

`systemd` is a system and service manager for Linux operating systems. It can be used to create a service that runs your
script at startup.

1. Create a new service file:
   ```bash
   sudo nano /etc/systemd/system/myscript.service
   ```
2. Add the following content to the file:
   ```text
   [Unit]
   Description=My Python Script
   After=network.target

   [Service]
   ExecStart=/usr/bin/python3 /path/to/your/script.py
   Restart=always
   User=pi

   [Install]
   WantedBy=multi-user.target
   ```
   Ensure the ExecStart path points to your Python script.
3. Save and close the file.
4. Enable the service to run at startup:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable myscript.service
   ```
5. Start the service immediately if desired:
   ```bash
   sudo systemctl start myscript.service
   ```
6. Check the status of the service to ensure it is running:
   ```bash
   sudo systemctl status myscript.service
   ```
   The script will now run at every boot.

---

## Method 3: Using `rc.local`

The `rc.local` file can be used to execute scripts at the end of the multi-user runlevel.

1. Open the rc.local file for editing:
   ```bash
   sudo nano /etc/rc.local
   ```
2. Add your command above the `exit 0` line:
   ```bash
   python3 /path/to/your/script.py &
   ```
   The ampersand (&) allows the script to run in the background.
3. Ensure the rc.local file is executable:
   ```bash
   sudo chmod +x /etc/rc.local
   ```
4. Reboot the Raspberry Pi to test:
   ```bash
   sudo reboot
   ```
   The script should now run at startup.

## Method 4: Using `Desktop Entry`

1. Create your Python script and test it to ensure it works correctly.
2. Create a .desktop file in the autostart directory:
   ```bash
   mkdir -p /home/pi/.config/autostart
   ```
   ```bash
   nano /home/pi/.config/autostart/script1.desktop
   ```
3. Add the following content to the .desktop file:
   ```text
   [Desktop Entry]
   Type=Application
   Name=script1
   Exec=lxterminal -e 'bash -c "cd /home/pi/<project> && /home/pi/<project>/.venv/bin/python main.py"'
   ```
   Replace "script1" with a descriptive name
   and adjust the path to your script accordingly
4. Save`ctrl + s` and exit`ctrl + x` the text editor.
5. Make the .desktop file executable:
   ```bash
   chmod +x /home/pi/.config/autostart/script1.desktop
   ```

Each method has its own advantages. crontab is simple and effective for most use cases, systemd offers more control and
logging, and rc.local is straightforward for quick setups. Choose the method that best suits your needs.