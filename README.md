--[[ 
    CLUR HUB v9 - ASSIS PRECEDENT
    SENHA: Clurscript3 | CONFIG: DvloperAssis
]]

local SENHA_PRINCIPAL = "Clurscript3"
local SENHA_CONFIG = "DvloperAssis"
local DISCORD_LINK = "https://discord.gg/zraSa5W2Qg"

local Player = game.Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local TweenService = game:GetService("TweenService")

-- Limpeza
if PlayerGui:FindFirstChild("ClurHubAssis") then PlayerGui.ClurHubAssis:Destroy() end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ClurHubAssis"
screenGui.Parent = PlayerGui
screenGui.ResetOnSpawn = false

-- Funções de Estilo
local function addBorder(parent, color, thickness)
    local stroke = Instance.new("UIStroke")
    stroke.Thickness = thickness or 1.8
    stroke.Color = color or Color3.fromRGB(100, 100, 100)
    stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    stroke.Parent = parent
    return stroke
end

local function applyWaveEffect(frame)
    local container = Instance.new("Frame")
    container.Size = UDim2.new(1, 0, 1, 0)
    container.BackgroundTransparency = 1
    container.ClipsDescendants = true
    container.ZIndex = 0
    container.Parent = frame
    
    for i = 1, 12 do
        local dot = Instance.new("Frame")
        dot.Size = UDim2.new(0, 2, 0, 2)
        dot.BackgroundColor3 = (i % 2 == 0) and Color3.new(1,1,1) or Color3.fromRGB(150,150,150)
        dot.Position = UDim2.new(math.random(), 0, math.random(), 0)
        dot.Parent = container
        Instance.new("UICorner", dot).CornerRadius = UDim.new(1,0)
        
        task.spawn(function()
            local t = 0
            while frame and frame.Parent do
                t = t + 0.04
                dot.Position = UDim2.new(
                    (math.sin(t + i) * 0.48) + 0.5, 0,
                    (math.cos(t * 0.7 + i) * 0.48) + 0.5, 0
                )
                task.wait()
            end
        end)
    end
end

-- TELA DE LOGIN
local loginFrame = Instance.new("Frame")
loginFrame.Size = UDim2.new(0, 400, 0, 300)
loginFrame.Position = UDim2.new(0.5, -200, 0.5, -150)
loginFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
loginFrame.Active = true
loginFrame.Draggable = true
loginFrame.Parent = screenGui
Instance.new("UICorner", loginFrame)
addBorder(loginFrame, Color3.fromRGB(88, 101, 242), 2.5)
applyWaveEffect(loginFrame)

local passBox = Instance.new("TextBox")
passBox.Size = UDim2.new(0.8, 0, 0, 45)
passBox.Position = UDim2.new(0.1, 0, 0.35, 0)
passBox.Text = ""
passBox.PlaceholderText = "SENHA..."
passBox.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
passBox.TextColor3 = Color3.new(1,1,1)
passBox.Parent = loginFrame
Instance.new("UICorner", passBox)
addBorder(passBox)

local loginBtn = Instance.new("TextButton")
loginBtn.Size = UDim2.new(0.8, 0, 0, 50)
loginBtn.Position = UDim2.new(0.1, 0, 0.6, 0)
loginBtn.Text = "ENTRAR"
loginBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
loginBtn.TextColor3 = Color3.new(1,1,1)
loginBtn.Font = Enum.Font.GothamBold
loginBtn.Parent = loginFrame
Instance.new("UICorner", loginBtn)
addBorder(loginBtn, Color3.new(1,1,1))

-- BOTAO DISCORD (IMAGEM REAL + NAVEGADOR)
local discordBtn = Instance.new("ImageButton")
discordBtn.Size = UDim2.new(0, 50, 0, 50)
discordBtn.Position = UDim2.new(0.5, -25, 0.82, 0)
discordBtn.Image = "rbxassetid://6031320306" -- Logo Discord Branca
discordBtn.BackgroundColor3 = Color3.fromRGB(88, 101, 242)
discordBtn.Parent = loginFrame
Instance.new("UICorner", discordBtn).CornerRadius = UDim.new(1, 0)
addBorder(discordBtn, Color3.new(1,1,1))

local dcTip = Instance.new("TextLabel")
dcTip.Size = UDim2.new(0, 100, 0, 25)
dcTip.Position = UDim2.new(0.5, -50, -0.6, 0)
dcTip.Text = "DISCORD"
dcTip.Visible = false
dcTip.BackgroundColor3 = Color3.new(0,0,0)
dcTip.TextColor3 = Color3.new(1,1,1)
dcTip.Font = Enum.Font.GothamBold
dcTip.Parent = discordBtn
Instance.new("UICorner", dcTip)

discordBtn.MouseEnter:Connect(function() dcTip.Visible = true end)
discordBtn.MouseLeave:Connect(function() dcTip.Visible = false end)
discordBtn.MouseButton1Click:Connect(function()
    local req = (syn and syn.request) or (http and http.request) or http_request or (fluxus and fluxus.request) or request
    if req then
        req({Url = DISCORD_LINK, Method = "GET"})
    else
        setclipboard(DISCORD_LINK)
    end
end)

-- HUB PRINCIPAL
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 550, 0, 400)
mainFrame.Position = UDim2.new(0.5, -275, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
mainFrame.Visible = false
mainFrame.Parent = screenGui
Instance.new("UICorner", mainFrame)
local mainStroke = addBorder(mainFrame, Color3.fromRGB(60,60,60), 2.5)
applyWaveEffect(mainFrame)

-- Sidebar
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 140, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
sidebar.Parent = mainFrame
Instance.new("UICorner", sidebar)

local credits = Instance.new("TextLabel")
credits.Size = UDim2.new(1, 0, 0, 30)
credits.Position = UDim2.new(0, 0, 1, -30)
credits.Text = "By: Assis"
credits.TextColor3 = Color3.fromRGB(150, 150, 150)
credits.BackgroundTransparency = 1
credits.Parent = sidebar

-- Conteúdo
local container = Instance.new("Frame")
container.Size = UDim2.new(1, -155, 1, -50)
container.Position = UDim2.new(0, 145, 0, 45)
container.BackgroundTransparency = 1
container.Parent = mainFrame

local function hide() for _, v in pairs(container:GetChildren()) do v.Visible = false end end

-- ABA JJs
local abaJJs = Instance.new("Frame")
abaJJs.Size = UDim2.new(1, 0, 1, 0)
abaJJs.BackgroundTransparency = 1
abaJJs.Parent = container

local jjsInput = Instance.new("TextBox")
jjsInput.Size = UDim2.new(0.8, 0, 0, 45)
jjsInput.Position = UDim2.new(0.1, 0, 0.2, 0)
jjsInput.Text = ""
jjsInput.PlaceholderText = "QUANTOS JJs?"
jjsInput.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
jjsInput.TextColor3 = Color3.new(1,1,1)
jjsInput.Parent = abaJJs
Instance.new("UICorner", jjsInput)
addBorder(jjsInput)

local startBtn = Instance.new("TextButton")
startBtn.Size = UDim2.new(0.8, 0, 0, 50)
startBtn.Position = UDim2.new(0.1, 0, 0.5, 0)
startBtn.Text = "INICIAR TREINO"
startBtn.BackgroundColor3 = Color3.fromRGB(0, 120, 60)
startBtn.TextColor3 = Color3.new(1,1,1)
startBtn.Font = Enum.Font.GothamBold
startBtn.Parent = abaJJs
Instance.new("UICorner", startBtn)
addBorder(startBtn, Color3.new(1,1,1))

-- ABA TEMAS (FOTOS)
local abaTemas = Instance.new("Frame")
abaTemas.Size = UDim2.new(1, 0, 1, 0)
abaTemas.BackgroundTransparency = 1
abaTemas.Visible = false
abaTemas.Parent = container

local overlay = Instance.new("Frame")
overlay.Size = UDim2.new(1,0,1,0)
overlay.BackgroundTransparency = 1
overlay.Parent = mainFrame

local function apply(tp)
    overlay:ClearAllChildren()
    if tp == "Carnaval" then
        mainStroke.Color = Color3.fromRGB(255, 200, 0)
        local img = Instance.new("ImageLabel")
        img.Size = UDim2.new(0, 120, 0, 120)
        img.Position = UDim2.new(0.5, -60, 0.5, -60)
        img.Image = "rbxassetid://12555314742"
        img.BackgroundTransparency = 1
        img.Parent = overlay
    elseif tp == "Pascoa" then
        mainStroke.Color = Color3.fromRGB(0, 255, 150)
        for i = 1, 4 do
            local img = Instance.new("ImageLabel")
            img.Size = UDim2.new(0, 45, 0, 45)
            img.Image = "rbxassetid://13501235316"
            img.BackgroundTransparency = 1
            img.Position = (i==1 and UDim2.new(0,10,0,10)) or (i==2 and UDim2.new(1,-55,0,10)) or (i==3 and UDim2.new(0,10,1,-55)) or UDim2.new(1,-55,1,-55)
            img.Parent = overlay
        end
    else
        mainStroke.Color = Color3.fromRGB(60,60,60)
    end
end

local function tButton(txt, y, tp)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.9, 0, 0, 40)
    b.Position = UDim2.new(0.05, 0, 0, y)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    b.TextColor3 = Color3.new(1,1,1)
    b.Parent = abaTemas
    Instance.new("UICorner", b)
    addBorder(b)
    b.MouseButton1Click:Connect(function() apply(tp) end)
end

tButton("Tema Normal", 20, "Normal")
tButton("Tema Carnaval", 70, "Carnaval")
tButton("Tema Pascoa", 120, "Pascoa")

-- Sidebar Nav
local function nav(txt, y, f)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.85, 0, 0, 40)
    b.Position = UDim2.new(0.07, 0, 0, y)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    b.TextColor3 = Color3.new(1,1,1)
    b.Parent = sidebar
    Instance.new("UICorner", b)
    addBorder(b)
    b.MouseButton1Click:Connect(f)
end

nav("JJs", 60, function() hide() abaJJs.Visible = true end)
nav("Temas", 110, function() hide() abaTemas.Visible = true end)

-- Login Logic
loginBtn.MouseButton1Click:Connect(function()
    if passBox.Text == SENHA_PRINCIPAL then loginFrame:Destroy() mainFrame.Visible = true end
end)

-- Fechar
local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 30, 0, 30)
close.Position = UDim2.new(1,-35,0,5)
close.Text = "X"
close.TextColor3 = Color3.new(1,0,0)
close.BackgroundTransparency = 1
close.Parent = mainFrame
close.MouseButton1Click:Connect(function() screenGui:Destroy() end)
