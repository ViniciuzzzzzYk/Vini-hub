-- VEX HUB - Um hub universal para Roblox
-- Desenvolvido com abas e funcionalidades específicas para diferentes jogos

-- Serviços principais
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

-- Criar GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "VEXHub"
ScreenGui.Parent = game.CoreGui

-- Configuração da Interface
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 300, 0, 400)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BorderSizePixel = 0
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 10)
UICorner.Parent = MainFrame

-- Título
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "VEX HUB"
Title.Font = Enum.Font.GothamBold
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(0, 255, 0)
Title.Parent = MainFrame

-- Abas
local TabContainer = Instance.new("Frame")
TabContainer.Size = UDim2.new(0, 100, 1, -40)
TabContainer.Position = UDim2.new(0, 0, 0, 40)
TabContainer.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
TabContainer.Parent = MainFrame

local UniversalTab = Instance.new("Frame")
UniversalTab.Size = UDim2.new(1, -100, 1, -40)
UniversalTab.Position = UDim2.new(0, 100, 0, 40)
UniversalTab.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
UniversalTab.Visible = true
UniversalTab.Parent = MainFrame

local GunfightTab = Instance.new("Frame")
GunfightTab.Size = UDim2.new(1, -100, 1, -40)
GunfightTab.Position = UDim2.new(0, 100, 0, 40)
GunfightTab.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
GunfightTab.Visible = false
GunfightTab.Parent = MainFrame

local BuildTab = Instance.new("Frame")
BuildTab.Size = UDim2.new(1, -100, 1, -40)
BuildTab.Position = UDim2.new(0, 100, 0, 40)
BuildTab.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
BuildTab.Visible = false
BuildTab.Parent = MainFrame

-- Função para alternar abas
local function switchTabs(tab)
    UniversalTab.Visible = false
    GunfightTab.Visible = false
    BuildTab.Visible = false
    tab.Visible = true
end

-- Botões das abas
local function createTabButton(name, tab)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, 0, 0, 40)
    btn.Text = name
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 16
    btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Parent = TabContainer

    btn.MouseButton1Click:Connect(function()
        switchTabs(tab)
    end)

    return btn
end

createTabButton("Universal", UniversalTab)
createTabButton("Gunfight", GunfightTab)
createTabButton("Build a Boat", BuildTab)

-- Funções Universais
local function toggleFly()
    -- Código para Fly
end

local function toggleESP()
    -- Código para ESP
end

local function toggleWallClip()
    -- Código para atravessar paredes
end

-- Funções Gunfight Arena
local function toggleAimbot()
    -- Código para Aimbot
end

local function toggleHitbox()
    -- Código para aumentar Hitbox
end

-- Funções Build a Boat
local function autoFarm()
    -- Código para Auto Farm
end

-- Botões (Exemplo Universal)
local FlyButton = Instance.new("TextButton")
FlyButton.Size = UDim2.new(1, 0, 0, 40)
FlyButton.Text = "Toggle Fly"
FlyButton.Font = Enum.Font.Gotham
FlyButton.TextSize = 16
FlyButton.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
FlyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
FlyButton.Parent = UniversalTab
FlyButton.MouseButton1Click:Connect(toggleFly)

-- Outras funcionalidades seguem o mesmo padrão
