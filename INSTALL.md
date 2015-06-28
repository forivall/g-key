## Plugin Installation
1. Open and install the package.
**64-bit users:** If you are using a 64-bit operating system you will need to use the 64-bit version of TeamSpeak 3.

2. Start TeamSpeak 3 and open the "Plugins" dialog (<kbd>Ctrl+Shift+P</kbd>).

3. Make sure the "G-Key Plugin" is checked.

4. Now to configure the G-Keys for usage with the plugin refer to the Logitech Gaming Software section.  
   Or, if you prefer the old legacy drivers go to the the GamePanel Software (Legacy) section.  
   **Note:** The old G930 plugin system is no longer supported. Users of the G930 should make sure their drivers are updated and refer to the Logitech Gaming Software section for instructions.

## Logitech Gaming Software

This is Logitech's new software package, it seems they're slowly merging more and more devices into this package. So we can just sit back and watch as more Logitech devices get supported by the plugin.

Here are the instructions on configuring the software to support the plugin.

1. Open the Logitech Gaming Software

2. Open the "Customize G-keys" tab

3. Open the script for your configuration.

4. Now enter the script, the simplest script that only supports push-to-talk is this:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()

    if gkey == 3 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_PTT_ACTIVATE")
        end
        if event == "G_RELEASED" then
            OutputDebugMessage("TS3_PTT_DEACTIVATE")
        end
    end
end
```

Change **3** to the G-key you would like to use for the push-to-talk command and **1** to the G-key Mode (M1, M2, M3) that key is assigned on.

If you use a non-keyboard device together with your keyboard and would like different g-key settings for them, refer to the full Push-to-talk example script.

For more functions and advanced scripting examples, refer to the Scripting section. For more examples, go to the Example scripts section.

## GamePanel Software (Legacy)
This is the old keyboard software, while the plugin still supports this software package, it is recommended that you update to the new Logitech Gaming Software.

1. Open the Logitech G-series Key Profiler

2. Assign the G-keys you want to use to control TeamSpeak 3 to "Script". Note the G-keys and Mode you've set here, as we will need them later.

3. Open the Script Editor

4. Now enter the script, the simplest script that only supports push-to-talk is this:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 3 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_PTT_ACTIVATE")
        end
        if event == "G_RELEASED" then
            OutputDebugMessage("TS3_PTT_DEACTIVATE")
        end
    end
end
```

Change **3** to the G-key you would like to use for the push-to-talk command and **1** to the G-key Mode (M1, M2, M3) that key is assigned on.

For more functions and advanced scripting examples, refer to the Scripting section. For more examples, go to the Example scripts section.

## Advanced scripting
All scripts should have the following layout:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()

    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            ...
        end
        if event == "G_RELEASED" then
            ...
        end
    end
end
```

You can change `gkey == 1` and `mkey == 1` to the G-key and mode you want. For example, if you want G3 to activate the command when M2 is active you change it to:  `gkey == 3` and `mkey == 2`. The `G_PRESSED` event should contain all the commands you want executed on pressing the key and `G_RELEASED` the commands on releasing the key. You can send a command to the plugin using `OutputDebugMessage` refer to the Command reference for a full list of commands.

If you use a G930 headset or any other non-keyboard device that uses the Logitech Gaming Software you can let some commands only be triggered if the key is pressed on those devices. In which case your script should use the following layout:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()

    if family == "kb" or family == "lhc" then
        if gkey == 1 and mkey == 1 then
            if event == "G_PRESSED" then
                ...
            end
            if event == "G_RELEASED" then
                ...
            end
        end
    else
        if gkey == 1 then
            if event == "G_PRESSED" then
                ...
            end
            if event == "G_RELEASED" then
                ...
            end
        end
    end
end
```

The first section should contain the commands intended for the keyboard, while the second section should contain commands for non-keyboard devices. Refer to the Push-to-talk example script to for an example.

```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()

    if family == "kb" or family == "lhc" then
        if gkey == 1 and mkey == 1 then
            if event == "G_PRESSED" then
                ...
            end
            if event == "G_RELEASED" then
                ...
            end
        end
    else
        if gkey == 2 then
            if event == "G_PRESSED" then
                ...
            end
            if event == "G_RELEASED" then
                ...
            end
        end
    end
end
```
