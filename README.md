# xray-proxy-linux

## VLESS + REALITY + Linux TPROXY

This repository contains configuration files and settings for **VLESS + REALITY + Linux TPROXY**.

---

## Setup

To get started, open this repository in your favorite IDE and enter your values in the following variables:

### Required Variables

The variables are marked with comments in the configuration files:

- **JSON files**: Variables are marked using `//` comments.
- **nftables configuration**: Variables are marked using `#` comments.

#### Variables:

- **TPROXY Port (optional):**  
  `_DOKODEMO_TPROXY_PORT`

- **VLESS Server Address:**  
  `_VLESS_ADDRESS`

- **VLESS Port:**  
  `_VLESS_PORT`

- **VLESS User UUID:**  
  `_VLESS_USER_ID`

- **REALITY Server Name (SNI):**  
  `_REALITY_SERVER_NAME`

- **REALITY Public Key:**  
  `_REALITY_PUBLIC_KEY`

- **REALITY Short ID:**  
  `_REALITY_SHORT_ID`

---

## Prerequisites

Before proceeding with the installation, ensure that the following packages are installed:

For **Ubuntu/Debian**:

```bash
sudo apt update && sudo apt install -y nftables iproute2
```

For **CentOS/RHEL**:

```bash
sudo yum install -y nftables iproute
```

For **Arch Linux**:

```bash
sudo pacman -S nftables iproute2
```

Ensure that the `nftables` service is enabled and running:

```bash
sudo systemctl enable nftables
sudo systemctl start nftables
```

---

## Installing Xray Core

Download and install the latest Xray binary from the [xray-core repository](https://github.com/XTLS/Xray-core/releases):

```bash
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```

Verify the installation:

```bash
xray --version
```

---

## Installation Guide

### 1. Clone the Repository

```bash
git clone https://github.com/IXLShizua/xray-proxy-linux.git
cd xray-proxy-linux
```

### 2. Configure the Settings

Open the necessary files in a text editor and update the required variables.

### 3. Install Configuration Files

#### 3.1 Xray Configuration

Copy the Xray configuration file to the correct location:

```bash
mkdir -p /etc/xray
cp config.json /etc/xray/config.json
```

#### 3.2 Systemd Service File

Copy the systemd service file and enable it:

```bash
cp xray-proxy.service /etc/systemd/system/xray-proxy.service
systemctl daemon-reload
systemctl enable xray-proxy
```

#### 3.3 Routing and Firewall Rules

Ensure the nftables configuration is in place:

```bash
mkdir -p /etc/nftables
cp proxy.conf /etc/nftables/proxy.conf
```

---

### 4. Start the Service

```bash
systemctl start xray-proxy
```

### 5. Check the Service Status

```bash
systemctl status xray-proxy
```

---

## Contributing & Support

For any questions or improvements, feel free to open an issue or submit a pull request.

