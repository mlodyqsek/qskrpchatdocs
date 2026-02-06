# QSK RPCHAT V2 - Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Commands](#commands)
5. [Security Features](#security-features)
6. [Custom Emotes](#custom-emotes)
7. [Framework Integration](#framework-integration)
8. [Localization](#localization)
9. [Exports](#exports)
10. [Troubleshooting](#troubleshooting)

---

## Introduction

QSK RPCHAT V2 is an advanced roleplay chat system for FiveM servers that enhances player communication with proximity-based commands, 3D text displays, custom emotes, profanity filtering, and extensive customization options.

### Key Features

- 5 Roleplay Commands - ME, DO, TRY, IF, MED with customizable 3D text displays
- Communication System - OOC, LOOC, Whisper, and Report commands
- Job-Restricted Commands - Dispatch and Department radio for emergency services
- Custom Emotes - Support for unlimited custom image-based emotes
- Security System - Profanity filter, spam detection, and rate limiting
- Multi-Language - English and Polish included, easily expandable
- Framework Support - Compatible with QBCore, ESX, or Standalone

### Technical Specifications

- **Version**: 2.0.1
- **Framework**: FiveM (Lua 5.4)
- **Performance**: 0.00ms idle, 0.01ms active
- **Dependencies**: None (standalone compatible)

---

## Installation

### Basic Installation

1. Download the resource package
2. Extract the folder to your server's `resources` directory
3. Rename the folder to `qsk-rpchat` (if not already named)
4. Add `ensure qsk-rpchat` to your `server.cfg`
5. Restart your server

### File Structure

```
qsk-rpchat/
├── client/
│   └── client.lua
├── server/
│   └── server.lua
├── shared/
│   ├── config.lua
│   ├── config_functions.lua
│   ├── config_censor.lua
│   └── config_emotes.lua
├── locales/
│   ├── locale.lua
│   ├── en.lua
│   └── pl.lua
├── html/
│   └── index.html
├── emotes/
│   └── laugh.png
└── fxmanifest.lua
```

### Post-Installation

After installation, configure the basic settings in `shared/config.lua`:
- Set your preferred language
- Configure the chat open key
- Adjust 3D text settings
- Enable/disable commands as needed

---

## Configuration

### Main Settings

Located in `shared/config.lua`

#### Language Configuration

Set the language for your server. Available languages include English (en) and Polish (pl). Additional languages can be added by creating new locale files in the `locales/` folder.

#### Player ID Display

Toggle whether player IDs appear next to names in chat. When enabled, displays as `PlayerName [123]`. This is useful for administrative purposes and player identification.

#### Chat Keybind

Configure which key opens the chat interface. The default is key 245 (T key), but can be changed to any valid FiveM control key.

#### 3D Text Settings

Customize the appearance of 3D text that appears above players when using RP commands:

**Font Options**
- Choose from FiveM's built-in fonts (0-7)
- Default: Font 4

**Scale**
- Controls text size
- Range: 0.1 - 1.0
- Default: 0.35

**Offset Z**
- Vertical offset above player head
- Adjusts how high text appears
- Default: 1.0

**Visual Effects**
- Outline: Adds black outline for better visibility
- Shadow: Adds drop shadow effect

#### Bypass Commands

Specify commands that should execute directly without processing through the chat system. These commands are typically administrative tools or framework-specific commands.

### RP Commands Configuration

Each roleplay command can be individually configured with the following options:

**Basic Settings**
- Enable/disable the command
- Display name shown in chat
- Description for help text
- Proximity distance (how far others can see)

**Visual Settings**
- Chat color (hexadecimal color code)
- Border color (hexadecimal color code)
- 3D text toggle
- 3D text color (RGBA values)
- 3D text visibility distance
- 3D text display duration (milliseconds)

#### ME Command

Describes character actions. Example: `/me scratches head`
- Default color: Purple (#9b59b6)
- Shows 3D text above player
- Proximity-based visibility

#### DO Command

Describes environmental events. Example: `/do The rain begins to fall`
- Default color: Red (#e74c3c)
- Shows 3D text above player
- Used for scene-setting

#### TRY Command

Attempts an action with random success/fail. Example: `/try pick the lock`
- Default color: Blue (#3498db)
- Shows SUCCESS or FAILED with different colors
- 50/50 chance of success

#### IF Command

50/50 yes or no chance. Example: `/if will it rain today`
- Default color: Orange (#f39c12)
- Shows YES or NO with different colors
- Used for random decisions

#### MED Command

Medical roleplay actions. Example: `/med checks vital signs`
- Default color: Red (#e74c3c)
- Specialized for medical personnel
- Shows 3D text above player

### Standard Commands Configuration

#### OOC (Out of Character)

Global out-of-character chat visible to all players on the server. Use for general non-roleplay discussions.

#### LOOC (Local Out of Character)

Local out-of-character chat only visible to nearby players. Respects proximity distance settings.

#### Whisper

Send direct messages to specific players by ID. Requires target player ID as first argument.

Usage: `/w [player_id] [message]`

#### Report

Send reports to online administrators. All online staff members with admin permissions will receive the report.

### Job Commands Configuration

Commands restricted to specific jobs. Configure which jobs have access to each command.

#### Dispatch

Emergency dispatch system for coordinating emergency services. Default jobs: police, ambulance, fire.

#### Department

Department-specific radio communications. Shares same job restrictions as dispatch.

### Custom Commands

Create custom commands that trigger external events in other scripts. Supports both server-side and client-side event triggers.

**Configuration Options**
- Command name (without slash)
- Display name
- Description
- Colors
- Event trigger (server or client)

**Example Use Cases**
- 911 emergency call system
- Taxi service integration
- Social media posts
- Custom job-specific actions

### System Messages

Configure colors and display names for system notifications:
- Server announcements
- System messages
- Success notifications
- Error messages
- Warning messages
- Info messages

---

## Commands

### Roleplay Commands

**ME Command**
- Usage: `/me [action]`
- Description: Describe your character's actions
- Example: `/me looks around nervously`
- Visibility: Proximity-based

**DO Command**
- Usage: `/do [event]`
- Description: Describe environmental events
- Example: `/do The door creaks open`
- Visibility: Proximity-based

**TRY Command**
- Usage: `/try [action]`
- Description: Attempt an action with random success
- Example: `/try lockpick the door`
- Result: Shows SUCCESS or FAILED

**IF Command**
- Usage: `/if [question]`
- Description: 50/50 yes or no chance
- Example: `/if will the guard notice me`
- Result: Shows YES or NO

**MED Command**
- Usage: `/med [action]`
- Description: Medical roleplay actions
- Example: `/med administers first aid`
- Visibility: Proximity-based

### Communication Commands

**OOC Command**
- Usage: `/ooc [message]`
- Description: Global out-of-character chat
- Example: `/ooc Is the server restarting soon?`
- Visibility: Server-wide

**LOOC Command**
- Usage: `/looc [message]`
- Description: Local out-of-character chat
- Example: `/looc Can we continue this RP later?`
- Visibility: Proximity-based

**Whisper Command**
- Usage: `/w [player_id] [message]`
- Description: Send private message to specific player
- Example: `/w 42 Meet me at the docks`
- Visibility: Target player only

**Report Command**
- Usage: `/report [message]`
- Description: Send report to online administrators
- Example: `/report Player breaking rules at Legion Square`
- Visibility: Admin team only

### Job Commands

**Dispatch Command**
- Usage: `/dispatch [message]`
- Description: Send emergency dispatch message
- Restriction: Requires emergency services job
- Example: `/dispatch 10-71 at Legion Square`

**Department Command**
- Usage: `/dept [message]`
- Description: Department radio communication
- Restriction: Requires department job
- Example: `/dept All units respond to code 3`

---

## Security Features

### Profanity Filter

The profanity filter system prevents inappropriate language in chat through multiple detection methods.

**Settings**

Configure in `shared/config_censor.lua`:
- Enable/disable entire system
- Block messages or replace words
- Warn players when censored
- Log censored messages
- Case-insensitive matching
- Leetspeak variation detection

**Banned Words**

Add words to the banned list. The system will detect these words regardless of case or common character substitutions.

**Word Replacement**

Configure specific words to be automatically replaced with alternatives (like asterisks or custom text).

**Leetspeak Detection**

Automatically detects common character substitutions:
- 0 → o
- 1 → i
- 3 → e
- 4 → a
- 5 → s
- 7 → t
- 8 → b
- @ → a
- $ → s
- ! → i

**Exemptions**

Commands that bypass censorship (like admin commands and reports). Administrators can also be exempted from all filters.

### Spam Detection

Prevents chat spam through multiple detection methods.

**Repeated Characters**

Blocks messages with excessive repeated characters. Configurable maximum (default: 5 consecutive characters).

Example blocked: "heeeeeeelp" or "aaaaaaa"

**Caps Lock Abuse**

Detects excessive use of capital letters. Configure maximum percentage of capitals allowed.

Requirements:
- Minimum message length to check
- Maximum percentage of capitals

**Repeated Messages**

Tracks player message history and blocks spam. Configure maximum number of identical messages allowed in succession.

**Configuration**

All spam detection thresholds are fully customizable in the config file.

### Rate Limiting

Prevents players from flooding the chat with too many messages.

**Message Rate Limit**
- Maximum messages per minute
- Cooldown between individual messages (milliseconds)

**Report Rate Limit**
- Maximum reports per hour
- Cooldown between reports (milliseconds)

**Tracking**

System automatically tracks player activity and enforces limits. Administrators can be exempted from rate limiting.

### Input Validation

Protects against malicious input and exploits.

**SQL Injection Protection**

Detects and blocks common SQL injection patterns:
- DROP TABLE attempts
- DELETE FROM attempts
- INSERT INTO attempts
- UNION SELECT attempts
- OR 1=1 patterns
- Other common injection methods

**Content Sanitization**

Automatically removes:
- HTML tags
- Script tags
- Excessive whitespace
- Potentially dangerous characters

**Message Length**

Enforces maximum message length (default: 500 characters) to prevent spam and performance issues.

**Admin Exemptions**

Administrators bypass all security checks including:
- Profanity filter
- Spam detection
- Rate limiting
- Content restrictions

Admin status is determined by the framework integration function or ACE permissions.

---

## Custom Emotes

### Built-in Emoji

Over 30 pre-configured emoji shortcuts available by default.

**Common Emotes**
- :smile: or :happy: → 😊
- :laugh: or :lol: → 😂
- :sad: or :cry: → 😢
- :angry: or :mad: → 😠
- :love: or :heart: → ❤️
- :fire: → 🔥
- :cool: → 😎
- :wink: → 😉

**Actions**
- :clap: → 👏
- :thumbsup: → 👍
- :thumbsdown: → 👎
- :ok: → 👌
- :pray: → 🙏
- :wave: → 👋
- :point: → 👉
- :eyes: → 👀

**Text-Based**
- :) → 🙂
- :( → 🙁
- :D → 😃
- :P → 😛
- ;) → 😉
- <3 → ❤️
- :o → 😮

**Objects**
- :gun: → 🔫
- :car: → 🚗
- :police: → 🚓
- :ambulance: → 🚑
- :fire_truck: → 🚒
- :money: → 💰
- :star: → ⭐

### Custom Image Emotes

Add unlimited custom emotes using image files.

**Supported Formats**
- PNG (recommended for transparency)
- JPG/JPEG
- GIF (animated support)
- WEBP

**Adding Custom Emotes**

1. Place your image file in the `emotes/` folder
2. Open `shared/config_emotes.lua`
3. Add entry to ConfigEmotes.Custom table
4. Use format: `[":emotename:"] = "emotes/filename.png"`
5. Restart server

**Example Configuration**

The file includes an example custom emote that references `laugh.png`. Follow this pattern for additional emotes.

**Best Practices**
- Use descriptive emote names
- Keep file sizes reasonable (under 500KB)
- Use square aspect ratio for consistent display
- Test emotes in-game before deploying

### Emote Settings

**Enable/Disable System**

Toggle the entire emote system on or off.

**Custom Emotes Toggle**

Allow or disallow custom image-based emotes while keeping built-in emoji active.

**Animation**

Enable animated display of emotes (applies to GIF files).

**Maximum Emotes**

Limit number of emotes allowed per message to prevent spam.

### Image URL Pasting

Optional feature to allow pasting external image URLs directly in chat.

**Security Settings**

This feature is disabled by default for security reasons. When enabled:
- Requires domain whitelist
- Maximum image dimensions
- Allowed file extensions only
- Automatic URL detection

**Whitelisted Domains**

Pre-configured safe image hosting domains:
- imgur.com
- cdn.discordapp.com
- i.gyazo.com
- tenor.com
- giphy.com

**Configuration Options**
- Enable/disable URL pasting
- Maximum image width (pixels)
- Maximum image height (pixels)
- Show as embedded image or link
- Require whitelist check
- Auto-detect image URLs in messages

**Security Note**

External image URLs can pose security and content moderation risks. Only enable this feature if you trust your player base and have active moderation.

---

## Framework Integration

### QBCore Integration

The script includes built-in support for QBCore framework.

**Admin Check**

Uncomment the QBCore section in `config_functions.lua` to enable admin permission checking through QBCore's permission system.

**Job System**

Uncomment the QBCore section to retrieve player job data for job-restricted commands.

**Player Data**

Access to QBCore player objects for advanced integrations.

### ESX Integration

Full support for ESX framework included.

**Admin Check**

Uncomment the ESX section in `config_functions.lua` to check player groups (admin, superadmin, etc.).

**Job System**

Uncomment the ESX section to retrieve player job information for command restrictions.

**Player Object**

Access to ESX player objects for custom functionality.

### Standalone Mode

Works without any framework by default.

**ACE Permissions**

Uses FiveM's native ACE permission system:
- `chat.admin` - Admin permissions
- `chat.bypass_censor` - Bypass profanity filter
- Custom ACE permissions can be added

**Default Job System**

Returns unemployed status when no framework is detected.

### Custom Framework

Easily adapt to custom frameworks.

**Admin Function**

Modify the `IsPlayerAdmin` function to check your custom permission system.

**Job Function**

Modify the `GetPlayerJob` function to return job data from your framework.

**Notification System**

Built-in notification functions can trigger your custom notification system.

### Notification System

Pre-configured notification functions available:

**Success Notifications**

Display success messages to players.

**Info Notifications**

Display informational messages.

**Warning Notifications**

Display warning messages.

**Error Notifications**

Display error messages.

**System Notifications**

Display system announcements.

**Welcome Messages**

Automatically sent when players join the server.

### Report System

**Submit Handler**

Customize what happens when a player submits a report:
- Send to Discord webhook
- Log to database
- Trigger custom notification system
- Forward to external admin tools

**Admin Check**

Configure which players receive report notifications based on your permission system.

**Player Identifier**

Retrieves player identifiers for logging:
- License
- Steam
- Discord
- Custom identifiers

### Event Handlers

**Player Join**

Triggered when a player connects. Default behavior sends a welcome message after 2 seconds.

**Player Leave**

Triggered when a player disconnects. Add custom cleanup logic as needed.

### Command Detection

**External Commands**

Check if commands exist in other resources before processing.

**Command Execution**

Execute commands from other resources programmatically.

---

## Localization

### Available Languages

- English (en) - Default
- Polish (pl) - Full translation included

### Adding New Languages

**Step 1: Create Language File**

Create a new file in the `locales/` folder following the naming pattern: `languagecode.lua` (example: `de.lua` for German).

**Step 2: Copy Structure**

Copy the structure from `locales/en.lua` to ensure all required translation keys are present.

**Step 3: Translate Strings**

Replace all English text with translations in your target language. Maintain the same key names.

**Step 4: Configure**

Set the locale in `shared/config.lua` to your new language code.

**Step 5: Test**

Restart the server and verify all messages display correctly.

### Translation Keys

**System Messages**
- Welcome message
- Report confirmations
- Admin notifications

**Error Messages**
- Invalid player ID
- Player not found
- Empty message
- Message too long
- Invalid content

**Whisper System**
- Usage instructions
- Message prefixes

**Rate Limiting**
- Cooldown messages
- Limit exceeded warnings

**Spam Detection**
- Repeated character warning
- Caps abuse warning
- Repeated message warning

**Censorship**
- Blocked message notification
- Warning to player

**Commands**
- Disabled command message
- No permission message
- Job requirement message

**3D Text**
- Try command results (success/failed)
- If command results (yes/no)

**General**
- System name
- Server name
- Admin title
- Staff title

### String Formatting

Translation strings support variable insertion using Lua's string.format syntax.

**Example**

The welcome message uses %s for player name insertion. When translating, maintain the same number and order of variables.

### Testing Translations

After adding a new language:
1. Restart the server
2. Check console for locale loading confirmation
3. Test all commands
4. Verify 3D text displays correctly
5. Check error messages
6. Test notification system

---

## Exports

### Client-Side Exports

**Add Message**

Programmatically add messages to chat from other resources.

Function: `exports['qsk-rpchat']:addMessage(type, user, content)`

Parameters:
- type: Message type (matches command types)
- user: Display name/username
- content: Message content

**Open Chat**

Open the chat interface programmatically.

Function: `exports['qsk-rpchat']:openChat()`

Use case: Custom keybinds or UI integrations.

**Close Chat**

Close the chat interface programmatically.

Function: `exports['qsk-rpchat']:closeChat()`

Use case: Force close chat during specific game events.

### Server-Side Events

**Send Message**

Trigger from client to send messages to server.

Event: `qsk-rpchat:sendMessage`

**Receive Message**

Triggered to send messages to clients.

Event: `qsk-rpchat:receiveMessage`

**Show 3D Text**

Display 3D text above specific players.

Event: `qsk-rpchat:show3DText`

**Request Config**

Client requests configuration from server.

Event: `qsk-rpchat:requestConfig`

**Load Config**

Server sends configuration to client.

Event: `qsk-rpchat:loadConfig`

### Integration Examples

**Custom Notification**

Send custom notifications using the chat system from any resource.

**Event Logging**

Log important events to chat for admin visibility.

**Announcement System**

Create server-wide announcements using the chat display.

**Custom Commands**

Integrate external commands with chat display using the export functions.

---

## Troubleshooting

### Chat Not Opening

**Keybind Issues**
- Verify the OpenKey config value
- Check for keybind conflicts with other resources
- Test with default key (245 - T key)

**Resource Not Starting**
- Check server console for errors
- Verify `ensure qsk-rpchat` is in server.cfg
- Confirm resource name matches folder name
- Check for missing files

**Client Errors**
- Press F8 to open client console
- Look for JavaScript errors
- Check for NUI-related errors
- Verify HTML file is loading

### 3D Text Not Appearing

**Configuration Check**
- Confirm Text3D.enabled is set to true
- Verify command has show3DText enabled
- Check text3DDuration is sufficient (min 3000ms recommended)

**Distance Issues**
- Increase text3DDistance value
- Check proximity distance for command
- Verify player is within range

**Visual Settings**
- Increase text scale if too small
- Adjust offsetZ if text appears in ground
- Enable outline for better visibility

### Commands Not Working

**Command Disabled**
- Check if command enabled in config
- Verify not in BypassCommands list

**Permission Issues**
- Confirm job requirements for job commands
- Check admin permissions for restricted commands
- Verify framework integration is correct

**Syntax Errors**
- Check command usage format
- Verify proper spacing
- For whisper, ensure player ID is valid number

### Emotes Not Loading

**File Issues**
- Verify image files exist in emotes folder
- Check file paths in config match actual filenames
- Confirm file extensions are supported
- Check file permissions on server

**Configuration**
- Ensure allowCustom is set to true
- Verify emote syntax uses colons (`:emotename:`)
- Check for typos in emote names

**Client Cache**
- Clear FiveM cache
- Reconnect to server
- Check browser cache if using NUI

### Profanity Filter Not Working

**Configuration**
- Verify enabled is set to true in ConfigCensor.Settings
- Check banned words list is populated
- Confirm caseInsensitive setting

**Exemptions**
- Check if player has admin exemption
- Verify command isn't in exemption list
- Test with non-admin account

**Detection Issues**
- Add more word variations to banned list
- Enable checkVariations for leetspeak
- Test with different word patterns

### Rate Limiting Issues

**Too Restrictive**
- Increase maxPerMinute/maxPerHour values
- Reduce cooldown times
- Check if values are appropriate for server size

**Not Working**
- Verify security settings are enabled
- Check console for rate limit errors
- Test with new player connection

**Admin Bypass**
- Confirm admin check function works
- Verify ACE permissions are set correctly
- Check framework integration

### Performance Issues

**High CPU Usage**
- Reduce number of active 3D texts
- Lower text3DDuration for commands
- Disable unused commands
- Check for message spam

**Memory Leaks**
- Monitor active3DTexts table size
- Check playerMessages tracking
- Verify old data is being cleared

**Client FPS Drops**
- Reduce 3D text render distance
- Disable outline/shadow effects
- Lower text scale
- Limit emotes per message

### Common Error Messages

**"Invalid player ID"**
- Whisper command requires valid numeric player ID
- Check player is online
- Use correct syntax: `/w [id] [message]`

**"Rate limit exceeded"**
- Player sent too many messages too quickly
- Wait for cooldown period
- Adjust rate limits if too restrictive

**"Message too long"**
- Message exceeds 500 character limit
- Split message into multiple parts
- Adjust max length in config if needed

**"Command disabled"**
- Command is set to enabled = false in config
- Enable command in configuration
- Restart resource after config change

**"No permission"**
- Player lacks required job for command
- Check job configuration
- Verify framework integration returns correct job

### Getting Help

**Before Requesting Support**
- Check F8 console for errors
- Review server console logs
- Verify configuration is correct
- Test with default configuration
- Check FiveM version compatibility

**When Requesting Support**
- Provide error messages from console
- Include relevant config sections
- Describe steps to reproduce issue
- Mention framework and version
- List other chat-related resources

**Debug Mode**

Enable console logging in config files to see detailed debug information:
- Message processing logs
- Censor detection logs
- Rate limit tracking
- Command execution logs
