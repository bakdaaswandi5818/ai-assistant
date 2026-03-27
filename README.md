# ai-assistant
zero-claw

## Linux VPS Installation Guide

This guide walks you through installing and running **ZeroClaw** on a Linux VPS.

### Prerequisites

- A Linux VPS (Ubuntu 20.04 / 22.04 recommended)
- Root or sudo access
- Git installed

### Step 1 — Update your system

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2 — Install Node.js (v18 or later)

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
node -v   # verify installation
npm -v    # verify npm
```

### Step 3 — Install Git

```bash
sudo apt install -y git
git --version   # verify installation
```

### Step 4 — Clone the repository

```bash
git clone https://github.com/bakdaaswandi5818/ai-assistant.git
cd ai-assistant
```

### Step 5 — Install dependencies

```bash
npm install
```

### Step 6 — Configure the application

Copy the example environment file and fill in your credentials:

```bash
cp .env.example .env
nano .env
```

Set the required values (API keys, tokens, etc.) inside `.env`.

### Step 7 — Start ZeroClaw

```bash
npm start
```

To keep the bot running after you close the SSH session, use **PM2**:

```bash
# Install PM2 globally
sudo npm install -g pm2

# Start the application with PM2
pm2 start npm --name "zeroclaw" -- start

# Save the process list and enable auto-start on reboot
pm2 save
pm2 startup
```

Follow the command that `pm2 startup` prints to enable autostart.

### Step 8 — Useful PM2 commands

| Command | Description |
|---|---|
| `pm2 status` | Show running processes |
| `pm2 logs zeroclaw` | View live logs |
| `pm2 restart zeroclaw` | Restart the application |
| `pm2 stop zeroclaw` | Stop the application |

### Updating ZeroClaw

```bash
cd ai-assistant
git pull
npm install
pm2 restart zeroclaw
```

### Troubleshooting

- **Port already in use** — Change the `PORT` value in your `.env` file.
- **Permission denied** — Run the command with `sudo` or fix directory ownership: `sudo chown -R $USER:$USER ~/ai-assistant`.
- **Node.js version too old** — Re-run Step 2 to install a newer version.
