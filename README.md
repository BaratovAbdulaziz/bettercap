# Install Bettercap
<h1>
  # Step 1.1: Install dependencies
sudo apt update
sudo apt install build-essential libpcap-dev libusb-1.0-0-dev pkg-config git ruby-dev libnetfilter-queue-dev golang -y

# Step 1.2: Clone the Bettercap repository
cd ~
git clone https://github.com/bettercap/bettercap.git

# Step 1.3: Build and install
cd bettercap
make build
sudo make install

</h1>
