# SSH Auth via Nmap Checking

## Introduction

This script allows you to perform batch checks for SSH authentication via Nmap scanning within subnet. It is useful for checking the status of SSH authentication on multiple devices simultaneously.

## Requirements

linux
sudo apt-get install nmap

window 
Download and install nmap from https://nmap.org/download.html#windows

## Usage

Before running `nmapScanning_subnet.py`, please prepare a `subnet.txt` file containing IP subnet address. You may edit the `subnet.txt` directly in the folder.

**Example of subnet.txt:**

```txt
172.22.32.0/22
172.22.28.0/22


To run the script:

```bash
python nmapScanning_subnet.py

