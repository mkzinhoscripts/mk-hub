repeat wait() until game:IsLoaded()

local player = game.Players.LocalPlayer  
local char = player.Character or player.CharacterAdded:Wait()
local hrp = char:WaitForChild("HumanoidRootPart")  

-- Função de Auto Farm (Ataca inimigos automaticamente)
function autoFarm()
    while wait(0.5) do
        for _, mob in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
            if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 then
                hrp.CFrame = mob.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)  
                wait(0.2)
                game:GetService("VirtualUser"):Button1Down(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
            end
        end
    end
end

-- Função de Auto TTK (Se já tiver as 3 espadas, pega a True Triple Katana)
function autoTTK()
    local swords = {"Shisui", "Wando", "Saddi"}
    local owned = 0
    for _, sword in ipairs(swords) do
        if player.Backpack:FindFirstChild(sword) or char:FindFirstChild(sword) then
            owned = owned + 1
        end
    end
    if owned == 3 then
        hrp.CFrame = CFrame.new(-4732, 872, -1932) -- Posição do NPC que dá a TTK
        wait(2)
        fireclickdetector(game.Workspace.NPCs["TTK Dealer"].ClickDetector)
    end
end

-- Função de Auto Haki V2 (Vai até o NPC do Haki V2 e interage)
function autoHakiV2()
    hrp.CFrame = CFrame.new(-958, 38, 5543) -- Coordenadas do NPC do Haki V2
    wait(2)
    fireclickdetector(game.Workspace.NPCs["Haki Master"].ClickDetector)
end

-- Função de Auto Farm Haki (Ataca mobs para upar o Haki)
function autoFarmHaki()
    while wait(0.5) do
        for _, mob in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
            if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 then
                hrp.CFrame = mob.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)  
                wait(0.2)
                game:GetService("VirtualUser"):Button1Down(Vector2.new(0, 0), workspace.CurrentCamera.CFrame)
            end
        end
    end
end

-- Ativa todas as funções automaticamente
spawn(autoFarm)
spawn(autoTTK)
spawn(autoHakiV2)
spawn(autoFarmHaki)
