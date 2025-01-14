local function createESP(player)
    local char = player.Character
    if char and char:FindFirstChild("HumanoidRootPart") then
        local box = Instance.new("Part")
        box.Size = Vector3.new(2, 5, 2)  -- Tamanho da caixa
        box.Position = char.HumanoidRootPart.Position
        box.Anchored = true
        box.CanCollide = false
        box.Transparency = 0.5  -- Opacidade (0.5 para meio transparente)
        box.BrickColor = BrickColor.new("Bright red")  -- Cor da caixa
        box.Parent = workspace
        
        -- Atualiza a posição da caixa
        game:GetService("RunService").Heartbeat:Connect(function()
            if char and char:FindFirstChild("HumanoidRootPart") then
                box.Position = char.HumanoidRootPart.Position
            end
        end)
        
        -- Remover a caixa quando o jogador sair
        player.CharacterRemoving:Connect(function()
            box:Destroy()
        end)
    end
end

-- Criar ESP para todos os jogadores
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        createESP(player)
    end)
end)
