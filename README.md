# **Discord Self-Bot with User Info Logging and Ban Toggle**

## **Overview**

This project is a **Discord Self-Bot** built using `discord.js-selfbot-v13` to log user information (roles, join date, user ID, etc.) from multiple servers and optionally ban users from a specific server after logging their information.

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
- A **Discord bot token** with necessary permissions to read user information and ban members from servers.

### **2. Installing Dependencies**

1. Clone or download this repository.
   
2. Run the following commands to install the required dependencies:

```bash
npm init -y
npm install discord.js-selfbot-v13
```

---

## **Configuration**

### **3. `servers.json`**

Create a file called `servers.json` in the root of your project. This file should store the IDs of the servers you want the bot to track.

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

## **Code Explanation**

### **Main Bot File:**

```javascript
const { Client } = require("discord.js-selfbot-v13");
const client = new Client();
const servers = require("./servers.json");

let banToggle = false;  // Toggle for banning users

client.on("ready", () => {
    console.log(`Logged in as ${client.user.tag}`);
});

client.on("messageCreate", async (message) => {
    if (message.author.id !== client.user.id) return;
    
    // Command to check user info
    if (message.content.startsWith("?#check")) {
        const args = message.content.split(/\s+/);
        const isCheckAll = args[0] === "?#checkall";
        
        let usersToCheck = [];

        if (isCheckAll) {
            try {
                const members = await message.guild.members.fetch();
                usersToCheck = members.map(m => m.user);
            } catch {
                return message.channel.send("Failed to fetch members.");
            }
        } else {
            const mentions = message.mentions.users;
            if (!mentions.size) {
                return message.channel.send("Mention at least one user.");
            }
            usersToCheck = mentions.map(user => user);
        }

        for (const user of usersToCheck) {
            let found = false;

            // Loop through tracked servers to fetch user data
            for (const guildId of servers) {
                const guild = client.guilds.cache.get(guildId);
                if (!guild) continue;

                let member;
                try {
                    member = await guild.members.fetch(user.id);
                } catch {
                    continue;
                }

                if (member) {
                    found = true;

                    // Get roles, excluding "@everyone"
                    const roles = member.roles.cache
                        .filter(r => r.name !== "@everyone")
                        .map(r => r.name);

                    let formattedRoles = "";
                    roles.forEach((role, index) => {
                        formattedRoles += `> ${role}\n`;
                    });

                    // Limit the number of roles shown
                    if (roles.length > 10) {
                        formattedRoles += `> ...and ${roles.length - 10} more roles.`;
                    }

                    const joinDate = member.joinedAt?.toUTCString() || "Unknown";

                    const userInfoMessage = `
**User Info:** ${member.user.tag}
**Server:** ${guild.name || "Unknown"}
**Roles:**
${formattedRoles}
**Joined At:** ${joinDate}
**User ID:** ${member.id}
                    `;

                    const splitMessages = splitMessage(userInfoMessage, 2000);

                    try {
                        for (const chunk of splitMessages) {
                            await client.user.send(chunk);
                        }
                    } catch (err) {
                        console.log("❌ DM blocked. Sending to channel instead.");
                        for (const chunk of splitMessages) {
                            await message.channel.send(chunk);
                        }
                    }
                }
            }

            if (!found) {
                await client.user.send(`User **${user.tag}** not found in any of the tracked servers.`);
            }

            await message.channel.send(`Finished logging user info for ${user.tag}.`);

            if (banToggle) {
                // Replace with your target server ID
                const targetGuild = client.guilds.cache.get('TARGET_SERVER_ID'); // <== Update this with your server ID
                if (!targetGuild) {
                    await message.channel.send("Target server not found.");
                    return;
                }

                try {
                    const memberToBan = await targetGuild.members.fetch(user.id);
                    if (memberToBan) {
                        await memberToBan.ban({ reason: 'Banned after logging user info.' });
                        await message.channel.send(`User **${user.tag}** has been banned from the target server.`);
                    }
                } catch (error) {
                    console.log(`Failed to ban ${user.tag}: ${error.message}`);
                    await message.channel.send(`Failed to ban **${user.tag}** from the target server.`);
                }
            }
        }

        await message.channel.send("All server logs for users have been completed.");
    }

    // Command to toggle the ban functionality
    if (message.content.startsWith("?#bantoggle")) {
        const args = message.content.split(" ");
        if (args[1] === "on") {
            banToggle = true;
            message.channel.send("Ban toggle is now ON.");
        } else if (args[1] === "off") {
            banToggle = false;
            message.channel.send("Ban toggle is now OFF.");
        } else {
            message.channel.send("Invalid option. Use `?#bantoggle on` or `?#bantoggle off`.");
        }
    }
});

// Function to split messages into chunks of 2000 characters or less
function splitMessage(message, maxLength) {
    const chunks = [];
    while (message.length > maxLength) {
        let index = message.lastIndexOf('\n', maxLength);
        if (index === -1) index = maxLength;
        chunks.push(message.slice(0, index));
        message = message.slice(index);
    }
    chunks.push(message);
    return chunks;
}

// Log in with your bot's token (replace with your own token)
client.login("YOUR_BOT_TOKEN"); // <== Update with your bot token
```

---

## **Final Notes**

- **Never expose your bot token publicly.** Always keep it secret.
- You can enable or disable banning users with the `?#bantoggle` command. When enabled, the bot will automatically ban users from the server specified in the `TARGET_SERVER_ID` placeholder.
- Modify the `TARGET_SERVER_ID` and `YOUR_BOT_TOKEN` placeholders with your actual information to make the bot functional.

