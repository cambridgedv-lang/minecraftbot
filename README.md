# TheSilence Minecraft Bot

A fully-featured Minecraft 1.21+ bot built with **mineflayer** that includes auto-eating, auto-respawning, auto-authentication, anti-AFK behavior, and a web dashboard for 24/7 hosting.

## Features

✅ **Auto-Register & Auto-Login** – Register on first join, login on subsequent joins (AuthMe-compatible servers)  
✅ **Auto-Eat from Hotbar** – Automatically eats when health/hunger is below threshold  
✅ **Auto-Respawn** – Automatically respawns when the bot dies  
✅ **Anti-AFK** – Random look rotations and jumps to prevent AFK kicks  
✅ **Command System** – Support for `/follow`, `/stop`, `/come`, `/jump`, `/say` and custom commands  
✅ **Web Dashboard** – Control bot, view status, send chat/commands from browser  
✅ **Auto-Reconnect** – Automatically reconnects if disconnected  
✅ **Cracked Server Support** – Works with offline-mode servers  

## Quick Start

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure `config.json`

Edit the configuration file to match your server and preferences:

```json
{
  "host": "play.arctixmc.net",
  "port": 25565,
  "username": "TheSilence",
  "owner": "cambridgedv",
  "prefix": "/",
  "auth": "offline",
  "reconnectDelayMs": 5000,
  "webPort": 3000,
  "autoEat": {
    "enabled": true,
    "foodThresholdHP": 15,
    "checkIntervalMs": 1000
  },
  "antiAfk": {
    "enabled": true,
    "minIntervalMs": 15000,
    "maxIntervalMs": 30000
  },
  "autoRespawn": {
    "enabled": true
  },
  "joinSequence": {
    "enabled": true,
    "password": "silencity22",
    "registerCommand": "/register silencity22 silencity22",
    "loginCommand": "/login silencity22",
    "afterLoginCommands": ["/warp afk"],
    "initialDelayMs": 2000,
    "stepDelayMs": 2500
  }
}
```

### 3. Start the Bot

```bash
npm start
```

The bot will:
1. Connect to the server
2. Auto-register on first join (if configured)
3. Auto-login on subsequent joins
4. Execute any configured after-login commands (e.g., `/warp afk`)
5. Start the web dashboard on http://localhost:3000

## Configuration Options

### Core Settings
- **host** – Server IP address
- **port** – Server port (default: 25565)
- **username** – Bot username (must match cracked account)
- **owner** – Username that can give commands (leave empty to allow anyone)
- **prefix** – Command prefix (default: `/`)
- **auth** – `"offline"` for cracked, `"microsoft"` for premium accounts
- **version** – `false` to auto-detect, or specific version like `"1.21"`

### Auto-Eat Settings
- **enabled** – Toggle auto-eating
- **foodThresholdHP** – Eat when health/hunger drops below this (default: 15)
- **checkIntervalMs** – How often to check health/hunger (default: 1000ms)

### Anti-AFK Settings
- **enabled** – Toggle anti-AFK behavior
- **minIntervalMs** – Minimum interval between AFK actions
- **maxIntervalMs** – Maximum interval between AFK actions

### Auto-Respawn
- **enabled** – Toggle auto-respawning on death

### Join Sequence (AuthMe servers)
- **enabled** – Toggle authentication sequence
- **password** – Password for `/register` and `/login`
- **registerCommand** – Command for first join (use `{password}` placeholder)
- **loginCommand** – Command for subsequent joins
- **afterLoginCommands** – Array of commands to run after spawning
- **initialDelayMs** – Delay before starting auth sequence
- **stepDelayMs** – Delay between commands

## Web Dashboard

Visit **http://localhost:3000** to:
- ✅ Start/Stop/Reconnect the bot
- 📊 View real-time bot status
- 💬 Send chat messages and commands directly
- 📜 See activity logs

## Commands

When chatting with the bot (prefix `/`), use:

| Command | Usage | Description |
|---------|-------|-------------|
| `/follow` | `/follow` | Follow the player |
| `/stop` | `/stop` | Stop following/pathfinding |
| `/come` | `/come` | Bot comes to you |
| `/jump` | `/jump` | Make the bot jump |
| `/say <msg>` | `/say Hello world` | Bot says a message |
| `/warp <name>` | `/warp afk` | Use server warps (if configured) |

## Project Structure

```
minecraftbot/
├── index.js          # Main bot logic
├── config.json       # Configuration
├── main.html         # Web dashboard
├── package.json      # Dependencies
├── README.md         # This file
└── .state.json       # Auto-generated state file (tracks registration)
```

## Troubleshooting

### Bot won't connect
- Check server IP and port in `config.json`
- Verify `auth` is set to `"offline"` for cracked servers
- Check firewall/port forwarding

### Bot connects but won't spawn
- Ensure `/register` and `/login` commands are correct for your server
- Increase `initialDelayMs` if server is slow
- Check server logs for authentication errors

### Auto-eat not working
- Verify food items are in hotbar (slots 0-8)
- Check that `autoEat.enabled` is `true`
- Lower `foodThresholdHP` to test

### Bot keeps disconnecting
- Increase `reconnectDelayMs`
- Check for server bans or rate limiting
- Enable anti-AFK to prevent AFK kicks

## Running 24/7

To keep the bot running 24/7:

1. **Use a cloud host** (Replit, Railway, Heroku, etc.)
2. **UptimeRobot monitoring** – Use the `/health` endpoint
3. **Process manager** – Use `pm2` for local machines:
   ```bash
   npm install -g pm2
   pm2 start index.js --name "minecraftbot"
   pm2 save
   pm2 startup
   ```

## Requirements

- **Node.js** >= 18
- **Minecraft Server** version 1.21+
- **Internet connection**

## License

MIT

## Credits

Built with [mineflayer](https://github.com/PrismarineJS/mineflayer) and [mineflayer-pathfinder](https://github.com/PrismarineJS/mineflayer-pathfinder).
