# Anti RK/RDM Prison Life style for FEGK

![bruh](https://c.tenor.com/QMf9LfAy5yEAAAAd/rdm-garrys-mod.gif)

By: BOBOH                         
made for FEGK by Thienbao2109

## Documentation
<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#Setup-Installation">Setup/Installation</a></li>
      </ul>
    </li>
  </ol>
</details>

## Setup/Installation

### Server setup(required)
To get started with using the Anti-RK system require the module script each time you intend to use it as shown below.

```lua
-- This is a script you would create inside a server script
local RKTagger = require(Module_path)
```

To see if a player was killed by another one we will need to check each time a player dies as shown below.

```lua
-- This is a script you would create inside a server script
local RKTagger = require(Module_path)

-- this function will use the anti RK module to listen to killings, FEGK adds a killer Tag on default which we can use to determine the killer
local function setupkilltagger(obj)
    obj.Humanoid.Died:connect(function()
	-- The module will handle kill infractions
	RKTagger.HumDied(obj.Humanoid)
    end)
end

-- Listen for players dying
Players.PlayerAdded:Connect(function(player)
    wait()
    player.CharacterAdded:connect(function(Character)
    -- listen for death
	setupkilltagger(Character)
    end)
end)
```

