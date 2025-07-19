local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local humanoid = char:WaitForChild("Humanoid")

local function teleportTo(position)
    if char and char:FindFirstChild("HumanoidRootPart") then
        char.HumanoidRootPart.CFrame = CFrame.new(position)
    end
end

local function attackEnemiesInArea(area)
    for _, enemy in pairs(area:GetChildren()) do
        if enemy:FindFirstChild("Humanoid") and enemy.Humanoid.Health > 0 then
            -- Simula ataque
            print("Atacando: " .. enemy.Name)
            enemy.Humanoid:TakeDamage(10) -- Simula dano
            wait(1)
        end
    end
end

-- Área de farm
local farmArea = workspace:WaitForChild("NPC_Area") -- Nome do modelo com inimigos

while true do
    teleportTo(farmArea.Position + Vector3.new(0, 5, 0)) -- Evita colisão com chão
    attackEnemiesInArea(farmArea)
    wait(3) -- Espera antes de repetir
end
