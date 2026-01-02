--[[ 
    CLUR HUB v10 - ASSIS ELITE EDITION
    SENHA: Clurscript3 | CONFIG: DvloperAssis
]]

local SENHA_PRINCIPAL = "Clurscript3"
local SENHA_CONFIG = "DvloperAssis"
local DISCORD_LINK = "https://discord.gg/zraSa5W2Qg"

local Player = game.Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

-- Limpeza de UI
if PlayerGui:FindFirstChild("ClurHubAssis") then PlayerGui.ClurHubAssis:Destroy() end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ClurHubAssis"
screenGui.Parent = PlayerGui
screenGui.ResetOnSpawn = false

-- FUNÇÃO: CRIAR BORDAS NEON NOS BOTÕES E CAMPOS
local function applyModernStroke(parent, color)
    local stroke = Instance.new("UIStroke")
    stroke.Thickness = 2
    stroke.Color = color or Color3.fromRGB(80, 80, 80)
    stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    stroke.Parent = parent
    return stroke
end

-- SISTEMA 1: BOLINHAS CAINDO (NEVE NO HUD)
local function createFallingParticles(frame)
    local container = Instance.new("Frame")
    container.Size = UDim2.new(1, 0, 1, 0)
    container.BackgroundTransparency = 1
    container.ClipsDescendants = true
    container.ZIndex = 0
    container.Parent = frame

    for i = 1, 20 do
        local p = Instance.new("Frame")
        p.Size = UDim2.new(0, 3, 0, 3)
        p.BackgroundColor3 = (i % 2 == 0) and Color3.new(1, 1, 1) or Color3.fromRGB(180, 180, 180)
        p.BackgroundTransparency = 0.4
        p.Parent = container
        Instance.new("UICorner", p).CornerRadius = UDim.new(1, 0)

        task.spawn(function()
            local speed = math.random(10, 30) / 100
            p.Position = UDim2.new(math.random(), 0, -0.1, 0)
            while frame and frame.Parent do
                local newY = p.Position.Y.Scale + (speed * 0.01)
                if newY > 1.1 then newY = -0.1 p.Position = UDim2.new(math.random(), 0, -0.1, 0) end
                p.Position = UDim2.new(p.Position.X.Scale, 0, newY, 0)
                RunService.RenderStepped:Wait()
            end
        end)
    end
end

-- SISTEMA 2: BOLINHAS DANDO VOLTA NAS LINHAS (ÓRBITA)
local function createOrbitParticles(frame, stroke)
    for i = 1, 4 do
        local dot = Instance.new("Frame")
        dot.Size = UDim2.new(0, 4, 0, 4)
        dot.BackgroundColor3 = Color3.new(1, 1, 1)
        dot.ZIndex = 10
        dot.Parent = frame
        Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)

        task.spawn(function()
            local t = i * (math.pi/2)
            while frame and frame.Parent do
                t = t + 0.02
                -- Lógica para seguir a borda retangular
                local x = math.clamp(math.cos(t) * 1.5, -0.5, 0.5) + 0.5
                local y = math.clamp(math.sin(t) * 1.5, -0.5, 0.5) + 0.5
                dot.Position = UDim2.new(x, -2, y, -2)
                RunService.RenderStepped:Wait()
            end
        end)
    end
end

-- TELA DE LOGIN
local loginFrame = Instance.new("Frame")
loginFrame.Size = UDim2.new(0, 420, 0, 320)
loginFrame.Position = UDim2.new(0.5, -210, 0.5, -160)
loginFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 14)
loginFrame.Active = true
loginFrame.Draggable = true
loginFrame.Parent = screenGui
Instance.new("UICorner", loginFrame)

local loginStroke = applyModernStroke(loginFrame, Color3.fromRGB(88, 101, 242))
createFallingParticles(loginFrame)
createOrbitParticles(loginFrame, loginStroke)

local passBox = Instance.new("TextBox")
passBox.Size = UDim2.new(0.7, 0, 0, 45)
passBox.Position = UDim2.new(0.15, 0, 0.35, 0)
passBox.Text = ""
passBox.PlaceholderText = "SENHA"
passBox.BackgroundColor3 = Color3.fromRGB(20, 20, 22)
passBox.TextColor3 = Color3.new(1,1,1)
passBox.Parent = loginFrame
Instance.new("UICorner", passBox)
applyModernStroke(passBox)

local loginBtn = Instance.new("TextButton")
loginBtn.Size = UDim2.new(0.7, 0, 0, 50)
loginBtn.Position = UDim2.new(0.15, 0, 0.55, 0)
loginBtn.Text = "DESBLOQUEAR"
loginBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
loginBtn.TextColor3 = Color3.new(1,1,1)
loginBtn.Font = Enum.Font.GothamBold
loginBtn.Parent = loginFrame
Instance.new("UICorner", loginBtn)
applyModernStroke(loginBtn, Color3.new(1,1,1))

-- BOTÃO DISCORD (IMAGEM REAL + NOME AO PASSAR)
local discordBtn = Instance.new("ImageButton")
discordBtn.Size = UDim2.new(0, 50, 0, 50)
discordBtn.Position = UDim2.new(0.5, -25, 0.8, 0)
discordBtn.Image = "rbxassetid://15623048952" -- Logo Clyde Oficial
discordBtn.BackgroundColor3 = Color3.fromRGB(88, 101, 242)
discordBtn.Parent = loginFrame
Instance.new("UICorner", discordBtn, UDim.new(1,0))
applyModernStroke(discordBtn, Color3.new(1,1,1))

local dcLabel = Instance.new("TextLabel")
dcLabel.Size = UDim2.new(0, 100, 0, 25)
dcLabel.Position = UDim2.new(0.5, -50, -0.6, 0)
dcLabel.Text = "DISCORD"
dcLabel.Visible = false
dcLabel.BackgroundColor3 = Color3.new(0,0,0)
dcLabel.TextColor3 = Color3.new(1,1,1)
dcLabel.Font = Enum.Font.GothamBold
dcLabel.Parent = discordBtn
Instance.new("UICorner", dcLabel)

discordBtn.MouseEnter:Connect(function() dcLabel.Visible = true end)
discordBtn.MouseLeave:Connect(function() dcLabel.Visible = false end)
discordBtn.MouseButton1Click:Connect(function()
    local req = (syn and syn.request) or (http and http.request) or request
    if req then req({Url = DISCORD_LINK, Method = "GET"}) else setclipboard(DISCORD_LINK) end
end)

-- HUB PRINCIPAL
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 550, 0, 400)
mainFrame.Position = UDim2.new(0.5, -275, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 12)
mainFrame.Visible = false
mainFrame.Parent = screenGui
Instance.new("UICorner", mainFrame)
local mainStroke = applyModernStroke(mainFrame, Color3.fromRGB(60, 60, 60))
createFallingParticles(mainFrame)
createOrbitParticles(mainFrame, mainStroke)

-- Layout lateral (Sidebar)
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 150, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(18, 18, 20)
sidebar.Parent = mainFrame
Instance.new("UICorner", sidebar)

local container = Instance.new("Frame")
container.Size = UDim2.new(1, -165, 1, -50)
container.Position = UDim2.new(0, 160, 0, 45)
container.BackgroundTransparency = 1
container.Parent = mainFrame

local function hideAll() for _, v in pairs(container:GetChildren()) do v.Visible = false end end

-- ABA TEMAS (FOTOS INTEGRADAS)
local abaTemas = Instance.new("Frame")
abaTemas.Size = UDim2.new(1, 0, 1, 0)
abaTemas.BackgroundTransparency = 1
abaTemas.Visible = false
abaTemas.Parent = container

local themeImg = Instance.new("ImageLabel")
themeImg.Size = UDim2.new(0, 200, 0, 200)
themeImg.Position = UDim2.new(0.5, -100, 0.5, -100)
themeImg.BackgroundTransparency = 1
themeImg.ImageTransparency = 0.7
themeImg.Parent = mainFrame
themeImg.ZIndex = 0

local function applyTheme(tp)
    themeImg.Image = ""
    if tp == "Carnaval" then
        mainStroke.Color = Color3.fromRGB(255, 0, 150)
        themeImg.Image = "rbxassetid://12555314742" -- Sua foto da máscara
    elseif tp == "Pascoa" then
        mainStroke.Color = Color3.fromRGB(0, 255, 120)
        themeImg.Image = "rbxassetid://13501235316" -- Sua foto do ovo
    else
        mainStroke.Color = Color3.fromRGB(60, 60, 60)
    end
end

local function tBtn(txt, y, tp)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.9, 0, 0, 45)
    b.Position = UDim2.new(0.05, 0, 0, y)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
    b.TextColor3 = Color3.new(1,1,1)
    b.Parent = abaTemas
    Instance.new("UICorner", b)
    applyModernStroke(b)
    b.MouseButton1Click:Connect(function() applyTheme(tp) end)
end

tBtn("Tema Normal", 20, "Normal")
tBtn("Tema Carnaval", 75, "Carnaval")
tBtn("Tema Pascoa", 130, "Pascoa")

-- ABA JJs
local abaJJs = Instance.new("Frame")
abaJJs.Size = UDim2.new(1, 0, 1, 0)
abaJJs.BackgroundTransparency = 1
abaJJs.Parent = container

local jjsInput = Instance.new("TextBox")
jjsInput.Size = UDim2.new(0.8, 0, 0, 50)
jjsInput.Position = UDim2.new(0.1, 0, 0.2, 0)
jjsInput.Text = ""
jjsInput.PlaceholderText = "NÚMERO DE JJs"
jjsInput.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
jjsInput.TextColor3 = Color3.new(1,1,1)
jjsInput.Parent = abaJJs
Instance.new("UICorner", jjsInput)
applyModernStroke(jjsInput)

local startBtn = Instance.new("TextButton")
startBtn.Size = UDim2.new(0.8, 0, 0, 55)
startBtn.Position = UDim2.new(0.1, 0, 0.5, 0)
startBtn.Text = "INICIAR"
startBtn.BackgroundColor3 = Color3.fromRGB(0, 150, 90)
startBtn.TextColor3 = Color3.new(1,1,1)
startBtn.Font = Enum.Font.GothamBold
startBtn.Parent = abaJJs
Instance.new("UICorner", startBtn)
applyModernStroke(startBtn, Color3.new(1,1,1))

-- Navegação Sidebar
local function nav(txt, y, f)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.85, 0, 0, 40)
    b.Position = UDim2.new(0.07, 0, 0, y)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(35, 35, 40)
    b.TextColor3 = Color3.new(1,1,1)
    b.Parent = sidebar
    Instance.new("UICorner", b)
    applyModernStroke(b)
    b.MouseButton1Click:Connect(f)
end

nav("JJs", 60, function() hideAll() abaJJs.Visible = true end)
nav("Temas", 115, function() hideAll() abaTemas.Visible = true end)

loginBtn.MouseButton1Click:Connect(function()
    if passBox.Text == SENHA_PRINCIPAL then loginFrame:Destroy() mainFrame.Visible = true end
end)

local credits = Instance.new("TextLabel")
credits.Size = UDim2.new(1, 0, 0, 30)
credits.Position = UDim2.new(0, 0, 1, -30)
credits.Text = "By: Assis"
credits.TextColor3 = Color3.fromRGB(150, 150, 150)
credits.BackgroundTransparency = 1
credits.Parent = sidebar

local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 30, 0, 30)
close.Position = UDim2.new(1, -35, 0, 5)
close.Text = "X"
close.TextColor3 = Color3.new(1,0,0)
close.BackgroundTransparency = 1
close.Parent = mainFrame
close.MouseButton1Click:Connect(function() screenGui:Destroy() end)
