Lua plugin processor V4.1
===============================

This is a portion of the vim2 editor, avaliable on Git: https://github.com/bendaws/vim2
===============================

This subfolder contains functions in C and Lua for plugins. For using this API, you should mostly use the plugins api in Lua.

Here is a small example, a tiny-sized command bar that can be activated by pressing `:`.
```lua
local command_bar = {}
local vim2 = require("vim2")

command_bar.version = "1.0.0"
command_bar.name = "Command Bar"
command_bar.author = "John Doe"

function helpCmd(args)
    print("help was ran")
end

local commands = {
    {
        "help",
        helpCmd,
    }
}

function onCommandBar()
    local command_raw = vim2.question(":") -- will emulate the :
    local command = command_raw.split(" ")

    for _, commandTemplate in commands do
        if commandTemplate[1] == command[1] then
            commandTemplate[2](command)
        end    
    end
end

vim2.set_keybind(":", onCommandBar)
```
