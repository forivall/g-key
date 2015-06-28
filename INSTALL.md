## Plugin Installation
1. Extract g-key.dll to your TeamSpeak 3 plugins folder. By default this is: C:\Program Files\TeamSpeak 3 Client\plugins
   **For 64-bit users:** If you are using a 64-bit system you will need to use the 64-bit version located in the x64 subfolder. This version can only be used with the 64-bit TeamSpeak3 client, available from the website.
2. Start TeamSpeak3 and open the "Plugins" dialog (<kbd>Ctrl+Shift+P</kbd>).
3. Make sure the "G-Key Plugin" is checked.

Now to configure the G-keys refer to either the Logitech Gaming Software (Current) section if you are using the new drivers or the GamePanel Software (Legacy) section if you prefer the old drivers.

Go to the Logitech G930 Headset section if you want to use your G930 to control  TeamSpeak 3.

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
<sub>(You can also find this example in scripts/ptt.lua, open it with notepad)</sub>
Change **3** to the G-key you would like to use for the push-to-talk command and **2** to the G-key Mode (M1, M2, M3) that key is assigned on.

For more commands, refer to the Command Reference section. For more examples, refer to the scripts folder.

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
<sub>(You can also find this example in scripts/ptt.lua, open it with notepad)</sub>
Change **3** to the G-key you would like to use for the push-to-talk command and **2** to the G-key Mode (M1, M2, M3) that key is assigned on.

For more commands, refer to the Command Reference section. For more examples, refer to the scripts folder.

## Logitech G930 Headset
1. Open the Logitech G930 Headset Settings

2. Click on the "+" below the word "Plugin"

3. Open "TS3GKey.dll" in the g930 subfolder.

4. Click "OK"

5. Click the "Select Application" dropdown box and choose "TS3GKey" for the keys you want to use to control TeamSpeak 3.

6. Choose the action you want the key to preform from the action dropdown.
