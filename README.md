Packet Tracer Step-by-Step
1) Start and place devices

Open Cisco Packet Tracer.

From the End Devices palette place:

1 Server

1 PC (wired)

1 Laptop (wireless-capable)

From Network Devices → Switches place:

1 Switch (e.g., 2960)

From Network Devices → Routers place:

1 Generic Router (e.g., 2911 or 1841)

From Network Devices → WAN place:

1 Cable Modem or use Cloud / Generic Device to represent the ISP/modem. (If Packet Tracer version lacks a cable modem, use a Cloud or a Router labelled “Modem/Internet”.)

2) Cable the devices

Use these cable types (Packet Tracer usually auto-selects the right cable if you click devices in order):

Cable Modem (or Cloud) → Router

If using a Cable Modem device, use Coaxial or Copper Straight-through depending on PT version.

Connect modem to router interface GigabitEthernet0/0 (or Fa0/0).

Router → Switch

Use Copper straight-through from router Gig0/1 (or Fa0/1) → Switch Fa0/1.

Switch → PC (wired)

Switch Fa0/2 → PC Fa0.

Switch → Server

Switch Fa0/3 → Server Fa0.

Wireless:

Place a Wireless Router or Access Point (if you want the laptop to connect wirelessly).

Connect the wireless router/AP to the same switch (AP Fa0 → Switch Fa0/x) using straight-through cable.

Or use the router’s built-in wireless if your router model supports it.

3) Basic device naming (optional but helpful)

Rename devices to match your file:

Router → Router1

Server → FTP-Server

PC → PC1

Laptop → Laptop1

Switch → Switch1

Modem/Cloud → CableModem

4) Configure the Router (LAN side + DHCP)

Open the router CLI and enter configuration mode. Example CLI commands:




Notes:

ip dhcp excluded-address keeps .1–.99 reserved (router & static servers).

DHCP will hand out addresses from 192.168.6.100 onward.

5) Configure the Server (static IP + FTP service)

Click the FTP-Server device → Desktop → IP Configuration:

IP Address: 192.168.6.214

Subnet Mask: 255.255.255.0

Default Gateway: 192.168.6.1

DNS: 8.8.8.8 (optional)

On the Server → Services tab:

Enable FTP service (switch it ON).

Create user:

Username: ftpUser

Password: ftpUser1234

Set the default folder (e.g., /FtpShared or use the server’s FTP file area).

You can also enable HTTP if you want to host a web page.

6) Configure PC (DHCP) and Laptop (wireless DHCP)

PC1 (Wired):

Click PC1 → Desktop → IP Configuration → select DHCP.

It should receive an IP like 192.168.6.100 and gateway 192.168.6.1.

Laptop1 (Wireless):

If using a Wireless Router/AP:

Click the AP → Wireless settings → set SSID (e.g., MyLabWiFi) and security (open or WPA2 with a password).

On Laptop → Desktop → PC Wireless → configure and connect to the SSID, choose DHCP for IP assignment.

Laptop should receive DHCP address from router (e.g., 192.168.6.101).

7) Check connectivity and tests

Ping the gateway from PC:

PC → Desktop → Command Prompt → ping 192.168.6.1 → should reply.

Ping the FTP Server:

ping 192.168.6.214 → should reply.

FTP Test (from PC or Laptop):

From PC → Desktop → Web Browser or Command Prompt use FTP:

Browser: ftp://192.168.6.214 — it should prompt credentials.

Or Command Prompt: ftp 192.168.6.214 then login ftpUser / ftpUser1234.

Check IPs assigned:

On PC: ipconfig (Desktop → IP Configuration or Command Prompt) to view DHCP IP.

On Router: show ip dhcp binding to see DHCP leases.

8) Wireless laptop specifics (if using Laptop wireless)

On the wireless router/AP interface set:

SSID: FtpLab

Security: None or WPA2-PSK (if you set a passphrase, use same on laptop)

On laptop → Desktop → PC Wireless → select SSID → Connect → DHCP

9) Extra: If you want the server’s folder to match your notes (FtpShared)

On Packet Tracer Server → Files → create a folder FtpShared or upload package.json or index.html as your lab file.

Ensure FTP service points to that folder (in Server services UI).

10) Troubleshooting checklist

If PC/Laptop did not receive DHCP: check router interface is no shutdown and DHCP pool is configured.

If ping fails: check cable types and port connections (Fa0/x).

If FTP login fails: confirm username/password and that FTP service is ON on the server.

Run show ip interface brief on router to verify interfaces are up and have IPs.
