# **Discord Self-Bot with User Info Logging and Ban Toggle**

## **Overview**

This project is a **Discord Self-Bot** built to log user information (roles, join date, user ID, etc.) from multiple servers and optionally ban users from a specific server after logging their information.

### **Important:**
- **Self-bots are against Discord's Terms of Service (TOS).** Using this bot can result in your Discord account being permanently banned. **Use at your own risk.**
- This bot requires the `discord.js-selfbot-v13` package to interact with Discord.

---

## **Features**

- **`?#check @user`**: Fetches and logs user information (roles, join date, user ID, etc.).
- **`?#checkall`**: Fetches and logs user information for all members in the current server.
- **`?#bantoggle on` / `?#bantoggle off`**: Toggles whether the bot will automatically ban users from a specific server after logging their information.

---

## **Setup**

### **1. Prerequisites**
Before starting, make sure you have:

- **Node.js** installed on your system.
- A **Discord bot token** with the necessary permissions to read user information and ban members from servers.

### **2. Installing Dependencies**

1. Clone or download the repository.
   
2. Run the following commands to install the required dependencies:

```bash
npm init -y
npm install discord.js-selfbot-v13
```

---

## **Configuration**

### **3. `servers.json`**

You need to create a `servers.json` file to store the IDs of the servers you want the bot to track. This file will be used to determine which servers to fetch user information from.

**Example `servers.json`:**
```json
[
  "YOUR_SERVER_ID_1",
  "YOUR_SERVER_ID_2"
]
```

Replace `YOUR_SERVER_ID_1` and `YOUR_SERVER_ID_2` with the actual server IDs.

### **4. Bot Token and Target Server Configuration**

- **Bot Token**: In the code, replace `YOUR_BOT_TOKEN` with your actual bot token.
- **Target Server for Banning**: Replace the placeholder `TARGET_SERVER_ID` with the server ID where users will be banned if `banToggle` is enabled.

---

## **Usage**

Once you've set everything up, follow these steps to run the bot:

1. Replace the placeholders in the code (`YOUR_BOT_TOKEN` and `TARGET_SERVER_ID`).
2. Run the bot using the following command:

```bash
node bot.js
```

The bot should now be online, and you can use the following commands in Discord:

- **`?#check @user`**: Check and log the mentioned user's information.
- **`?#checkall`**: Log information for all members in the current server.
- **`?#bantoggle on`**: Enable banning users after logging their info.
- **`?#bantoggle off`**: Disable banning users after logging their info.

---

## **How to Purchase**

To get the full code and configuration files for this bot, please follow the instructions below:

1. **Contact the Seller**: Reach out via the provided contact method to express interest in purchasing the code.
2. **Payment**: The price for the bot is **up to 500 Robux**. Once payment is confirmed, the full code will be provided, along with detailed instructions for setup.
3. **Support**: You will receive ongoing support for setting up and troubleshooting the bot once purchased.

**Contact Information:**
- **Discord User ID**: `1305961143503945772`
- You can send a friend request to my Discord ID: [Click here to send a friend request](https://discordapp.com/users/1305961143503945772). Please make sure to message me regarding your purchase!

---

## **Disclaimer**

- **Use responsibly**: While the bot provides powerful features, it is essential to remember that self-bots violate Discord’s Terms of Service. By using this bot, you assume all responsibility for any consequences related to its use.
- **No Refunds**: Once the code has been delivered, it is non-refundable.
- **Robux Payment**: The payment must be made through Robux. You can use **Roblox Group Funds** or a **Roblox Payment Link** to pay. If you need further instructions for making the payment, feel free to contact me directly.

---

### **Robux Payment Instructions:**

1. **Roblox Group Funds**: You can pay using the group funds of a Roblox group you own. Once the payment is confirmed, I will provide the code.
   
2. **Roblox Payment Link**: You can also send Robux directly through the **Roblox Payment Link** system. For more details, please reach out to me.

