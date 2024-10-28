# SSH from other Network Connections (Forward Port)

To set up port forwarding from your Ethernet network to your Wi-Fi network on a Windows computer and allow access to
your Raspberry Pi from Computer2 via Computer1, you'll need to configure Windows' built-in routing and remote access
capabilities. Here's a step-by-step guide to achieve this:

---

## Step 1: Enable IP Routing on Computer1

First, you need to enable IP routing on Computer1 to allow traffic to pass between its network interfaces:

1. Open the Registry Editor by pressing Win + R, typing "regedit", and pressing Enter.
2. Navigate to HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
3. Right-click in the right pane, select New > DWORD (32-bit) Value, and name it "IPEnableRouter"
4. Double-click the new value, set it to 1, and click OK.
5. Restart your computer for the changes to take effect.

## Step 2: Configure Port Forwarding on Computer1

Now, you need to set up port forwarding using the Windows Firewall:

1. Press the Windows key and type "Windows Defender Firewall with Advanced Security"3.
2. Click on "Inbound Rules" in the left panel3.
3. Click "New Rule" in the right panel3.
4. Select "Port" and click Next3.
5. Choose "TCP" and enter "2000" as the specific local port, then click Next3.
6. Select "Allow the connection" and click Next3.
7. Apply the rule to all profiles (Domain, Private, and Public) and click Next3.
8. Give the rule a name (e.g., "Raspberry Pi SSH Forwarding") and click Finish3.

## Step 3: Set Up Port Forwarding Using PowerShell

To forward the incoming traffic on port 2000 to your Raspberry Pi, use the following PowerShell commands:

1. Open PowerShell as Administrator.
2. Run the following command to add the port forwarding rule:

```powershell
netsh interface portproxy add v4tov4 listenport=2000 listenaddress=192.168.1.20 connectport=22 connectaddress=192.168.3.2
listenaddress=192.168.1.20 connectport=22 connectaddress=192.168.3.2
```

This command forwards traffic from Computer1's Wi-Fi IP (192.168.1.20) on port 2000 to the Raspberry Pi's IP (
192.168.3.2) on port 22 (SSH).

## Step 4: Configure SSH on Raspberry Pi

Ensure SSH is enabled on your Raspberry Pi:

1. On the Raspberry Pi, open a terminal and run:
   ```bash
   sudo raspi-config
   ```
2. Navigate to "Interfacing Options" > "SSH" and select "Enable".

## Step 5: Connect from Computer2

Now you can connect to your Raspberry Pi from Computer2 using the following SSH command:

```bash
ssh -p 2000 pi@192.168.1.20
```

Replace "pi" with your Raspberry Pi username if it's different.

## Additional Security Considerations

1. Change the default SSH port on your Raspberry Pi for enhanced security:

    - Edit the SSH configuration file:
       ```bash
       sudo nano /etc/ssh/sshd_config
       ```
    - Find the line #Port 22 and change it to Port 2222 (or any other unused port)
    - Restart the SSH service:
       ```bash
       sudo systemctl restart ssh
       ```

2. Update the port forwarding rule on Computer1 to reflect the new SSH port:
   ```bash
   netsh interface portproxy delete v4tov4 listenport=2000 listenaddress=192.168.1.20
   netsh interface portproxy add v4tov4 listenport=2000 listenaddress=192.168.1.20 connectport=2222 connectaddress=192.168.3.2
   ```
3. Set up key-based authentication instead of password authentication for increased security.
4. Regularly update your Raspberry Pi and Computer1 to ensure you have the latest security patches.

By following these steps, you should be able to connect to your Raspberry Pi from Computer2 via Computer1's Wi-Fi IP
address (192.168.1.20) on port 2000. This setup creates a bridge between your Ethernet and Wi-Fi networks, allowing
secure access to your Raspberry Pi from the Wi-Fi network.