-- Script no ServerScriptService

-- Lista de admins (UserIds)
local admins = {
    [11223344] = true, -- Substitua com seu próprio UserId
}

-- Lista de banidos
local bannedUsers = {}

game.Players.PlayerAdded:Connect(function(player)
    if bannedUsers[player.UserId] then
        player:Kick("Você foi banido deste jogo.")
    end
end)

game.ReplicatedStorage:WaitForChild("BanPlayer").OnServerEvent:Connect(function(sender, targetName)
    if not admins[sender.UserId] then return end

    local targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer then
        bannedUsers[targetPlayer.UserId] = true
        targetPlayer:Kick("Você foi banido por um administrador.")
    end
end)
