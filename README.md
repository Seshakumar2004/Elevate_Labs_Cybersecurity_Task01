# Elevate_Labs_Cybersecurity_Task01

Output ScreenShot:
![Task 01](https://github.com/user-attachments/assets/04c3e26d-f1f3-4706-b287-07bcc19dd533)

Hints/Mini Guide:
. Install Nmap from the Official Website
Explanation: Nmap (Network Mapper) is a free and open-source utility for network discovery and security auditing. It's widely used by network administrators and security professionals for tasks like host discovery, port scanning, OS detection, and more.

How to Install:

Visit the Official Nmap Website: Go to https://nmap.org/download.html.
Choose Your Operating System:
Windows: Download the latest nmap-*-setup.exe installer. Run the executable and follow the on-screen instructions.
macOS: Download the latest nmap-*-macOS.dmg disk image. Open the DMG, then drag the Nmap application to your Applications folder. You might also consider installing it via Homebrew (brew install nmap).
Linux (Debian/Ubuntu): Open your terminal and run:
Bash

sudo apt update
sudo apt install nmap
Linux (CentOS/Fedora/RHEL): Open your terminal and run:
Bash

sudo yum install nmap  # For older systems
sudo dnf install nmap  # For newer systems
Verify Installation: After installation, open your command prompt (Windows) or terminal (macOS/Linux) and type:
Bash

nmap -v
You should see the Nmap version information, confirming it's installed correctly.
2. Find Your Local IP Range (e.g., 192.168.1.0/24)
Explanation: Your local IP range (also known as your local subnet or network address) defines the set of IP addresses that devices on your local network use to communicate with each other. Common private IP ranges include 192.168.1.0/24, 192.168.0.0/24, or 10.0.0.0/8. The /24 (or other number) is called a CIDR (Classless Inter-Domain Routing) suffix, which indicates the number of bits used for the network portion of the IP address, effectively defining the size of the network.

How to Find:

Windows:

Open Command Prompt by searching for cmd in the Start menu.
Type: ipconfig
Look for your "IPv4 Address" and "Subnet Mask" under your active network adapter (e.g., "Ethernet adapter" or "Wireless LAN adapter Wi-Fi").
Your local IP range will typically be your IPv4 address with the last octet replaced by 0, and the subnet mask will help you determine the CIDR suffix (e.g., a subnet mask of 255.255.255.0 corresponds to /24).
Example: If your IPv4 is 192.168.1.100 and Subnet Mask is 255.255.255.0, your range is 192.168.1.0/24.

3. Run: nmap -sS 192.168.1.0/24 to Perform TCP SYN Scan
   
Explanation:

nmap: The command to invoke the Nmap utility.
-sS: This is the option for a TCP SYN scan, often referred to as a "stealth scan" or "half-open scan."
How it works: Instead of completing the full three-way TCP handshake (SYN, SYN-ACK, ACK), Nmap sends a SYN packet to the target port.
If the port is open, the target responds with a SYN-ACK packet. Nmap then immediately sends an RST (reset) packet, tearing down the connection before a full handshake is established. This makes it less likely to be logged by intrusion detection systems compared to a full TCP connect scan (-sT).
If the port is closed, the target responds with an RST packet.
If no response is received, the port might be filtered (e.g., by a firewall).
192.168.1.0/24: This is a placeholder for your actual local IP range that you found in step 2. This tells Nmap to scan all IP addresses within that subnet.
How to Run (after identifying your actual IP range):

Open your command prompt or terminal.
Replace 192.168.1.0/24 with your identified local IP range.
Execute the command:
Bash

nmap -sS [Your_Local_IP_Range_Here]
Example: If your range is 192.168.1.0/24, you'd type: nmap -sS 192.168.1.0/24
Important Note: Running network scans on networks you do not own or have explicit permission to scan is illegal and unethical. Ensure you are only scanning your own local network.

4. Note Down IP Addresses and Open Ports Found
Explanation: After the Nmap scan completes, it will output a summary of the discovered hosts and their open ports. Nmap identifies open ports by analyzing the responses to its SYN packets. An "open" port means that an application or service is listening on that port and is ready to accept connections.

How to Interpret the Output:

The output will typically look something like this (this is a simplified example):


Starting Nmap 7.92 ( https://nmap.org ) at 2025-06-23 15:24 IST
Nmap scan report for 192.168.1.1
Host is up (0.0023s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
3389/tcp open  ms-wbt-server

Nmap scan report for 192.168.1.105
Host is up (0.005s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp

Nmap scan report for 192.168.1.120
Host is up (0.003s latency).
All 1000 scanned ports on 192.168.1.120 are closed.

Nmap done: 256 IP addresses (3 hosts up) scanned in 5.67 seconds


What to Note Down:

From the Nmap output, you should record the following for each "Host is up" entry:

IP Address: The IP address of the device (e.g., 192.168.1.1, 192.168.1.105).
Open Ports: For each IP address, list the PORT and SERVICE columns where the STATE is "open".

Example for 192.168.1.1:
IP: 192.168.1.1
Open Ports:
22/tcp (ssh)
80/tcp (http)
443/tcp (https)
3389/tcp (ms-wbt-server - Remote Desktop)
Example for 192.168.1.105:
IP: 192.168.1.105
Open Ports:
21/tcp (ftp)

This information provides a snapshot of which devices are active on your network and what services they are running that are exposed over the network. This is fundamental for network troubleshooting, security auditing, and understanding your network's landscape.
