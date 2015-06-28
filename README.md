# TeamSpeak 3 G-Key Plugin

## Plugin Installation
1. Extract g-key.dll to your TeamSpeak3 plugins folder. By default this is: C:\\Program Files\\TeamSpeak 3 Client\\plugins

2. Start TeamSpeak3 and open the "Plugins" dialog (<kbd>Ctrl+Shift+P</kbd>).

3. Make sure the "G-Key Plugin" is checked.

4. Now to configure the G-keys refer to either the Logitech Gaming Software (Current) section if you are using the new drivers or the GamePanel Software (Legacy) section if you prefer the old drivers.

## Logitech Gaming Software (Current)
1. Open the Logitech Gaming Software

2. Open the "Customize G-keys" tab

3. Open the script for your configuration.

4. Now enter the script, the simplest script that only supports push-to-talk is this:
```lua
function OnEvent(event, arg)
    gkey = arg
    mkey = GetMKeyState()
    if event == "G_PRESSED" and gkey == 3 and mkey == 2 then
        OutputDebugMessage("TS3_PTT_ACTIVATE")
    end
    if event == "G_RELEASED" and gkey == 3 and mkey == 2 then
        OutputDebugMessage("TS3_PTT_DEACTIVATE")
    end
end
```
  <sup>(You can also find this example in scripts/ptt.lua, open it with notepad)</sup>

  Change **3** to the G-key you would like to use for the push-to-talk command and **2** to the G-key Mode (M1, M2, M3) that key is assigned on.

  For more commands, refer to the Command Reference section. For more examples, refer to the scripts folder.

5. You're done, you are now forever relieved from having to rebind G-keys.

## GamePanel Software (Legacy)
1. Open the Logitech G-series Key Profiler

2. Assign the G-keys you want to use to control TeamSpeak 3 to "Script". Note the G-keys and Mode you've set here, as we will need them later.

3. Open the Script Editor

4. Now enter the script, the simplest script that only supports push-to-talk is this:
```lua
function OnEvent(event, arg)
    gkey = arg
    mkey = GetMKeyState()
    if event == "G_PRESSED" and gkey == 3 and mkey == 2 then
        OutputDebugMessage("TS3_PTT_ACTIVATE")
    end
    if event == "G_RELEASED" and gkey == 3 and mkey == 2 then
        OutputDebugMessage("TS3_PTT_DEACTIVATE")
    end
end
```
  <sup>(You can also find this example in scripts/ptt.lua, open it with notepad)</sup>

  Change **3** to the G-key you would like to use for the push-to-talk command and **2** to the G-key Mode (M1, M2, M3) that key is assigned on.

  For more commands, refer to the Command Reference section. For more examples, refer to the scripts folder.

5. You're done, you are now forever relieved from having to rebind G-keys.

## Command Reference
This is a full list of commands supported by the plugin with a description about their function.
You can send these commands to the plugin with OutputDebugMessage, refer to the scripts folder for examples on how to use them.

Command            | Description
-------------------|--------------------
TS3_PTT_ACTIVATE   | Activate Push-to-talk
TS3_PTT_DEACTIVATE | Deactivate Push-to-talk
TS3_INPUT_MUTE     | Mute the Microphone
TS3_INPUT_UNMUTE   | Unmute the Microphone
TS3_INPUT_TOGGLE   | Toggle Microphone mute on/off
TS3_OUTPUT_MUTE    | Mute the Speakers/Headphones
TS3_OUTPUT_UNMUTE  | Unmute the Speakers/Headphones
TS3_OUTPUT_TOGGLE  | Toggle Speakers/Headphones mute on/off
TS3_AWAY_ZZZ       | Turn on globally away status
TS3_AWAY_NONE      | Turn off globally away status
TS3_AWAY_TOGGLE    | Toggle globally away status on/off


## Changelog

### Version 0.3
* Fixed a crash while activating Push-to-talk when the client hasn't joined any server yet.

### Version 0.2
* Changed the way debug messages are caught.
* Beta release.

### Version 0.1
* Internal development release.
