local function aimbot()
    local playerService = game:GetService("Players")
    local localPlayer = playerService.LocalPlayer
    local camera = workspace.CurrentCamera

    game:GetService("RunService").RenderStepped:Connect(function()
        if not aimbotEnabled then return end

        local closestPlayer = nil
        local shortestDistance = math.huge

        for _, player in pairs(playerService:GetPlayers()) do
            if player ~= localPlayer and player.Character and player.Character:FindFirstChild("Humanoid") and player.Character:FindFirstChild("HumanoidRootPart") then
                local humanoid = player.Character.Humanoid
                local rootPart = player.Character.HumanoidRootPart
                local rootPosition = camera:WorldToScreenPoint(rootPart.Position)

                -- Ignorar jogadores mortos
                if humanoid.Health <= 0 then
                    continue
                end
