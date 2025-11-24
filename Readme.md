# OPNSense Dynamic DNS for DirectAdmin

*"Why is a raven like a writing desk? Why is a static IP like a moving target? Both questions have answers that change with time!"*

## 🎩 Overview

This repository provides a Dynamic DNS (DDNS) solution that bridges OPNSense with DirectAdmin's API, allowing your domain records to dance along with your ever-changing IP address.

This script was cobbled together for personal use. It may require adjustments to fit your particular head... err, setup. Basic Bash knowledge will serve you better.

## 🍄 What's in the Box?

- **actions_daddns.conf** - The configuration file that determines how everything appears in OPNSense's Cron UI
- **directadmin_ddns.sh_MULTIDOMAINS** - Script for updating main domain only (subdomains use DNS ALIAS)
- **directadmin_ddns.sh_SUBDOMAINSONLY** - Script for updating specific subdomains with separate IPs

### 🎯 Choosing Your Script

This repository includes two different script options to match your DNS setup:

#### MULTIDOMAINS Version
Use `directadmin_ddns.sh_MULTIDOMAINS` if:
- You want to update **only the main domain** (e.g., `mydomain.com`)
- Your subdomains use **ALIAS records** pointing to the main domain
- All subdomains rely on the main domain's IP address
- You want a simpler setup with a single IP update

#### SUBDOMAINSONLY Version
Use `directadmin_ddns.sh_SUBDOMAINSONLY` if:
- You need to update **specific subdomains individually**
- Each subdomain has **its own separate IP address**
- You want granular control over which subdomains get updated

**Important:** Rename your chosen script to `directadmin_ddns.sh` (remove the `_MULTIDOMAINS` or `_SUBDOMAINSONLY` suffix) before use.

## 🐰 Installation

### Step 1: Place the Configuration File

Drop `actions_daddns.conf` into: `/usr/local/opnsense/service/conf/actions.d`

### Step 2: Position the Script

Choose either `directadmin_ddns.sh_MULTIDOMAINS` or `directadmin_ddns.sh_SUBDOMAINSONLY` based on your needs (see "Choosing Your Script" above), then rename it to `directadmin_ddns.sh`. The script can live anywhere you fancy, as long as you update the location in `actions_daddns.conf`

## ⚙️ Configuration

### Configure actions_daddns.conf

Within this file, you can adjust:
- **Message** - What appears in the UI
- **Description** - Additional details for the cron job
- **Script Location** - Where you've placed directadmin_ddns.sh
- **Parameters** - Ensure you have enough "%s" placeholders for all your subdomains

### Configure directadmin_ddns.sh

Update the following variables in your chosen script:

| Variable | Description |
|----------|-------------|
| `DOMAIN` | Your domain name (main domain for MULTIDOMAINS, base domain for SUBDOMAINSONLY) |
| `DIRECTADMIN` | DirectAdmin portal URL |
| `DIRECT_USER` | Your DirectAdmin username |
| `DIRECT_PW` | Your DirectAdmin password |

**Note:** If using the SUBDOMAINSONLY version, you'll also need to specify which subdomains to update within the script.

### Update DNS server used

This is prefered to make sure your DNS names update as quickly as possible.

Adjust the name of the DNS server (currently set to regional DNS) in your chosen script. The DNS server setting allows faster verification of DNS updates.

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
