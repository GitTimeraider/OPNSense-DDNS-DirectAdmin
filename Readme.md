# OPNSense Dynamic DNS for DirectAdmin

*"Why is a raven like a writing desk? Why is a static IP like a moving target? Both questions have answers that change with time!"*

## 🎩 Overview

This repository provides a Dynamic DNS (DDNS) solution that bridges OPNSense with DirectAdmin's API, allowing your domain records to dance along with your ever-changing IP address.

This script was cobbled together for personal use. It may require adjustments to fit your particular head... err, setup. Basic Bash knowledge will serve you better.

## 🍄 What's in the Box?

- **actions_daddns.conf** - The configuration file that determines how everything appears in OPNSense's Cron UI
- **directadmin_ddns.sh** - The main script that performs the DNS update magic

## 🐰 Installation

### Step 1: Place the Configuration File

Drop `actions_daddns.conf` into: `/usr/local/opnsense/service/conf/actions.d`

### Step 2: Position the Script

The `directadmin_ddns.sh` script can live anywhere you fancy, as long as you update the location in `actions_daddns.conf`

## ⚙️ Configuration

### Configure actions_daddns.conf

Within this file, you can adjust:
- **Message** - What appears in the UI
- **Description** - Additional details for the cron job
- **Script Location** - Where you've placed directadmin_ddns.sh
- **Parameters** - Ensure you have enough "%s" placeholders for all your subdomains

### Configure directadmin_ddns.sh

Update the following variables in the script:

| Variable | Description |
|----------|-------------|
| `DOMAIN` | Your domain name |
| `DIRECTADMIN` | DirectAdmin portal URL |
| `DIRECT_USER` | Your DirectAdmin username |
| `DIRECT_PW` | Your DirectAdmin password |
| `CONFIGURED_IP` | DNS server URL for IP checks (currently set to regional DNS) |

## 🎪 Usage

Once configured, navigate to:
**OPNSense → System → Settings → Cron**

You'll find your DDNS update job ready to run at your chosen intervals!

## ⚠️ Mad Warnings

- This script lacks some features you might expect
- It may include additions some find undesirable
- Regional DNS is currently configured - adjust to your domain host's DNS for faster checks

## 🫖 Contributing

Feel free to modify this script to suit your needs.
