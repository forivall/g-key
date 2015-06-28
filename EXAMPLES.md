
## Example scripts
### Push-to-talk
The command this plugin was written for, push-to-talk with just G-keys.
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_PTT_ACTIVATE")
        end
        if event == "G_RELEASED" then
            OutputDebugMessage("TS3_PTT_DEACTIVATE")
        end
    end
end
```

#### Non-keyboard devices
If you use a non-keyboard device like the G930 headset in combination with a keyboard and you want to differentiate between keys pressed on the headset or on the keyboard use the following variation on the script:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()

    if family == "kb" or family == "lhc" then
        if gkey == 1 and mkey == 1 then
            if event == "G_PRESSED" then
                OutputDebugMessage("TS3_PTT_ACTIVATE")
            end
            if event == "G_RELEASED" then
                OutputDebugMessage("TS3_PTT_DEACTIVATE")
            end
        end
    else
        if gkey == 2 then
            if event == "G_PRESSED" then
                OutputDebugMessage("TS3_PTT_ACTIVATE")
            end
            if event == "G_RELEASED" then
                OutputDebugMessage("TS3_PTT_DEACTIVATE")
            end
        end
    end
end
```

You can use this method with the other commands too.

### Input mute
Mutes the microphone, we can make a toggle key for this using the following script:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_INPUT_TOGGLE")
        end
    end
end
```

We can also make a PTT-like input mute that only unmutes while the key is pressed:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_INPUT_UNMUTE")
        end
        if event == "G_RELEASED" then
            OutputDebugMessage("TS3_INPUT_MUTE")
        end
    end
end
```

### Output mute
Mutes the speakers, pretty much the same as input mute, a toggle is:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_OUTPUT_TOGGLE")
        end
    end
end
```

We can also combine this function with PTT and make a script that mutes the output while PTT is active:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_OUTPUT_MUTE")
            OutputDebugMessage("TS3_PTT_ACTIVATE")
        end
        if event == "G_RELEASED" then
            OutputDebugMessage("TS3_OUTPUT_UNMUTE")
            OutputDebugMessage("TS3_PTT_DEACTIVATE")
        end
    end
end
```

### Away status
Sets away status on all servers, mostly we want this to toggle on the same key so we use the following script:
```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_AWAY_TOGGLE")
        end
    end
end
```

But sometimes we want one key to activate and one key to deactivate the away status:

```lua
function OnEvent(event, gkey, family)
    mkey = GetMKeyState()
    if gkey == 1 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_AWAY_ZZZ")
        end
    end
    if gkey == 2 and mkey == 1 then
        if event == "G_PRESSED" then
            OutputDebugMessage("TS3_AWAY_NONE")
        end
    end
end
```
