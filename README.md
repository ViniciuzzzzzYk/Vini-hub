-- Roblox FPS Hack Menu with GUI, Aimbot, ESP, Speed Boost, and Minimizable Menu
-- WARNING: Use at your own risk. This script is for educational purposes only.

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local Camera = workspace.CurrentCamera

-- Settings
local AimbotEnabled = false
local ESPEnabled = false
local SpeedBoostEnabled = false
local SpeedBoostValue = 50 -- default walk speed when speed boost is enabled
local NormalSpeed = 16 -- default Roblox walk speed

-- Create ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "HackMenuGui"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.CoreGui

-- Main Frame
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 300, 0, 350)
MainFrame.Position = UDim2.new(0.05, 0, 0.2, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BorderSizePixel = 0
MainFrame.Parent = ScreenGui
MainFrame.Visible = true

-- UI Corner for rounded edges
local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 10)
UICorner.Parent = MainFrame

-- Title
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "Roblox FPS Hack Menu"
Title.TextColor3 = Color3.new(1,1,1)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 24
Title.Parent = MainFrame

-- Minimize Button
local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Name = "MinimizeButton"
MinimizeButton.Size = UDim2.new(0, 40, 0, 40)
MinimizeButton.Position = UDim2.new(1, -45, 0, 0)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
MinimizeButton.Text = "-"
MinimizeButton.TextColor3 = Color3.new(1,1,1)
MinimizeButton.Font = Enum.Font.SourceSansBold
MinimizeButton.TextSize = 28
MinimizeButton.Parent = MainFrame

local MinimizedIcon = Instance.new("TextButton")
MinimizedIcon.Name = "MinimizedIcon"
MinimizedIcon.Size = UDim2.new(0, 50, 0, 50)
MinimizedIcon.Position = UDim2.new(0, 10, 0, 10)
MinimizedIcon.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MinimizedIcon.Text = "☰"
MinimizedIcon.TextColor3 = Color3.new(1,1,1)
MinimizedIcon.Font = Enum.Font.SourceSansBold
MinimizedIcon.TextSize = 30
MinimizedIcon.Visible = false
MinimizedIcon.Parent = ScreenGui

local UICornerIcon = Instance.new("UICorner")
UICornerIcon.CornerRadius = UDim.new(0, 10)
UICornerIcon.Parent = MinimizedIcon

-- Toggles and Buttons
local function createToggle(name, position, initialState)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, -20, 0, 40)
    frame.Position = position
    frame.BackgroundTransparency = 1
    frame.Parent = MainFrame

    local label = Instance.new("TextLabel")
    label.Text = name
    label.Size = UDim2.new(0.7, 0, 1, 0)
    label.BackgroundTransparency = 1
    label.TextColor3 = Color3.new(1,1,1)
    label.Font = Enum.Font.SourceSans
    label.TextSize = 20
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = frame

    local toggle = Instance.new("TextButton")
    toggle.Size = UDim2.new(0, 60, 0, 30)
    toggle.Position = UDim2.new(0.75, 0, 0.15, 0)
    toggle.BackgroundColor3 = initialState and Color3.fromRGB(0, 170, 0) or Color3.fromRGB(170, 0, 0)
    toggle.Text = initialState and "ON" or "OFF"
    toggle.TextColor3 = Color3.new(1,1,1)
    toggle.Font = Enum.Font.SourceSansBold
    toggle.TextSize = 18
    toggle.Parent = frame

    return toggle
end

local aimbotToggle = createToggle("Aimbot", UDim2.new(0, 10, 0, 60), AimbotEnabled)
local espToggle = createToggle("ESP", UDim2.new(0, 10, 0, 110), ESPEnabled)
local speedToggle = createToggle("Speed Boost", UDim2.new(0, 10, 0, 160), SpeedBoostEnabled)

-- Speed Slider
local speedLabel = Instance.new("TextLabel")
speedLabel.Text = "Speed Value"
speedLabel.Size = UDim2.new(0, 100, 0, 30)
speedLabel.Position = UDim2.new(0, 10, 0, 210)
speedLabel.BackgroundTransparency = 1
speedLabel.TextColor3 = Color3.new(1,1,1)
speedLabel.Font = Enum.Font.SourceSans
speedLabel.TextSize = 18
speedLabel.Parent = MainFrame

local speedValueLabel = Instance.new("TextLabel")
speedValueLabel.Text = tostring(SpeedBoostValue)
speedValueLabel.Size = UDim2.new(0, 40, 0, 30)
speedValueLabel.Position = UDim2.new(0, 120, 0, 210)
speedValueLabel.BackgroundTransparency = 1
speedValueLabel.TextColor3 = Color3.new(1,1,1)
speedValueLabel.Font = Enum.Font.SourceSansBold
speedValueLabel.TextSize = 18
speedValueLabel.Parent = MainFrame

local speedSlider = Instance.new("TextBox")
speedSlider.Size = UDim2.new(0, 100, 0, 30)
speedSlider.Position = UDim2.new(0, 170, 0, 210)
speedSlider.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
speedSlider.TextColor3 = Color3.new(1,1,1)
speedSlider.Font = Enum.Font.SourceSans
speedSlider.TextSize = 18
speedSlider.Text = tostring(SpeedBoostValue)
speedSlider.ClearTextOnFocus = false
speedSlider.Parent = MainFrame

-- Functions for toggles
aimbotToggle.MouseButton1Click:Connect(function()
    AimbotEnabled = not AimbotEnabled
    aimbotToggle.BackgroundColor3 = AimbotEnabled and Color3.fromRGB(0, 170, 0) or Color3.fromRGB(170, 0, 0)
    aimbotToggle.Text = AimbotEnabled and "ON" or "OFF"
end)

espToggle.MouseButton1Click:Connect(function()
    ESPEnabled = not ESPEnabled
    espToggle.BackgroundColor3 = ESPEnabled and Color3.fromRGB(0, 170, 0) or Color3.fromRGB(170, 0, 0)
    espToggle.Text = ESPEnabled and "ON" or "OFF"
end)

speedToggle.MouseButton1Click:Connect(function()
    SpeedBoostEnabled = not SpeedBoostEnabled
    speedToggle.BackgroundColor3 = SpeedBoostEnabled and Color3.fromRGB(0, 170, 0) or Color3.fromRGB(170, 0, 0)
    speedToggle.Text = SpeedBoostEnabled and "ON" or "OFF"
    if not SpeedBoostEnabled then
        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
            LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = NormalSpeed
        end
    end
end)

speedSlider.FocusLost:Connect(function(enterPressed)
    local val = tonumber(speedSlider.Text)
    if val and val >= 16 and val <= 200 then
        SpeedBoostValue = val
        speedValueLabel.Text = tostring(SpeedBoostValue)
        if SpeedBoostEnabled and LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
            LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = SpeedBoostValue
        end
    else
        speedSlider.Text = tostring(SpeedBoostValue)
    end
end)

-- Minimize and maximize functions
MinimizeButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    MinimizedIcon.Visible = true
end)

MinimizedIcon.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    MinimizedIcon.Visible = false
end)

-- Aimbot function tailored for Unnamed Shooter game
local function getClosestTarget()
    local closestPlayer = nil
    local shortestDistance = math.huge
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.Health > 0 then
            -- Target Head or UpperTorso for Unnamed Shooter
            local targetPart = player.Character:FindFirstChild("Head") or player.Character:FindFirstChild("UpperTorso")
            if targetPart then
                local screenPos, onScreen = Camera:WorldToViewportPoint(targetPart.Position)
                if onScreen then
                    local mousePos = Vector2.new(Mouse.X, Mouse.Y)
                    local dist = (Vector2.new(screenPos.X, screenPos.Y) - mousePos).Magnitude
                    if dist < shortestDistance then
                        shortestDistance = dist
                        closestPlayer = player
                    end
                end
            end
        end
    end
    return closestPlayer
end

-- ESP Setup tailored for Unnamed Shooter game
local espBoxes = {}

local function createEspBox(player)
    local box = Drawing.new("Square")
    box.Visible = false
    box.Color = Color3.new(1, 0, 0)
    box.Thickness = 2
    box.Transparency = 1
    box.Filled = false
    return box
end

local function updateEsp()
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.Health > 0 then
            -- Use UpperTorso or HumanoidRootPart for ESP box position
            local targetPart = player.Character:FindFirstChild("UpperTorso") or player.Character:FindFirstChild("HumanoidRootPart")
            if targetPart then
                local screenPos, onScreen = Camera:WorldToViewportPoint(targetPart.Position)
                if onScreen then
                    local box = espBoxes[player]
                    if not box then
                        box = createEspBox(player)
                        espBoxes[player] = box
                    end
                    local size = 50
                    box.Position = Vector2.new(screenPos.X - size/2, screenPos.Y - size/2)
                    box.Size = Vector2.new(size, size)
                    box.Visible = ESPEnabled
                elseif espBoxes[player] then
                    espBoxes[player].Visible = false
                end
            end
        elseif espBoxes[player] then
            espBoxes[player].Visible = false
        end
    end
end

-- Main loop
RunService.RenderStepped:Connect(function()
    -- Aimbot
    if AimbotEnabled then
        local target = getClosestTarget()
        if target and target.Character and target.Character:FindFirstChild("Head") then
            local headPos = target.Character.Head.Position
            Camera.CFrame = CFrame.new(Camera.CFrame.Position, headPos)
        end
    end

    -- Speed Boost
    if SpeedBoostEnabled and LocalPlayer.Character and LocalPlayer.Character:FindFirstChildOfClass("Humanoid") then
        LocalPlayer.Character:FindFirstChildOfClass("Humanoid").WalkSpeed = SpeedBoostValue
    end

    -- ESP
    updateEsp()
end)

-- Responsive GUI scaling
local function onResize()
    local screenSize = workspace.CurrentCamera.ViewportSize
    MainFrame.Size = UDim2.new(0, math.clamp(screenSize.X * 0.3, 250, 400), 0, math.clamp(screenSize.Y * 0.5, 300, 450))
    MinimizedIcon.Position = UDim2.new(0, 10, 0, screenSize.Y - 60)
end

workspace.CurrentCamera:GetPropertyChangedSignal("ViewportSize"):Connect(onResize)
onResize()

-- Anti-cheat bypass note:
-- This script uses basic techniques and obfuscation is recommended for better bypass.
-- Use with caution and test in your environment.

print("Roblox FPS Hack Menu loaded.")
