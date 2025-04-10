```markdown
# **Discord Self-Bot with Blacklist Check & Auto-Ban**

## **Overview**

This project is a **Discord Self-Bot** designed to check if users are part of any blacklisted servers and optionally ban them from your own server if they're found. It's highly customizable and includes a command-based toggle to enable or disable the auto-ban feature.

> ⚠️ **Important:**  
> - **Self-bots are against Discord's Terms of Service.** Running this bot can result in your account being permanently banned.  
> - **Use at your own risk.**  
> - This bot uses `discord.js-selfbot-v13` to interface with Discord.

---

## **Features**

- `?#check @user`: Check if the mentioned user is in any blacklisted servers.
- `?#checkall`: Check all members of the current server (excluding bots).
- `?#bantoggle on / off`: Toggle the auto-ban function on or off.
- `?#blacklist add <server_id>`: Add a server to the blacklist.
- `?#blacklist remove <server_id>`: Remove a server from the blacklist.
- `?#blacklist list`: List all blacklisted servers.
- `?#ban @user`: Manually ban a user from the target server.
- Automatically bans blacklisted users if toggled on.

---

## **Setup**

### **1. Requirements**

- **Node.js** installed
- A **user token** from your Discord account (not a bot token)
- Access to servers you want to check against

### **2. Installation**

```bash
npm init -y
npm install discord.js-selfbot-v13
```

---

## **Configuration**

### **3. `servers.json`**

Create a `servers.json` file that lists the server IDs you want to track as "blacklisted".

```json
[
  "123456789012345678",
  "987654321098765432"
]
```

### **4. Set Your Token and Target Server**

In the main file, replace:

- `YOUR_TOKEN_HERE` with your Discord **user token**.
- `'TARGET_SERVER_ID'` with the server ID where users will be **banned** if found.

---

## **Usage**

Run the bot with:

```bash
node bot.js
```

Once it's running, use these commands in any server:

- `?#check @user` — Check a specific user.
- `?#checkall` — Check everyone in the current server (skips bots).
- `?#bantoggle on` — Turns **on** auto-ban after detecting blacklisted users.
- `?#bantoggle off` — Turns **off** auto-ban.
- `?#blacklist add <server_id>` — Add a server to the blacklist.
- `?#blacklist remove <server_id>` — Remove a server from the blacklist.
- `?#blacklist list` — List all blacklisted servers.
- `?#ban @user` — Manually ban a user from the target server.

### **Example Output:**
```
🔍 Checking: @user123 (user123) (123456789012345678)
⚠️ Found in 5 blacklisted server(s).
🚫 This user has been banned from the target server.
```

---

## **How to Purchase**

Want the full working code with support?

### 🔥 Price: **Up to 500 Robux**

1. **Contact Me**
   - Discord ID: `123456789012345678`
   - [Click to add on Discord](https://discordapp.com/users/123456789012345678)

2. **Payment via Robux**
   - You'll get full code + setup help after confirmation.

3. **Ongoing Support**
   - Troubleshooting and configuration assistance included after purchase.

---

## **Disclaimer**

- ❗ **Self-bots break Discord's TOS.** Use it only if you're aware of the risks.
- 💸 **No Refunds** after delivery.
- 💵 **Payment in Robux only** via **Roblox Payment Link**.

---

## **Robux Payment Instructions**

- Request a payment link directly from me on Discord.
- After successful payment, you will receive:
  - Complete source code
  - Setup help
  - Future updates (if any)
```
