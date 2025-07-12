#!/bin/bash

# Exit immediately if any command fails
set -e  

# Ensure script is run as root
if [ "$EUID" -ne 0 ]; then
    echo "[ERROR] Please run as root or with sudo."
    exit 1
fi
echo "Updating package list..."
apt-get update -y > /dev/null

echo "Installing Apache..."
apt-get install apache2 -y > /dev/null

echo "Enabling Apache to start on boot..."
systemctl enable apache2 > /dev/null
systemctl start apache2 > /dev/null
systemctl status apache2 > /dev/null 2>&1

echo "Apache installation complete."
