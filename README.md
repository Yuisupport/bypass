game:GetService("ScriptContext"):SetTimeout(0.1)

local Player = game.Players.LocalPlayer
local Character = Player.Character
local StarterScript = game.StarterPlayer.StarterCharacterScripts:WaitForChild("Anticheat")
function findscriptconnection(connection, scr)
    local connections = getconnections(connection)
    local scrconnection = nil
    for _, tbl in next, connections do
        local env = getfenv(tbl.Function)
        for _, val in next, env do
            if val == scr then
                scrconnection = tbl
                break
            end
        end
    end
    return scrconnection
end

if not shared.bypassed then
    local gmt = getrawmetatable(game)
    local oldnamecall = gmt.__namecall
    local oldindex = gmt.__index
    local oldnewindex = gmt.__newindex
    setreadonly(gmt, false)
    local s = Instance.new("Hint", workspace)
    s.Text = "Made by zxcazz..."
    local t = findscriptconnection(game.Players.LocalPlayer.CharacterAdded, game.Players.LocalPlayer.PlayerScripts.Client)
    t:Disable()
    Player.CharacterAdded:Connect(function()
        local char = Player.Character or Player.CharacterAdded:Wait()

        if char:FindFirstChild("Anticheat") then
            local a = char:FindFirstChild("Anticheat")
            a.Disabled = true
        end
        char.ChildAdded:Connect(function(obj)
            if obj.Name == "Anticheat" then
                obj.Disabled = true
            end
        end)
    end)
	
	 local char = Player.Character or Player.CharacterAdded:Wait()

        if char:FindFirstChild("Anticheat") then
            local a = char:FindFirstChild("Anticheat")
            a.Disabled = true
        end
        char.ChildAdded:Connect(function(obj)
            if obj.Name == "Anticheat" then
                obj.Disabled = true
            end
        end)

    gmt.__namecall = newcclosure(function(self, ...)
        local method = getnamecallmethod()
        if method == "FireServer" then
            if tostring(self):lower() == "2event" then
                return wait(9e9)
            end
        elseif method == "Kick" and self == Player then
            return wait(9e9)
        end
        return oldnamecall(self, ...)
    end)
    gmt.__index = newcclosure(function(self, key, value, ...)
        if key == "Enabled" and self.Name == "Anticheat" then return false end
        return oldindex(self, key, value, ...)
    end)
    gmt.__newindex = newcclosure(function(self, key, value,...)
        if key == "Enabled" and self.Name == "Anticheat" then return wait(9e9) end
        return oldnewindex(self, key, value, ...)
    end)


    s.Text = "reach bypassed be lol"
    shared.bypassed = true
    game.Debris:AddItem(s, 5)
end
--/ Services
function serv(n)
    return game:service(n)
end
