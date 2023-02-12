

# SSH-into-your-Raspiblitz-over-TOR- [ old one bro ] we're already facing new stuff and, its  such a pain in literal `*ss`

This guide will instruct you on how to SSH into your Raspiblitz over TOR using an android device.



**Prerequisites:**
- TOR enabled on your Raspiblitz 
- Orbot android app
- An SSH android app (JuiceSSH or Termux)

----------------------------------------------

**Setup SSH Hidden Service**
1. Open the command line terminal on your raspiblitz
2. Open your torrc file
  ```
  sudoedit /etc/tor/torrc
  ```
3. Add the following lines to your torrc file  
  ```
  # SSH Hidden Service
  HiddenServiceDir /mnt/hdd/tor/sshd
  HiddenServiceVersion 3
  HiddenServicePort 22 127.0.0.1:22
  ```
4. Save torrc file and exit back to command line
5. Restart TOR
  ```
  sudo systemctl restart tor
  ```
6. Retrieve your SSH onion address
  ```
  sudo cat /mnt/hdd/tor/sshd/hostname
  ```

----------------------------------------------

**Connect Through Mobile Device**

For **JuiceSSH**
  1. Install and launch Orbot
  2. Enable 'VPN mode' and connect to TOR
  3. Install and launch your SSH app
  4. SSH into your raspiblitz

  In JuiceSSH: Add a new connection
  ```
   - Type: SSH
   - Address: youraddress.onion (from step 6)
   - Identity
      Username: admin
      Password: 'Your Raspiblitz Password A'
   - Port: 22
  ```
For **Termux**: Run the following commands
  1. Install necessary packages
  ```
  pkg install openssh tor proxychains-ng termux-services
  ```
  2. Restart Termux
  3. Enable tor service and SSH into your raspiblitz
  ```
  sv-enable tor
  proxychains4 ssh admin@youraddress.onion
  ```
  *Note: if you use Orbot VPN system-wide you need to deselect Termux.*
  
You should now be connected to your raspiblitz node!

