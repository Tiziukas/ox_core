Contents for secondary testing resource, using `@ox_core/imports.lua`

```lua
local function test(player)
	if player then
		print(json.encode(player, {indent=true}))
		print(vec3(player.getCoords()))

		local playerState = player.state

		local police = GlobalState['group:police']
		print(police.label, police.ranks[playerState.police])

		local ox = GlobalState['group:ox']
		print(ox.label, ox.ranks[playerState.ox])

		player.setGroup('police', math.random(0, 1))
		player.setGroup('ox', math.random(0, 4))

		print(json.encode(player.getGroups(), {indent=true}))
	end
end

AddEventHandler('ox:playerLoaded', function(source, userid, charid)
    test(Ox.Player(source))
end)

CreateThread(function()
	local players = exports.ox_core:getPlayers()

	for _, player in pairs(players) do
		return test(Ox.Player(player.source))
	end
end)
```
