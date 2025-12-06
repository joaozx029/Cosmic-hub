-- ============================================
-- 🌌 COSMIC HUB V5.0 - Brookhaven Mobile Edition
-- 🚀 Versão: 5.0 Purple
-- 📱 Otimizado para Mobile
-- 💜 Tema Roxo Cosmic
-- 🔗 Discord: https://discord.gg/cosmichub
-- ============================================

-- ============================================
-- TELA DE CARREGAMENTO
-- ============================================
local LoadingScreen = Instance.new("ScreenGui")
LoadingScreen.Name = "CosmicHubLoading"
LoadingScreen.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
LoadingScreen.IgnoreGuiInset = true
LoadingScreen.Parent = game.CoreGui

-- Fundo com gradiente roxo
local LoadingBackground = Instance.new("Frame")
LoadingBackground.Name = "LoadingBackground"
LoadingBackground.Size = UDim2.new(1, 0, 1, 0)
LoadingBackground.BackgroundColor3 = Color3.fromRGB(10, 10, 20)
LoadingBackground.BorderSizePixel = 0
LoadingBackground.Parent = LoadingScreen

-- Gradiente
local UIGradient = Instance.new("UIGradient")
UIGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(40, 10, 60)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(15, 15, 25))
}
UIGradient.Rotation = 45
UIGradient.Parent = LoadingBackground

-- Logo Cosmic Hub
local CosmicLogo = Instance.new("TextLabel")
CosmicLogo.Name = "CosmicLogo"
CosmicLogo.Size = UDim2.new(0, 400, 0, 100)
CosmicLogo.Position = UDim2.new(0.5, -200, 0.25, -50)
CosmicLogo.Text = "🌌 COSMIC HUB"
CosmicLogo.TextColor3 = Color3.fromRGB(157, 78, 221)
CosmicLogo.Font = Enum.Font.GothamBlack
CosmicLogo.TextSize = 48
CosmicLogo.BackgroundTransparency = 1
CosmicLogo.TextStrokeTransparency = 0.7
CosmicLogo.TextStrokeColor3 = Color3.fromRGB(255, 255, 255)
CosmicLogo.Parent = LoadingBackground

local VersionText = Instance.new("TextLabel")
VersionText.Name = "VersionText"
VersionText.Size = UDim2.new(0, 300, 0, 30)
VersionText.Position = UDim2.new(0.5, -150, 0.25, 60)
VersionText.Text = "V5.0 - Brookhaven Mobile Edition"
VersionText.TextColor3 = Color3.fromRGB(200, 200, 255)
VersionText.Font = Enum.Font.Gotham
VersionText.TextSize = 18
VersionText.BackgroundTransparency = 1
VersionText.Parent = LoadingBackground

-- Barra de progresso
local ProgressContainer = Instance.new("Frame")
ProgressContainer.Name = "ProgressContainer"
ProgressContainer.Size = UDim2.new(0, 350, 0, 30)
ProgressContainer.Position = UDim2.new(0.5, -175, 0.5, -15)
ProgressContainer.BackgroundColor3 = Color3.fromRGB(30, 30, 45)
ProgressContainer.BorderSizePixel = 0
ProgressContainer.Parent = LoadingBackground

local UICornerProgress = Instance.new("UICorner")
UICornerProgress.CornerRadius = UDim.new(0, 15)
UICornerProgress.Parent = ProgressContainer

local ProgressBar = Instance.new("Frame")
ProgressBar.Name = "ProgressBar"
ProgressBar.Size = UDim2.new(0, 0, 1, 0)
ProgressBar.BackgroundColor3 = Color3.fromRGB(157, 78, 221)
ProgressBar.BorderSizePixel = 0
ProgressBar.Parent = ProgressContainer

local UICornerProgressFill = Instance.new("UICorner")
UICornerProgressFill.CornerRadius = UDim.new(0, 15)
UICornerProgressFill.Parent = ProgressBar

-- Texto de progresso
local ProgressText = Instance.new("TextLabel")
ProgressText.Name = "ProgressText"
ProgressText.Size = UDim2.new(0, 350, 0, 25)
ProgressText.Position = UDim2.new(0.5, -175, 0.5, 25)
ProgressText.Text = "Inicializando... 0%"
ProgressText.TextColor3 = Color3.fromRGB(220, 220, 255)
ProgressText.Font = Enum.Font.GothamMedium
ProgressText.TextSize = 16
ProgressText.BackgroundTransparency = 1
ProgressText.Parent = LoadingBackground

-- Status
local StatusText = Instance.new("TextLabel")
StatusText.Name = "StatusText"
StatusText.Size = UDim2.new(0, 400, 0, 30)
StatusText.Position = UDim2.new(0.5, -200, 0.5, 60)
StatusText.Text = "Carregando módulos..."
StatusText.TextColor3 = Color3.fromRGB(180, 140, 255)
StatusText.Font = Enum.Font.Gotham
StatusText.TextSize = 14
StatusText.BackgroundTransparency = 1
StatusText.Parent = LoadingBackground

-- Créditos
local CreditsText = Instance.new("TextLabel")
CreditsText.Name = "CreditsText"
CreditsText.Size = UDim2.new(0, 400, 0, 60)
CreditsText.Position = UDim2.new(0.5, -200, 0.75, -30)
CreditsText.Text = "💜 Desenvolvido por Cosmic Team\n🌐 Discord: discord.gg/cosmichub"
CreditsText.TextColor3 = Color3.fromRGB(150, 150, 200)
CreditsText.Font = Enum.Font.Gotham
CreditsText.TextSize = 14
CreditsText.TextWrapped = true
CreditsText.BackgroundTransparency = 1
CreditsText.Parent = LoadingBackground

-- Dicas rotativas
local Tips = {
    "💡 Dica: Use VPN se o ping estiver alto!",
    "🎮 Modo mobile otimizado para touch!",
    "🚀 Auto Farm para farm mais rápido!",
    "💜 Tema roxo cosmic exclusivo!",
    "📱 Triple-tap para abrir menu rápido!"
}

local TipText = Instance.new("TextLabel")
TipText.Name = "TipText"
TipText.Size = UDim2.new(0, 450, 0, 40)
TipText.Position = UDim2.new(0.5, -225, 0.9, -20)
TipText.Text = Tips[1]
TipText.TextColor3 = Color3.fromRGB(120, 120, 180)
TipText.Font = Enum.Font.Gotham
TipText.TextSize = 14
TipText.TextWrapped = true
TipText.BackgroundTransparency = 1
TipText.Parent = LoadingBackground

-- Função de atualização de progresso
local CurrentProgress = 0
local function UpdateProgress(percent, status)
    CurrentProgress = percent
    local tweenInfo = TweenInfo.new(0.3, Enum.EasingStyle.Quad)
    local tween = game:GetService("TweenService"):Create(ProgressBar, tweenInfo, 
        {Size = UDim2.new(percent/100, 0, 1, 0)})
    tween:Play()
    
    ProgressText.Text = string.format("%s %d%%", status, percent)
    StatusText.Text = status
    
    -- Efeito de partícula
    if percent % 20 == 0 then
        local particle = Instance.new("TextLabel")
        particle.Size = UDim2.new(0, 30, 0, 30)
        particle.Position = UDim2.new(math.random(), -15, 0.25, -15)
        particle.Text = "✨"
        particle.TextSize = 24
        particle.BackgroundTransparency = 1
        particle.TextColor3 = Color3.fromRGB(157, 78, 221)
        particle.Parent = LoadingBackground
        
        spawn(function()
            for i = 1, 30 do
                particle.TextTransparency = i/30
                particle.Position = particle.Position + UDim2.new(0, 0, 0, -2)
                wait(0.03)
            end
            particle:Destroy()
        end)
    end
end

-- Rotação de dicas
spawn(function()
    local tipIndex = 1
    while LoadingScreen.Parent do
        wait(5)
        tipIndex = tipIndex + 1
        if tipIndex > #Tips then tipIndex = 1 end
        TipText.Text = Tips[tipIndex]
        
        -- Efeito de fade
        TipText.TextTransparency = 1
        local tween = game:GetService("TweenService"):Create(TipText, 
            TweenInfo.new(0.5), {TextTransparency = 0})
        tween:Play()
    end
end)

-- Animação do logo
spawn(function()
    while LoadingScreen.Parent do
        CosmicLogo.TextColor3 = Color3.fromRGB(157, 78, 221)
        wait(1)
        CosmicLogo.TextColor3 = Color3.fromRGB(180, 100, 255)
        wait(1)
    end
end)

-- Iniciar carregamento
UpdateProgress(5, "Verificando ambiente...")
wait(0.3)

-- ============================================
-- CONFIGURAÇÕES PRINCIPAIS
-- ============================================
UpdateProgress(10, "Configurando sistema...")

local Cosmic = {
    -- Configurações principais
    Version = "5.0",
    ThemeColor = Color3.fromRGB(157, 78, 221),
    AccentColor = Color3.fromRGB(180, 100, 255),
    
    -- Auto Farm
    AutoFarm = false,
    CollectMoney = true,
    CollectCrates = true,
    CollectGifts = true,
    
    -- Player
    WalkSpeed = 20,
    JumpPower = 50,
    Noclip = false,
    Fly = false,
    
    -- Misc
    AntiAFK = true,
    AutoJob = false,
    JobType = "Delivery",
    RainbowMode = false,
    Notifications = true
}

-- Serviços
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local HumanoidRootPart = Character:WaitForChild("HumanoidRootPart")
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")

UpdateProgress(20, "Detectando dispositivo...")

-- Detecção de plataforma
local IS_MOBILE = game:GetService("UserInputService").TouchEnabled
local IS_TABLET = not game:GetService("UserInputService").KeyboardEnabled
local PLATFORM = IS_MOBILE and "Mobile" or (IS_TABLET and "Tablet" or "Desktop")

-- ============================================
-- SISTEMA DE NOTIFICAÇÕES
-- ============================================
UpdateProgress(30, "Criando notificações...")

function CosmicNotify(Title, Message, Duration)
    if Cosmic.Notifications then
        game.StarterGui:SetCore("SendNotification", {
            Title = "💜 " .. Title,
            Text = Message,
            Duration = Duration or 3,
            Icon = "rbxassetid://4483345998"
        })
    end
    print("💜 COSMIC HUB: " .. Title .. " - " .. Message)
end

-- ============================================
-- INTERFACE PRINCIPAL
-- ============================================
UpdateProgress(40, "Criando interface...")

-- GUI Principal
local CosmicGUI = Instance.new("ScreenGui")
CosmicGUI.Name = "CosmicHubV5"
CosmicGUI.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
CosmicGUI.Parent = game.CoreGui

-- Botão flutuante principal
local MainButton = Instance.new("TextButton")
MainButton.Name = "CosmicMainButton"
MainButton.Size = UDim2.new(0, 70, 0, 70)
MainButton.Position = UDim2.new(1, -80, 1, -80)
MainButton.BackgroundColor3 = Cosmic.ThemeColor
MainButton.Text = "🌌"
MainButton.TextSize = 32
MainButton.Font = Enum.Font.GothamBlack
MainButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MainButton.BorderSizePixel = 0
MainButton.AutoButtonColor = false
MainButton.Parent = CosmicGUI

-- Efeitos do botão
local ButtonCorner = Instance.new("UICorner")
ButtonCorner.CornerRadius = UDim.new(1, 0)
ButtonCorner.Parent = MainButton

local ButtonStroke = Instance.new("UIStroke")
ButtonStroke.Color = Color3.fromRGB(255, 255, 255)
ButtonStroke.Thickness = 3
ButtonStroke.Parent = MainButton

-- Menu principal
local MainMenu = Instance.new("Frame")
MainMenu.Name = "MainMenu"
MainMenu.Size = UDim2.new(0, 350, 0, 500)
MainMenu.Position = UDim2.new(0.5, -175, 0.5, -250)
MainMenu.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
MainMenu.Visible = false
MainMenu.Parent = CosmicGUI

local MenuCorner = Instance.new("UICorner")
MenuCorner.CornerRadius = UDim.new(0, 12)
MenuCorner.Parent = MainMenu

-- Header do menu
local MenuHeader = Instance.new("Frame")
MenuHeader.Size = UDim2.new(1, 0, 0, 70)
MenuHeader.BackgroundColor3 = Cosmic.ThemeColor
MenuHeader.Parent = MainMenu

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 12)
HeaderCorner.Parent = MenuHeader

local MenuTitle = Instance.new("TextLabel")
MenuTitle.Size = UDim2.new(1, 0, 0, 40)
MenuTitle.Position = UDim2.new(0, 0, 0, 10)
MenuTitle.Text = "🌌 COSMIC HUB V5.0"
MenuTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
MenuTitle.Font = Enum.Font.GothamBlack
MenuTitle.TextSize = 22
MenuTitle.BackgroundTransparency = 1
MenuTitle.Parent = MenuHeader

local MenuSubtitle = Instance.new("TextLabel")
MenuSubtitle.Size = UDim2.new(1, 0, 0, 20)
MenuSubtitle.Position = UDim2.new(0, 0, 0, 40)
MenuSubtitle.Text = "Brookhaven Mobile | " .. PLATFORM
MenuSubtitle.TextColor3 = Color3.fromRGB(200, 200, 255)
MenuSubtitle.Font = Enum.Font.Gotham
MenuSubtitle.TextSize = 14
MenuSubtitle.BackgroundTransparency = 1
MenuSubtitle.Parent = MenuHeader

-- Botão fechar
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 40, 0, 40)
CloseButton.Position = UDim2.new(1, -50, 0, 15)
CloseButton.Text = "✕"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.GothamBold
CloseButton.TextSize = 20
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 60, 60)
CloseButton.Parent = MenuHeader

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(1, 0)
CloseCorner.Parent = CloseButton

-- Tabs
UpdateProgress(50, "Criando abas...")

local TabsContainer = Instance.new("Frame")
TabsContainer.Size = UDim2.new(1, 0, 0, 40)
TabsContainer.Position = UDim2.new(0, 0, 0, 70)
TabsContainer.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
TabsContainer.BorderSizePixel = 0
TabsContainer.Parent = MainMenu

local Tabs = {"Início", "Auto Farm", "Jogador", "Teleportes", "Misc", "Créditos"}
local TabButtons = {}

for i, tabName in ipairs(Tabs) do
    local TabButton = Instance.new("TextButton")
    TabButton.Size = UDim2.new(1/#Tabs, 0, 1, 0)
    TabButton.Position = UDim2.new((i-1)/#Tabs, 0, 0, 0)
    TabButton.Text = tabName
    TabButton.TextColor3 = Color3.fromRGB(200, 200, 200)
    TabButton.Font = Enum.Font.Gotham
    TabButton.TextSize = 14
    TabButton.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
    TabButton.BorderSizePixel = 0
    TabButton.Parent = TabsContainer
    
    TabButtons[tabName] = TabButton
end

-- Conteúdo das tabs
local ContentFrame = Instance.new("ScrollingFrame")
ContentFrame.Size = UDim2.new(1, -20, 1, -130)
ContentFrame.Position = UDim2.new(0, 10, 0, 120)
ContentFrame.BackgroundTransparency = 1
ContentFrame.BorderSizePixel = 0
ContentFrame.ScrollBarThickness = 4
ContentFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
ContentFrame.Parent = MainMenu

UpdateProgress(60, "Configurando funções...")

-- ============================================
-- FUNÇÕES PRINCIPAIS
-- ============================================

-- Função para criar seções
function CreateSection(Title)
    local Section = Instance.new("Frame")
    Section.Size = UDim2.new(1, 0, 0, 40)
    Section.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
    Section.LayoutOrder = #ContentFrame:GetChildren()
    
    local SectionCorner = Instance.new("UICorner")
    SectionCorner.CornerRadius = UDim.new(0, 8)
    SectionCorner.Parent = Section
    
    local TitleLabel = Instance.new("TextLabel")
    TitleLabel.Size = UDim2.new(1, -20, 1, 0)
    TitleLabel.Position = UDim2.new(0, 10, 0, 0)
    TitleLabel.Text = "   " .. Title
    TitleLabel.TextColor3 = Cosmic.AccentColor
    TitleLabel.Font = Enum.Font.GothamBold
    TitleLabel.TextSize = 16
    TitleLabel.TextXAlignment = Enum.TextXAlignment.Left
    TitleLabel.BackgroundTransparency = 1
    TitleLabel.Parent = Section
    
    return Section
end

-- Função para criar botões
function CreateButton(Text, Callback)
    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(1, 0, 0, 45)
    Button.Text = Text
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.Font = Enum.Font.Gotham
    Button.TextSize = 15
    Button.BackgroundColor3 = Cosmic.ThemeColor
    Button.AutoButtonColor = true
    
    local ButtonCorner = Instance.new("UICorner")
    ButtonCorner.CornerRadius = UDim.new(0, 8)
    ButtonCorner.Parent = Button
    
    Button.MouseButton1Click:Connect(Callback)
    
    return Button
end

-- Função para criar toggle
function CreateToggle(Text, Default, Callback)
    local ToggleFrame = Instance.new("Frame")
    ToggleFrame.Size = UDim2.new(1, 0, 0, 40)
    ToggleFrame.BackgroundTransparency = 1
    
    local ToggleText = Instance.new("TextLabel")
    ToggleText.Size = UDim2.new(0.7, 0, 1, 0)
    ToggleText.Text = Text
    ToggleText.TextColor3 = Color3.fromRGB(220, 220, 220)
    ToggleText.Font = Enum.Font.Gotham
    ToggleText.TextSize = 14
    ToggleText.TextXAlignment = Enum.TextXAlignment.Left
    ToggleText.BackgroundTransparency = 1
    ToggleText.Parent = ToggleFrame
    
    local ToggleButton = Instance.new("TextButton")
    ToggleButton.Size = UDim2.new(0, 50, 0, 25)
    ToggleButton.Position = UDim2.new(1, -55, 0.5, -12.5)
    ToggleButton.Text = ""
    ToggleButton.BackgroundColor3 = Default and Cosmic.ThemeColor or Color3.fromRGB(80, 80, 100)
    
    local ToggleCorner = Instance.new("UICorner")
    ToggleCorner.CornerRadius = UDim.new(1, 0)
    ToggleCorner.Parent = ToggleButton
    
    local ToggleCircle = Instance.new("Frame")
    ToggleCircle.Size = UDim2.new(0, 21, 0, 21)
    ToggleCircle.Position = UDim2.new(Default and 1 or 0, -23, 0.5, -10.5)
    ToggleCircle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ToggleCircle.Parent = ToggleButton
    
    local CircleCorner = Instance.new("UICorner")
    CircleCorner.CornerRadius = UDim.new(1, 0)
    CircleCorner.Parent = ToggleCircle
    
    ToggleButton.MouseButton1Click:Connect(function()
        local newState = not (ToggleCircle.Position.X.Scale == 1)
        TweenService:Create(ToggleCircle, TweenInfo.new(0.2), {
            Position = UDim2.new(newState and 1 or 0, -23, 0.5, -10.5)
        }):Play()
        
        TweenService:Create(ToggleButton, TweenInfo.new(0.2), {
            BackgroundColor3 = newState and Cosmic.ThemeColor or Color3.fromRGB(80, 80, 100)
        }):Play()
        
        Callback(newState)
    end)
    
    ToggleButton.Parent = ToggleFrame
    
    return ToggleFrame
end

-- ============================================
-- TAB: INÍCIO
-- ============================================
UpdateProgress(65, "Configurando aba Início...")

local HomeContent = Instance.new("Frame")
HomeContent.Size = UDim2.new(1, 0, 0, 400)
HomeContent.BackgroundTransparency = 1
HomeContent.Visible = true
HomeContent.Name = "HomeContent"
HomeContent.Parent = ContentFrame

-- Status
local StatusSection = CreateSection("📊 STATUS DO SISTEMA")
StatusSection.Parent = HomeContent

local StatusInfo = Instance.new("TextLabel")
StatusInfo.Size = UDim2.new(1, -20, 0, 100)
StatusInfo.Position = UDim2.new(0, 10, 0, 50)
StatusInfo.Text = "Plataforma: " .. PLATFORM .. "\n\n" ..
                   "💜 Cosmic Hub V5.0\n" ..
                   "🎮 Brookhaven Mobile\n" ..
                   "🚀 Pronto para uso!"
StatusInfo.TextColor3 = Color3.fromRGB(200, 200, 220)
StatusInfo.Font = Enum.Font.Gotham
StatusInfo.TextSize = 14
StatusInfo.TextXAlignment = Enum.TextXAlignment.Left
StatusInfo.TextYAlignment = Enum.TextYAlignment.Top
StatusInfo.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
StatusInfo.BackgroundTransparency = 0.5
StatusInfo.Parent = HomeContent

local StatusCorner = Instance.new("UICorner")
StatusCorner.CornerRadius = UDim.new(0, 8)
StatusCorner.Parent = StatusInfo

-- Início Rápido
local QuickSection = CreateSection("⚡ INÍCIO RÁPIDO")
QuickSection.Position = UDim2.new(0, 0, 0, 160)
QuickSection.Parent = HomeContent

local StartFarmBtn = CreateButton("🚀 INICIAR AUTO FARM", function()
    Cosmic.AutoFarm = not Cosmic.AutoFarm
    if Cosmic.AutoFarm then
        CosmicNotify("AUTO FARM", "Sistema ativado!", 3)
        StartCosmicFarm()
    else
        CosmicNotify("AUTO FARM", "Sistema desativado!", 3)
    end
end)
StartFarmBtn.Position = UDim2.new(0, 0, 0, 210)
StartFarmBtn.Parent = HomeContent

local CollectAllBtn = CreateButton("🎁 COLETAR TUDO AGORA", function()
    CosmicCollectAll()
end)
CollectAllBtn.Position = UDim2.new(0, 0, 0, 265)
CollectAllBtn.Parent = HomeContent

-- ============================================
-- TAB: AUTO FARM
-- ============================================
UpdateProgress(70, "Configurando aba Auto Farm...")

local FarmContent = Instance.new("Frame")
FarmContent.Size = UDim2.new(1, 0, 0, 600)
FarmContent.BackgroundTransparency = 1
FarmContent.Visible = false
FarmContent.Name = "FarmContent"
FarmContent.Parent = ContentFrame

local FarmSection = CreateSection("⚙️ CONFIGURAÇÕES AUTO FARM")
FarmSection.Parent = FarmContent

local MoneyToggle = CreateToggle("💰 Coletar Dinheiro", true, function(state)
    Cosmic.CollectMoney = state
end)
MoneyToggle.Position = UDim2.new(0, 0, 0, 50)
MoneyToggle.Parent = FarmContent

local CratesToggle = CreateToggle("📦 Coletar Caixas", true, function(state)
    Cosmic.CollectCrates = state
end)
CratesToggle.Position = UDim2.new(0, 0, 0, 100)
CratesToggle.Parent = FarmContent

local GiftsToggle = CreateToggle("🎁 Coletar Presentes", true, function(state)
    Cosmic.CollectGifts = state
end)
GiftsToggle.Position = UDim2.new(0, 0, 0, 150)
GiftsToggle.Parent = FarmContent

-- Ações rápidas
local ActionsSection = CreateSection("🎯 AÇÕES RÁPIDAS")
ActionsSection.Position = UDim2.new(0, 0, 0, 200)
ActionsSection.Parent = FarmContent

local FindMoneyBtn = CreateButton("🔍 ENCONTRAR DINHEIRO", function()
    CosmicCollectMoney()
end)
FindMoneyBtn.Position = UDim2.new(0, 0, 0, 250)
FindMoneyBtn.Parent = FarmContent

local FindCratesBtn = CreateButton("🔍 ENCONTRAR CAIXAS", function()
    CosmicCollectCrates()
end)
FindCratesBtn.Position = UDim2.new(0, 0, 0, 305)
FindCratesBtn.Parent = FarmContent

-- ============================================
-- TAB: JOGADOR
-- ============================================
UpdateProgress(75, "Configurando aba Jogador...")

local PlayerContent = Instance.new("Frame")
PlayerContent.Size = UDim2.new(1, 0, 0, 500)
PlayerContent.BackgroundTransparency = 1
PlayerContent.Visible = false
PlayerContent.Name = "PlayerContent"
PlayerContent.Parent = ContentFrame

local PlayerSection = CreateSection("👤 CONFIGURAÇÕES DO JOGADOR")
PlayerSection.Parent = PlayerContent

-- Velocidade
local SpeedFrame = Instance.new("Frame")
SpeedFrame.Size = UDim2.new(1, 0, 0, 60)
SpeedFrame.Position = UDim2.new(0, 0, 0, 50)
SpeedFrame.BackgroundTransparency = 1
SpeedFrame.Parent = PlayerContent

local SpeedText = Instance.new("TextLabel")
SpeedText.Size = UDim2.new(0.7, 0, 1, 0)
SpeedText.Text = "⚡ Velocidade: 20"
SpeedText.TextColor3 = Color3.fromRGB(220, 220, 220)
SpeedText.Font = Enum.Font.Gotham
SpeedText.TextSize = 14
SpeedText.TextXAlignment = Enum.TextXAlignment.Left
SpeedText.BackgroundTransparency = 1
SpeedText.Parent = SpeedFrame

local SpeedSlider = Instance.new("TextButton")
SpeedSlider.Size = UDim2.new(0, 150, 0, 20)
SpeedSlider.Position = UDim2.new(1, -155, 0.5, -10)
SpeedSlider.Text = ""
SpeedSlider.BackgroundColor3 = Color3.fromRGB(80, 80, 100)
SpeedSlider.Parent = SpeedFrame

local SpeedSliderCorner = Instance.new("UICorner")
SpeedSliderCorner.CornerRadius = UDim.new(1, 0)
SpeedSliderCorner.Parent = SpeedSlider

local SpeedFill = Instance.new("Frame")
SpeedFill.Size = UDim2.new(0.4, 0, 1, 0)
SpeedFill.BackgroundColor3 = Cosmic.ThemeColor
SpeedFill.Parent = SpeedSlider

local SpeedFillCorner = Instance.new("UICorner")
SpeedFillCorner.CornerRadius = UDim.new(1, 0)
SpeedFillCorner.Parent = SpeedFill

-- Pulo
local JumpFrame = Instance.new("Frame")
JumpFrame.Size = UDim2.new(1, 0, 0, 60)
JumpFrame.Position = UDim2.new(0, 0, 0, 120)
JumpFrame.BackgroundTransparency = 1
JumpFrame.Parent = PlayerContent

local JumpText = Instance.new("TextLabel")
JumpText.Size = UDim2.new(0.7, 0, 1, 0)
JumpText.Text = "🦘 Pulo: 50"
JumpText.TextColor3 = Color3.fromRGB(220, 220, 220)
JumpText.Font = Enum.Font.Gotham
JumpText.TextSize = 14
JumpText.TextXAlignment = Enum.TextXAlignment.Left
JumpText.BackgroundTransparency = 1
JumpText.Parent = JumpFrame

-- Botões de jogador
local ResetBtn = CreateButton("🔄 RESETAR PERSONAGEM", function()
    Character:BreakJoints()
    CosmicNotify("JOGADOR", "Personagem resetado!", 2)
end)
ResetBtn.Position = UDim2.new(0, 0, 0, 200)
ResetBtn.Parent = PlayerContent

local AntiAFKBtn = CreateButton("🔄 ANTI-AFK ON/OFF", function()
    Cosmic.AntiAFK = not Cosmic.AntiAFK
    if Cosmic.AntiAFK then
        ActivateCosmicAntiAFK()
        CosmicNotify("ANTI-AFK", "Ativado!", 2)
    else
        CosmicNotify("ANTI-AFK", "Desativado!", 2)
    end
end)
AntiAFKBtn.Position = UDim2.new(0, 0, 0, 255)
AntiAFKBtn.Parent = PlayerContent

-- ============================================
-- TAB: TELEPORTES
-- ============================================
UpdateProgress(80, "Configurando aba Teleportes...")

local TeleportContent = Instance.new("Frame")
TeleportContent.Size = UDim2.new(1, 0, 0, 400)
TeleportContent.BackgroundTransparency = 1
TeleportContent.Visible = false
TeleportContent.Name = "TeleportContent"
TeleportContent.Parent = ContentFrame

local TeleportSection = CreateSection("📍 TELEPORTES RÁPIDOS")
TeleportSection.Parent = TeleportContent

local HouseTPBtn = CreateButton("🏠 TELEPORTAR PARA CASA", function()
    CosmicTPHouse()
end)
HouseTPBtn.Position = UDim2.new(0, 0, 0, 50)
HouseTPBtn.Parent = TeleportContent

local ShopTPBtn = CreateButton("🛒 TELEPORTAR PARA LOJA", function()
    CosmicTPShop()
end)
ShopTPBtn.Position = UDim2.new(0, 0, 0, 105)
ShopTPBtn.Parent = TeleportContent

local BankTPBtn = CreateButton("🏦 TELEPORTAR PARA BANCO", function()
    HumanoidRootPart.CFrame = CFrame.new(200, 5, 200)
    CosmicNotify("TELEPORT", "Área do banco", 3)
end)
BankTPBtn.Position = UDim2.new(0, 0, 0, 160)
BankTPBtn.Parent = TeleportContent

local HospitalTPBtn = CreateButton("🏥 TELEPORTAR PARA HOSPITAL", function()
    HumanoidRootPart.CFrame = CFrame.new(-200, 5, 200)
    CosmicNotify("TELEPORT", "Área do hospital", 3)
end)
HospitalTPBtn.Position = UDim2.new(0, 0, 0, 215)
HospitalTPBtn.Parent = TeleportContent

-- ============================================
-- TAB: MISC
-- ============================================
UpdateProgress(85, "Configurando aba Misc...")

local MiscContent = Instance.new("Frame")
MiscContent.Size = UDim2.new(1, 0, 0, 300)
MiscContent.BackgroundTransparency = 1
MiscContent.Visible = false
MiscContent.Name = "MiscContent"
MiscContent.Parent = ContentFrame

local MiscSection = CreateSection("🔧 FERRAMENTAS EXTRAS")
MiscSection.Parent = MiscContent

local RainbowToggle = CreateToggle("🌈 MODO RAINBOW", false, function(state)
    Cosmic.RainbowMode = state
    if state then
        ActivateRainbowMode()
    end
end)
RainbowToggle.Position = UDim2.new(0, 0, 0, 50)
RainbowToggle.Parent = MiscContent

local NotificationsToggle = CreateToggle("🔔 NOTIFICAÇÕES", true, function(state)
    Cosmic.Notifications = state
end)
NotificationsToggle.Position = UDim2.new(0, 0, 0, 100)
NotificationsToggle.Parent = MiscContent

local RejoinBtn = CreateButton("🔄 REJOIN SERVER", function()
    game:GetService("TeleportService"):Teleport(game.PlaceId)
end)
RejoinBtn.Position = UDim2.new(0, 0, 0, 170)
RejoinBtn.Parent = MiscContent

-- ============================================
-- TAB: CRÉDITOS
-- ============================================
UpdateProgress(90, "Configurando aba Créditos...")

local CreditsContent = Instance.new("Frame")
CreditsContent.Size = UDim2.new(1, 0, 0, 400)
CreditsContent.BackgroundTransparency = 1
CreditsContent.Visible = false
CreditsContent.Name = "CreditsContent"
CreditsContent.Parent = ContentFrame

local CreditsSection = CreateSection("🌟 CRÉDITOS & INFORMAÇÕES")
CreditsSection.Parent = CreditsContent

local CreditsInfo = Instance.new("TextLabel")
CreditsInfo.Size = UDim2.new(1, -20, 0, 300)
CreditsInfo.Position = UDim2.new(0, 10, 0, 50)
CreditsInfo.Text = [[💜 COSMIC HUB V5.0

🌟 CRÉDITOS:
Desenvolvedor: Cosmic Team
Design: Cosmic Studio
Testers: Comunidade Cosmic

🎮 FUNÇÕES:
• Auto Farm Completo
• Teleportes Rápidos
• Modificações de Jogador
• Sistema Anti-AFK
• Interface Mobile Otimizada

🌐 LINKS:
Discord: discord.gg/cosmichub
Suporte: @cosmichub

🚀 VERSÃO 5.0
Brookhaven Mobile Edition
Totalmente otimizado para touch!

💜 Obrigado por usar Cosmic Hub!]]
CreditsInfo.TextColor3 = Color3.fromRGB(200, 200, 220)
CreditsInfo.Font = Enum.Font.Gotham
CreditsInfo.TextSize = 14
CreditsInfo.TextXAlignment = Enum.TextXAlignment.Left
CreditsInfo.TextYAlignment = Enum.TextYAlignment.Top
CreditsInfo.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
CreditsInfo.BackgroundTransparency = 0.5
CreditsInfo.Parent = CreditsContent

local CreditsCorner = Instance.new("UICorner")
CreditsCorner.CornerRadius = UDim.new(0, 8)
CreditsCorner.Parent = CreditsInfo

-- ============================================
-- FUNÇÕES DO SISTEMA
-- ============================================
UpdateProgress(95, "Inicializando funções...")

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
            wait(2)
        end
    end)
end

function CosmicCollectMoney()
    local collected = 0
    for _, obj in pairs(Workspace:GetChildren()) do
        if not Cosmic.AutoFarm then break end
        
        if obj.Name:lower():find("money") or obj.Name:lower():find("cash") then
            if obj:IsA("BasePart") then
                local distance = (HumanoidRootPart.Position - obj.Position).Magnitude
                if distance < 150 then
                    TweenService:Create(HumanoidRootPart, TweenInfo.new(0.5), {
                        CFrame = CFrame.new(obj.Position + Vector3.new(0, 3, 0))
                    }):Play()
                    wait(0.6)
                    
                    firetouchinterest(HumanoidRootPart, obj, 0)
                    firetouchinterest(HumanoidRootPart, obj, 1)
                    
                    collected = collected + 1
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
        if not Cosmic.AutoFarm then break end
        
        if obj.Name:lower():find("crate") or obj.Name:lower():find("box") then
            if obj:IsA("BasePart") then
                local distance = (HumanoidRootPart.Position - obj.Position).Magnitude
                if distance < 150 then
                    HumanoidRootPart.CFrame = CFrame.new(obj.Position + Vector3.new(0, 3, 0))
                    wait(0.5)
                    firetouchinterest(HumanoidRootPart, obj, 0)
                    firetouchinterest(HumanoidRootPart, obj, 1)
                end
            end
        end
    end
end

function CosmicCollectGifts()
    for _, obj in pairs(Workspace:GetChildren()) do
        if not Cosmic.AutoFarm then break end
        
        if obj.Name:lower():find("gift") or obj.Name:lower():find("present") then
            if obj:IsA("BasePart") then
                local distance = (HumanoidRootPart.Position - obj.Position).Magnitude
                if distance < 150 then
                    HumanoidRootPart.CFrame = CFrame.new(obj.Position + Vector3.new(0, 3, 0))
                    wait(0.5)
                    firetouchinterest(HumanoidRootPart, obj, 0)
                    firetouchinterest(HumanoidRootPart, obj, 1)
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
    for _, obj in pairs(Workspace:GetChildren()) do
        if obj.Name:find(LocalPlayer.Name) and obj.Name:find("House") then
            HumanoidRootPart.CFrame = CFrame.new(obj.Position + Vector3.new(0, 5, 0))
            CosmicNotify("TELEPORT", "Casa encontrada!", 3)
            return
        end
    end
    HumanoidRootPart.CFrame = CFrame.new(500, 10, 500)
    CosmicNotify("TELEPORT", "Área residencial", 3)
end

function CosmicTPShop()
    HumanoidRootPart.CFrame = CFrame.new(-50, 5, -100)
    CosmicNotify("TELEPORT", "Área comercial", 3)
end

function ActivateCosmicAntiAFK()
    spawn(function()
        while Cosmic.AntiAFK do
            wait(30)
            if Character and Character:FindFirstChild("Humanoid") then
                Character.Humanoid:Move(Vector3.new(1, 0, 0))
                wait(0.1)
                Character.Humanoid:Move(Vector3.new(-1, 0, 0))
            end
        end
    end)
end

function ActivateRainbowMode()
    spawn(function()
        while Cosmic.RainbowMode do
            local hue = tick() % 5 / 5
            Cosmic.ThemeColor = Color3.fromHSV(hue, 0.8, 0.9)
            
            MainButton.BackgroundColor3 = Cosmic.ThemeColor
            MenuHeader.BackgroundColor3 = Cosmic.ThemeColor
            
            for _, btn in pairs(ContentFrame:GetDescendants()) do
                if btn:IsA("TextButton") and btn.BackgroundColor3 == Color3.fromRGB(157, 78, 221) then
                    btn.BackgroundColor3 = Cosmic.ThemeColor
                end
            end
            
            wait(0.1)
        end
    end)
end

-- ============================================
-- INTERAÇÕES DA INTERFACE
-- ============================================
UpdateProgress(98, "Configurando interações...")

-- Sistema de tabs
local CurrentTab = "Início"
local TabContents = {
    ["Início"] = HomeContent,
    ["Auto Farm"] = FarmContent,
    ["Jogador"] = PlayerContent,
    ["Teleportes"] = TeleportContent,
    ["Misc"] = MiscContent,
    ["Créditos"] = CreditsContent
}

for tabName, tabButton in pairs(TabButtons) do
    tabButton.MouseButton1Click:Connect(function()
        CurrentTab = tabName
        
        -- Esconder todas as tabs
        for name, content in pairs(TabContents) do
            content.Visible = false
        end
        
        -- Mostrar tab atual
        TabContents[tabName].Visible = true
        
        -- Atualizar cor dos botões
        for name, button in pairs(TabButtons) do
            button.BackgroundColor3 = name == tabName and Cosmic.ThemeColor or Color3.fromRGB(30, 30, 40)
            button.TextColor3 = name == tabName and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(200, 200, 200)
        end
    end)
end

-- Botão principal
MainButton.MouseButton1Click:Connect(function()
    MainMenu.Visible = not MainMenu.Visible
    if MainMenu.Visible then
        MainButton.BackgroundColor3 = Cosmic.AccentColor
    else
        MainButton.BackgroundColor3 = Cosmic.ThemeColor
    end
end)

-- Botão fechar
CloseButton.MouseButton1Click:Connect(function()
    MainMenu.Visible = false
    MainButton.BackgroundColor3 = Cosmic.ThemeColor
end)

-- Sistema de gestos mobile
if IS_MOBILE then
    local tapCount = 0
    local lastTap = 0
    
    game:GetService("UserInputService").TouchTap:Connect(function()
        local now = tick()
        if now - lastTap < 0.5 then
            tapCount = tapCount + 1
            if tapCount == 3 then
                MainMenu.Visible = not MainMenu.Visible
                tapCount = 0
            end
        else
            tapCount = 1
        end
        lastTap = now
    end)
end

-- ============================================
-- FINALIZAÇÃO
-- ============================================
UpdateProgress(100, "Pronto! Inicializando...")

-- Fechar tela de loading
wait(1)
local fadeTween = TweenService:Create(LoadingBackground, TweenInfo.new(0.8), {
    BackgroundTransparency = 1
})
fadeTween:Play()

for _, child in pairs(LoadingBackground:GetChildren()) do
    if child:IsA("GuiObject") then
        local childTween = TweenService:Create(child, TweenInfo.new(0.8), {
            BackgroundTransparency = 1,
            TextTransparency = 1
        })
        childTween:Play()
    end
end

wait(1)
LoadingScreen:Destroy()

-- Animação de entrada
MainButton.Position = UDim2.new(1, -80, 1, 80)
local slideTween = TweenService:Create(MainButton, TweenInfo.new(0.6, Enum.EasingStyle.Back), {
    Position = UDim2.new(1, -80, 1, -80)
})
slideTween:Play()

-- Notificação inicial
CosmicNotify("COSMIC HUB V5.0", 
    "🌌 Brookhaven Mobile Edition carregado!\n" ..
    "💜 Tema Roxo Cosmic ativado!\n" ..
    "📱 " .. PLATFORM .. " detectado!", 5)

-- Log no console
print([[
    
   _____                      _       _   _     
  / ____|                    | |     | | | |    
 | |     ___  _ __ ___   __ _| |_ ___| |_| |__  
 | |    / _ \| '_ ` _ \ / _` | __/ __| __| '_ \ 
 | |___| (_) | | | | | | (_| | || (__| |_| | | |
  \_____\___/|_| |_| |_|\__,_|\__\___|\__|_| |_|
                                                
💜 COSMIC HUB V5.0 - Brookhaven Mobile
📱 Plataforma: ]] .. PLATFORM .. [[
🚀 Auto Farm: Pronto
📍 Teleportes: Configurados
🎮 Controles: ]] .. (IS_MOBILE and "Touch" or "Teclado") .. [[

]])

-- Sistema de atualização
spawn(function()
    while wait(10) do
        if Cosmic.AutoFarm then
            MainButton.Text = "🚀"
        else
            MainButton.Text = "🌌"
        end
    end
end)

-- Reconexão de personagem
LocalPlayer.CharacterAdded:Connect(function(char)
    Character = char
    HumanoidRootPart = char:WaitForChild("HumanoidRootPart")
    CosmicNotify("SISTEMA", "Personagem reconectado!", 2)
end)

-- Mensagem final
print("💜 Cosmic Hub V5.0 inicializado com sucesso!")
print("🎮 Pressione o botão roxo para abrir o menu!")
print("🌐 Discord: discord.gg/cosmichub")
