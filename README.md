# Anti RK/RDM for FEGK
<img src="https://user-images.githubusercontent.com/16319829/81180309-2b51f000-8fee-11ea-8a78-ddfe8c3412a7.png](https://www.wikihow.com/images/thumb/f/f4/Avoid-Being-Killed-on-ROBLOX-Step-3.jpg/v4-460px-Avoid-Being-Killed-on-ROBLOX-Step-3.jpg.webp" width=50% height=50%>

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

### **Server setup (required)**
To get started with using the Anti-RK system require the module script each time you intend to use it as shown below.
You will also need a remoteEvent called NotifyPlayer inside game.ReplicatedStorage.Remotes.
```lua
-- This is a script you would create inside a server script
local RKTagger = require(Module_path)
```

To see if a player was killed by another one we will need to check each time a player dies as shown below.

```lua
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
Now incase you plan on using Anti RK on dummies you can do the following.

```lua
-- This will loop trough all existing dummies inside a folder in worpkspace called TaggedDummies and will set them up.
for i, v in pairs(game.Workspace.TaggedDummies:GetChildren()) do
   setupkilltagger(v)
end
-- This will setup any Dummie that might get added in the future, make sure its actually a character with a Humanoid.
game.Workspace.TaggedDummies.ChildAdded:Connect(function(v)
    setupkilltagger(v)
end)
```

This is how the finished script should look like.

```lua
-- Listen for players dying
Players.PlayerAdded:Connect(function(player)
    wait()
    player.CharacterAdded:connect(function(Character)
    -- listen for death
	setupkilltagger(Character)
    end)
end)

-- This will loop trough all existing dummies inside a folder in worpkspace called TaggedDummies and will set them up.
for i, v in pairs(game.Workspace.TaggedDummies:GetChildren()) do
   setupkilltagger(v)
end
-- This will setup any dummy that might get added in the future, make sure its actually a character with a humanoid.
game.Workspace.TaggedDummies.ChildAdded:Connect(function(v)
    setupkilltagger(v)
end)
```

### **Client setup (optional)**
If you wish the player to be notified of any kill infractions then follow the instructions below.
