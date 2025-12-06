-- 🌌 Cosmic Hub - Brookhaven Mobile Edition
-- 🚀 Versão: 2.0 Purple
-- 📱 Otimizado para Mobile
-- 💜 Tema Roxo Cosmic

-- Configurações do Cosmic Hub
local Cosmic = {
    AutoFarm = false,
    CollectMoney = true,
    CollectCrates = true,
    CollectGifts = true,
    AutoJob = false,
    JobType = "Pizza Delivery",
    WalkSpeed = 20,
    JumpPower = 50,
    AntiAFK = true,
    Notifications = true,
    ThemeColor = Color3.fromRGB(157, 78, 221), -- Roxo Cosmic
    RainbowMode = false
}

-- Variáveis
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")
local TeleportService = game:GetService("TeleportService")

-- Verificar dispositivo
local IS_MOBILE = (game:GetService("UserInputService").TouchEnabled == true)
local IS_TABLET = (game:GetService("UserInputService").KeyboardEnabled == false)

-- Sistema de notificações mobile-friendly
function CosmicNotify(Title, Message, Duration)
    if Cosmic.Notifications then
        game.StarterGui:SetCore("SendNotification", {
            Title = "💜 " .. Title,
            Text = Message,
            Duration = Duration or 3,
            Icon = "rbxassetid://4483345998"
        })
    end
    
    -- Log no console para mobile
    print("💜 COSMIC HUB: " .. Title .. " - " .. Message)
end

-- Interface mobile simplificada
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "CosmicHubMobile"
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = game.CoreGui

-- Botão flutuante para mobile
local FloatingButton = Instance.new("TextButton")
FloatingButton.Name = "CosmicMenuButton"
FloatingButton.Size = UDim2.new(0, 60, 0, 60)
FloatingButton.Position = UDim2.new(1, -70, 1, -70)
FloatingButton.BackgroundColor3 = Cosmic.ThemeColor
FloatingButton.Text = "🌌"
FloatingButton.TextSize = 24
FloatingButton.Font = Enum.Font.GothamBold
FloatingButton.TextColor3 = Color3.fromRGB(255, 255, 255)
FloatingButton.BorderSizePixel = 0
FloatingButton.AutoButtonColor = false
FloatingButton.Parent = ScreenGui

-- Arredondar botão
local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(1, 0)
UICorner.Parent = FloatingButton

-- Efeito de sombra
local UIStroke = Instance.new("UIStroke")
UIStroke.Color = Color3.fromRGB(255, 255, 255)
UIStroke.Thickness = 2
UIStroke.Parent = FloatingButton

-- Menu principal mobile
local MainFrame = Instance.new("Frame")
MainFrame.Name = "CosmicMenu"
MainFrame.Size = UDim2.new(0, 300, 0, 400)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
MainFrame.Visible = false
MainFrame.Parent = ScreenGui

local UICorner2 = Instance.new("UICorner")
UICorner2.CornerRadius = UDim.new(0, 12)
UICorner2.Parent = MainFrame

-- Header do menu
local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 60)
Header.BackgroundColor3 = Cosmic.ThemeColor
Header.Parent = MainFrame

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 12)
HeaderCorner.Parent = Header

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 1, 0)
Title.Text = "🌌 COSMIC HUB"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 20
Title.BackgroundTransparency = 1
Title.Parent = Header

local Subtitle = Instance.new("TextLabel")
Subtitle.Size = UDim2.new(1, 0, 0, 20)
Subtitle.Position = UDim2.new(0, 0, 0, 35)
Subtitle.Text = "Brookhaven Mobile Edition"
Subtitle.TextColor3 = Color3.fromRGB(200, 200, 200)
Subtitle.Font = Enum.Font.Gotham
Subtitle.TextSize = 14
Subtitle.BackgroundTransparency = 1
Subtitle.Parent = Header

-- Container de botões
local ButtonsContainer = Instance.new("ScrollingFrame")
ButtonsContainer.Size = UDim2.new(1, -20, 1, -80)
ButtonsContainer.Position = UDim2.new(0, 10, 0, 70)
ButtonsContainer.BackgroundTransparency = 1
ButtonsContainer.BorderSizePixel = 0
ButtonsContainer.ScrollBarThickness = 4
ButtonsContainer.Parent = MainFrame

-- Fechar botão
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 40, 0, 40)
CloseButton.Position = UDim2.new(1, -50, 0, 10)
CloseButton.Text = "✕"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.GothamBold
CloseButton.TextSize = 20
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 60, 60)
CloseButton.Parent = Header

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(1, 0)
CloseCorner.Parent = CloseButton

-- Status label
local StatusLabel = Instance.new("TextLabel")
StatusLabel.Size = UDim2.new(1, -20, 0, 40)
StatusLabel.Position = UDim2.new(0, 10, 0, 10)
StatusLabel.Text = "Status: Pronto"
StatusLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
StatusLabel.Font = Enum.Font.Gotham
StatusLabel.TextSize = 16
StatusLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
StatusLabel.Parent = ButtonsContainer

local StatusCorner = Instance.new("UICorner")
StatusCorner.CornerRadius = UDim.new(0, 8)
StatusCorner.Parent = StatusLabel

-- Função para criar botões mobile
function CreateMobileButton(Text, Callback)
    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(1, 0, 0, 50)
    Button.Text = Text
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.Font = Enum.Font.Gotham
    Button.TextSize = 16
    Button.BackgroundColor3 = Cosmic.ThemeColor
    Button.AutoButtonColor = true
    
    local ButtonCorner = Instance.new("UICorner")
    ButtonCorner.CornerRadius = UDim.new(0, 8)
    ButtonCorner.Parent = Button
    
    Button.MouseButton1Click:Connect(function()
        Callback()
    end)
    
    return Button
end

-- Adicionar botões ao menu
local AutoFarmBtn = CreateMobileButton("🚀 INICIAR AUTO FARM", function()
    Cosmic.AutoFarm = not Cosmic.AutoFarm
    if Cosmic.AutoFarm then
        StatusLabel.Text = "Status: Auto Farm ATIVADO"
        StatusLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
        CosmicNotify("AUTO FARM", "Sistema ativado!", 3)
        StartCosmicFarm()
    else
        StatusLabel.Text = "Status: Auto Farm DESATIVADO"
        StatusLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
        CosmicNotify("AUTO FARM", "Sistema desativado!", 3)
    end
end)

local CollectMoneyBtn = CreateMobileButton("💰 COLETAR DINHEIRO", function()
    CosmicCollectMoney()
end)

local CollectAllBtn = CreateMobileButton("🎁 COLETAR TUDO", function()
    CosmicCollectAll()
end)

local TPHouseBtn = CreateMobileButton("🏠 TELEPORTAR CASA", function()
    CosmicTPHouse()
end)

local TPShopBtn = CreateMobileButton("🛒 TELEPORTAR LOJA", function()
    CosmicTPShop()
end)

local SpeedBtn = CreateMobileButton("⚡ VELOCIDADE (20)", function()
    Cosmic.WalkSpeed = 20
    if Character and Character:FindFirstChild("Humanoid") then
        Character.Humanoid.WalkSpeed = Cosmic.WalkSpeed
        CosmicNotify("VELOCIDADE", "Ajustada para 20", 2)
    end
end)

local AntiAFKBtn = CreateMobileButton("🔄 ANTI-AFK ON/OFF", function()
    Cosmic.AntiAFK = not Cosmic.AntiAFK
    if Cosmic.AntiAFK then
        ActivateCosmicAntiAFK()
        CosmicNotify("ANTI-AFK", "Ativado!", 2)
    else
        CosmicNotify("ANTI-AFK", "Desativado!", 2)
    end
end)

local CloseMenuBtn = CreateMobileButton("📱 FECHAR MENU", function()
    MainFrame.Visible = false
end)

-- Adicionar botões ao container
local buttons = {AutoFarmBtn, CollectMoneyBtn, CollectAllBtn, TPHouseBtn, TPShopBtn, SpeedBtn, AntiAFKBtn, CloseMenuBtn}
for i, btn in ipairs(buttons) do
    btn.Parent = ButtonsContainer
    btn.Position = UDim2.new(0, 0, 0, (i-1) * 60)
end

ButtonsContainer.CanvasSize = UDim2.new(0, 0, 0, #buttons * 60)

-- Interações
FloatingButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

CloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)

-- Funções Cosmic
function StartCosmicFarm()
    spawn(function()
        while Cosmic.AutoFarm do
            if Cosmic.CollectMoney then
                CosmicCollectMoney()
            end
            if Cosmic.CollectCrates then
                CosmicCollectCrates()
            end
            if Cosmic.CollectGifts then
                CosmicCollectGifts()
            end
            wait(2) -- Intervalo maior para mobile
        end
    end)
end

function CosmicCollectMoney()
    local collected = 0
    for _, obj in pairs(Workspace:GetChildren()) do
        if Cosmic.AutoFarm == false then break end
        
        if obj.Name:lower():find("money") or obj.Name:lower():find("cash") or obj.Name:lower():find("dollar") then
            if obj:IsA("Part") or obj:IsA("MeshPart") then
                local distance = (HumanoidRootPart.Position - obj.Position).Magnitude
                if distance < 150 then
                    -- Tween suave para mobile
                    local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad)
                    local tween = TweenService:Create(HumanoidRootPart, tweenInfo, {CFrame = CFrame.new(obj.Position + Vector3.new(0, 3, 0))})
                    tween:Play()
                    wait(0.6)
                    
                    if obj:FindFirstChild("TouchInterest") then
                        firetouchinterest(HumanoidRootPart, obj, 0)
                        firetouchinterest(HumanoidRootPart, obj, 1)
                    end
                    
                    collected = collected + 1
                    if collected % 5 == 0 then
                        StatusLabel.Text = "Status: Coletado " .. collected .. " itens"
                    end
                end
            end
        end
    end
    
    if collected > 0 then
        CosmicNotify("DINHEIRO", "Coletados " .. collected .. " itens!", 2)
    end
end

function CosmicCollectCrates()
    for _, obj in pairs(Workspace:GetChildren()) do
        if Cosmic.AutoFarm == false then break end
        
        if obj.Name:lower():find("crate") or obj.Name:lower():find("box") or obj.Name:lower():find("gift") then
            if obj:IsA("Part") or obj:IsA("MeshPart") then
                local distance = (HumanoidRootPart.Position - obj.Position).Magnitude
                if distance < 150 then
                    HumanoidRootPart.CFrame = CFrame.new(obj.Position + Vector3.new(0, 3, 0))
                    wait(0.5)
                    
                    if obj:FindFirstChild("TouchInterest") then
                        firetouchinterest(HumanoidRootPart, obj, 0)
                        firetouchinterest(HumanoidRootPart, obj, 1)
                    end
                end
            end
        end
    end
end

function CosmicCollectGifts()
    for _, obj in pairs(Workspace:GetChildren()) do
        if Cosmic.AutoFarm == false then break end
        
        if obj.Name:lower():find("present") or obj.Name:lower():find("gift") or obj.Name:lower():find("package") then
            if obj:IsA("Part") or obj:IsA("MeshPart") then
                local distance = (HumanoidRootPart.Position - obj.Position).Magnitude
                if distance < 150 then
                    HumanoidRootPart.CFrame = CFrame.new(obj.Position + Vector3.new(0, 3, 0))
                    wait(0.5)
                    
                    if obj:FindFirstChild("TouchInterest") then
                        firetouchinterest(HumanoidRootPart, obj, 0)
                        firetouchinterest(HumanoidRootPart, obj, 1)
                    end
                end
            end
        end
    end
end

function CosmicCollectAll()
    CosmicCollectMoney()
    CosmicCollectCrates()
    CosmicCollectGifts()
    CosmicNotify("COLETA", "Todos os itens coletados!", 3)
end

function CosmicTPHouse()
    -- Procurar casa do jogador
    local playerName = LocalPlayer.Name
    local houseFound = false
    
    for _, obj in pairs(Workspace:GetChildren()) do
        if obj.Name:find(playerName) and (obj.Name:find("House") or obj.Name:find("house")) then
            local tweenInfo = TweenInfo.new(1, Enum.EasingStyle.Quad)
            local tween = TweenService:Create(HumanoidRootPart, tweenInfo, {CFrame = CFrame.new(obj.Position + Vector3.new(0, 5, 0))})
            tween:Play()
            houseFound = true
            CosmicNotify("TELEPORT", "Casa encontrada!", 3)
            break
        end
    end
    
    if not houseFound then
        -- Posição padrão de casas
        HumanoidRootPart.CFrame = CFrame.new(500, 10, 500)
        CosmicNotify("TELEPORT", "Teleportado para área residencial", 3)
    end
end

function CosmicTPShop()
    -- Teleportar para área comercial
    HumanoidRootPart.CFrame = CFrame.new(-50, 5, -100)
    CosmicNotify("TELEPORT", "Área comercial", 3)
end

function ActivateCosmicAntiAFK()
    spawn(function()
        while Cosmic.AntiAFK do
            wait(30) -- Intervalo menor para mobile
            
            -- Simular movimento simples
            if Character and Character:FindFirstChild("Humanoid") then
                Character.Humanoid:Move(Vector3.new(1, 0, 0))
                wait(0.1)
                Character.Humanoid:Move(Vector3.new(-1, 0, 0))
            end
        end
    end)
end

-- Sistema de gestos para mobile
if IS_MOBILE then
    local lastTapTime = 0
    local tapCount = 0
    
    game:GetService("UserInputService").TouchTap:Connect(function(touchPositions)
        local currentTime = tick()
        
        if currentTime - lastTapTime < 0.5 then
            tapCount = tapCount + 1
            if tapCount == 3 then
                -- Triple tap para mostrar/esconder menu
                MainFrame.Visible = not MainFrame.Visible
                tapCount = 0
            end
        else
            tapCount = 1
        end
        
        lastTapTime = currentTime
    end)
end

-- Hotkeys para tablets com teclado
if IS_TABLET then
    game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        
        if input.KeyCode == Enum.KeyCode.F then
            Cosmic.AutoFarm = not Cosmic.AutoFarm
            if Cosmic.AutoFarm then
                StartCosmicFarm()
                CosmicNotify("HOTKEY", "Auto Farm ATIVADO", 2)
            else
                CosmicNotify("HOTKEY", "Auto Farm DESATIVADO", 2)
            end
        end
        
        if input.KeyCode == Enum.KeyCode.G then
            CosmicCollectAll()
        end
        
        if input.KeyCode == Enum.KeyCode.H then
            CosmicTPHouse()
        end
        
        if input.KeyCode == Enum.KeyCode.M then
            MainFrame.Visible = not MainFrame.Visible
        end
    end)
end

-- Efeito de pulsação no botão flutuante
spawn(function()
    while wait(2) do
        local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut, 0, true)
        local tween = TweenService:Create(FloatingButton, tweenInfo, {Size = UDim2.new(0, 65, 0, 65)})
        tween:Play()
        wait(0.6)
    end
end)

-- Efeito de cor roxa dinâmica
if Cosmic.RainbowMode then
    spawn(function()
        local hue = 0
        while wait(0.1) do
            hue = (hue + 1) % 360
            local color = Color3.fromHSV(hue/360, 0.8, 0.9)
            FloatingButton.BackgroundColor3 = color
            Header.BackgroundColor3 = color
        end
    end)
end

-- Inicialização
CosmicNotify("COSMIC HUB", "🌌 Brookhaven Mobile v2.0\n💜 Tema Roxo Cosmic\n📱 Otimizado para Mobile", 5)

-- Reconectar quando o personagem morre
LocalPlayer.CharacterAdded:Connect(function(char)
    Character = char
    HumanoidRootPart = char:WaitForChild("HumanoidRootPart")
    
    if char:FindFirstChild("Humanoid") then
        char.Humanoid.WalkSpeed = Cosmic.WalkSpeed
        char.Humanoid.JumpPower = Cosmic.JumpPower
    end
    
    CosmicNotify("PERSONAGEM", "Personagem resetado!", 2)
end)

-- Status inicial
if IS_MOBILE then
    StatusLabel.Text = "Status: Modo Mobile Ativo"
elseif IS_TABLET then
    StatusLabel.Text = "Status: Modo Tablet Ativo"
else
    StatusLabel.Text = "Status: Modo Desktop Detectado"
end

-- Mensagem de boas-vindas
print([[

   _____                      _       _   _     
  / ____|                    | |     | | | |    
 | |     ___  _ __ ___   __ _| |_ ___| |_| |__  
 | |    / _ \| '_ ` _ \ / _` | __/ __| __| '_ \ 
 | |___| (_) | | | | | | (_| | || (__| |_| | | |
  \_____\___/|_| |_| |_|\__,_|\__\___|\__|_| |_|
                                                
💜 COSMIC HUB - Brookhaven Mobile Edition
📱 Otimizado para dispositivos móveis
🚀 Pressione o botão roxo para abrir o menu
🎮 Triple-tap para abrir/ocultar menu (mobile)

]])
