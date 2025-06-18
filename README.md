-- Galaxy Hub - Blox Fruits (Completo)
-- Feito por Galaxy Team

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("🌌 Galaxy Hub", "Midnight")

-- Variáveis de controle
local AutoFarm = false
local AutoHaki = false
local AutoMission = false
local AutoStoreFruit = false
local FPSBoost = false

-- Funções
function StartAutoFarm()
    while AutoFarm do
        wait(1)
        -- Substitua com lógica real do Auto Farm
        print("Auto Farm ativo...")
    end
end

function StartAutoHaki()
    while AutoHaki do
        wait(1)
        local plyr = game.Players.LocalPlayer
        if plyr.Character:FindFirstChild("HumanoidRootPart") then
            game:GetService("ReplicatedStorage").Remotes.Combat:FireServer("ToggleBuso")
        end
    end
end

function StartAutoMission()
    while AutoMission do
        wait(1)
        -- Código de auto missão
        print("Auto Missão ativa...")
    end
end

function StartAutoStoreFruit()
    while AutoStoreFruit do
        wait(3)
        local args = {
            [1] = "StoreFruit",
            [2] = game:GetService("Players").LocalPlayer.Data.DevilFruit.Value
        }
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
end

function RunFPSBoost()
    if FPSBoost then
        sethiddenproperty(game:GetService("Lighting"), "Technology", Enum.Technology.Compatibility)
        game:GetService("Lighting").GlobalShadows = false
        game:GetService("Lighting").FogEnd = 100000
        game:GetService("Workspace").Terrain.WaterWaveSize = 0
        game:GetService("Workspace").Terrain.WaterWaveSpeed = 0
        game:GetService("Workspace").Terrain.WaterReflectance = 0
        game:GetService("Workspace").Terrain.WaterTransparency = 1
        print("FPS Boost ativado.")
    end
end

-- Abas do menu
local TabFarm = Window:NewTab("Farm")
local TabCombat = Window:NewTab("Combate")
local TabExtras = Window:NewTab("Extras")

local SectionFarm = TabFarm:NewSection("Farm")
SectionFarm:NewToggle("Auto Farm", "Farm automático de inimigos", function(value)
    AutoFarm = value
    if value then
        spawn(StartAutoFarm)
    end
end)

SectionFarm:NewToggle("Auto Missão", "Aceita missões automaticamente", function(value)
    AutoMission = value
    if value then
        spawn(StartAutoMission)
    end
end)

local SectionCombat = TabCombat:NewSection("Combate")
SectionCombat:NewToggle("Auto Haki", "Ativa o Haki automaticamente", function(value)
    AutoHaki = value
    if value then
        spawn(StartAutoHaki)
    end
end)

local SectionExtras = TabExtras:NewSection("Extras")
SectionExtras:NewToggle("Auto Store Fruit", "Armazena fruta automaticamente", function(value)
    AutoStoreFruit = value
    if value then
        spawn(StartAutoStoreFruit)
    end
end)

SectionExtras:NewButton("FPS Boost", "Aumenta o desempenho", function()
    FPSBoost = true
    RunFPSBoost()
end)

print("Galaxy Hub carregado com sucesso.")
