--[[ 
    CLUR HUB v6 - OFFICIAL ASSIS EDITION
    SENHA: Clurscript3 | CONFIG: DvloperAssis
    LINK DISCORD: https://discord.gg/zraSa5W2Qg
]]

local SENHA_PRINCIPAL = "Clurscript3"
local SENHA_CONFIG = "DvloperAssis"
local DISCORD_LINK = "https://discord.gg/zraSa5W2Qg"

local Player = game.Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")

-- Limpeza de UI anterior
if PlayerGui:FindFirstChild("ClurHubAssis") then PlayerGui.ClurHubAssis:Destroy() end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ClurHubAssis"
screenGui.Parent = PlayerGui
screenGui.ResetOnSpawn = false

local function createCorner(p, r) 
    Instance.new("UICorner", p).CornerRadius = r or UDim.new(0, 12) 
end

-- TELA DE LOGIN
local loginFrame = Instance.new("Frame")
loginFrame.Size = UDim2.new(0, 420, 0, 320)
loginFrame.Position = UDim2.new(0.5, -210, 0.5, -160)
loginFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 18)
loginFrame.BorderSizePixel = 0
loginFrame.Active = true
loginFrame.Draggable = true
loginFrame.Parent = screenGui
createCorner(loginFrame)

local loginTitle = Instance.new("TextLabel")
loginTitle.Size = UDim2.new(1, 0, 0, 80)
loginTitle.Text = "CLUR HUB"
loginTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
loginTitle.Font = Enum.Font.GothamBold
loginTitle.TextSize = 30
loginTitle.BackgroundTransparency = 1
loginTitle.Parent = loginFrame

local passInput = Instance.new("TextBox")
passInput.Size = UDim2.new(0.8, 0, 0, 50)
passInput.Position = UDim2.new(0.1, 0, 0.35, 0)
passInput.Text = ""
passInput.PlaceholderText = "INSIRA A SENHA"
passInput.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
passInput.TextColor3 = Color3.new(1,1,1)
passInput.Font = Enum.Font.Gotham
passInput.Parent = loginFrame
createCorner(passInput)

local loginBtn = Instance.new("TextButton")
loginBtn.Size = UDim2.new(0.8, 0, 0, 55)
loginBtn.Position = UDim2.new(0.1, 0, 0.6, 0)
loginBtn.Text = "LOGAR"
loginBtn.BackgroundColor3 = Color3.fromRGB(114, 137, 218)
loginBtn.TextColor3 = Color3.new(1,1,1)
loginBtn.Font = Enum.Font.GothamBold
loginBtn.TextSize = 18
loginBtn.Parent = loginFrame
createCorner(loginBtn)

-- BOTAO DISCORD (IMAGEM REAL)
local discordBtn = Instance.new("ImageButton")
discordBtn.Size = UDim2.new(0, 50, 0, 50)
discordBtn.Position = UDim2.new(0.5, -25, 0.82, 0)
discordBtn.Image = "rbxassetid://10650965780" -- Logo oficial Discord Asset
discordBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 45)
discordBtn.Parent = loginFrame
createCorner(discordBtn, UDim.new(1, 0))

discordBtn.MouseButton1Click:Connect(function()
    if setclipboard then setclipboard(DISCORD_LINK) end
    if request then 
        request({Url = DISCORD_LINK, Method = "GET"})
    elseif syn and syn.request then
        syn.request({Url = DISCORD_LINK, Method = "GET"})
    end
end)

-- HUB PRINCIPAL
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 550, 0, 400)
mainFrame.Position = UDim2.new(0.5, -275, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 15)
mainFrame.Visible = false
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui
createCorner(mainFrame)

-- Sidebar
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 150, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
sidebar.Parent = mainFrame
createCorner(sidebar)

local credits = Instance.new("TextLabel")
credits.Size = UDim2.new(1, 0, 0, 40)
credits.Position = UDim2.new(0, 0, 1, -30)
credits.Text = "Créditos: Assis"
credits.TextColor3 = Color3.fromRGB(120, 120, 130)
credits.Font = Enum.Font.Gotham
credits.BackgroundTransparency = 1
credits.Parent = sidebar

-- Conteudo
local container = Instance.new("Frame")
container.Size = UDim2.new(1, -160, 1, -50)
container.Position = UDim2.new(0, 155, 0, 45)
container.BackgroundTransparency = 1
container.Parent = mainFrame

local function hideAll()
    for _, v in pairs(container:GetChildren()) do v.Visible = false end
end

-- ABA JJs
local abaJJs = Instance.new("Frame")
abaJJs.Size = UDim2.new(1, 0, 1, 0)
abaJJs.BackgroundTransparency = 1
abaJJs.Parent = container

local jjsInput = Instance.new("TextBox")
jjsInput.Size = UDim2.new(0.8, 0, 0, 50)
jjsInput.Position = UDim2.new(0.1, 0, 0.2, 0)
jjsInput.Text = ""
jjsInput.PlaceholderText = "QUANTIDADE DE JJs"
jjsInput.BackgroundColor3 = Color3.fromRGB(30, 30, 35)
jjsInput.TextColor3 = Color3.new(1,1,1)
jjsInput.Parent = abaJJs
createCorner(jjsInput)

local startBtn = Instance.new("TextButton")
startBtn.Size = UDim2.new(0.8, 0, 0, 50)
startBtn.Position = UDim2.new(0.1, 0, 0.5, 0)
startBtn.Text = "EXECUTAR"
startBtn.BackgroundColor3 = Color3.fromRGB(0, 180, 100)
startBtn.TextColor3 = Color3.new(1,1,1)
startBtn.Font = Enum.Font.GothamBold
startBtn.Parent = abaJJs
createCorner(startBtn)

-- ABA TEMAS
local abaTemas = Instance.new("Frame")
abaTemas.Size = UDim2.new(1, 0, 1, 0)
abaTemas.BackgroundTransparency = 1
abaTemas.Visible = false
abaTemas.Parent = container

local temaOverlay = Instance.new("Frame")
temaOverlay.Size = UDim2.new(1, 0, 1, 0)
temaOverlay.BackgroundTransparency = 1
temaOverlay.Parent = mainFrame
temaOverlay.ZIndex = 0

local function applyTema(tipo)
    temaOverlay:ClearAllChildren()
    if tipo == "Carnaval" then
        local mask = Instance.new("TextLabel")
        mask.Text = "🎭"
        mask.Size = UDim2.new(0, 60, 0, 60)
        mask.Position = UDim2.new(0.5, -30, 0, -30)
        mask.BackgroundTransparency = 1
        mask.TextSize = 50
        mask.Parent = temaOverlay
    elseif tipo == "Pascoa" then
        -- Páscoa Elegante
        local decor = {"🐰", "🥚", "🌸", "🍫"}
        local positions = {
            UDim2.new(0,10,0,10), UDim2.new(1,-40,0,10),
            UDim2.new(0,10,1,-40), UDim2.new(1,-40,1,-40),
            UDim2.new(0.5,-20,1,-40)
        }
        for i, p in pairs(positions) do
            local t = Instance.new("TextLabel")
            t.Text = decor[math.random(1,#decor)]
            t.Size = UDim2.new(0,35,0,35)
            t.Position = p
            t.BackgroundTransparency = 1
            t.TextSize = 25
            t.Parent = temaOverlay
        end
    end
end

local bCar = Instance.new("TextButton")
bCar.Size = UDim2.new(0.9,0,0,45)
bCar.Position = UDim2.new(0.05,0,0.1,0)
bCar.Text = "Tema Carnaval"
bCar.Parent = abaTemas
createCorner(bCar)
bCar.MouseButton1Click:Connect(function() applyTema("Carnaval") end)

local bPas = Instance.new("TextButton")
bPas.Size = UDim2.new(0.9,0,0,45)
bPas.Position = UDim2.new(0.05,0,0.3,0)
bPas.Text = "Tema Páscoa PRO"
bPas.Parent = abaTemas
createCorner(bPas)
bPas.MouseButton1Click:Connect(function() applyTema("Pascoa") end)

-- ABA CONFIG (SENHA)
local abaConfig = Instance.new("Frame")
abaConfig.Size = UDim2.new(1, 0, 1, 0)
abaConfig.BackgroundTransparency = 1
abaConfig.Visible = false
abaConfig.Parent = container

local function askConfig()
    abaConfig:ClearAllChildren()
    local cInp = Instance.new("TextBox")
    cInp.Size = UDim2.new(0.8,0,0,50)
    cInp.Position = UDim2.new(0.1,0,0.4,0)
    cInp.PlaceholderText = "SENHA CONFIG"
    cInp.Text = ""
    cInp.BackgroundColor3 = Color3.fromRGB(30,30,35)
    cInp.TextColor3 = Color3.new(1,1,1)
    cInp.Parent = abaConfig
    createCorner(cInp)
    
    cInp.FocusLost:Connect(function()
        if cInp.Text == SENHA_CONFIG then
            abaConfig:ClearAllChildren()
            local l = Instance.new("TextLabel")
            l.Size = UDim2.new(1,0,1,0)
            l.Text = "EM BREVE"
            l.TextColor3 = Color3.new(0.5,0.5,0.5)
            l.TextSize = 35
            l.BackgroundTransparency = 1
            l.Parent = abaConfig
        end
    end)
end

-- Navegação sidebar
local function navBtn(txt, y, f)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.8,0,0,45)
    b.Position = UDim2.new(0.1,0,0,y)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(40,40,45)
    b.TextColor3 = Color3.new(1,1,1)
    b.Font = Enum.Font.GothamBold
    b.Parent = sidebar
    createCorner(b, UDim.new(0,8))
    b.MouseButton1Click:Connect(f)
end

navBtn("JJs", 60, function() hideAll() abaJJs.Visible = true end)
navBtn("Temas", 115, function() hideAll() abaTemas.Visible = true end)
navBtn("Config", 170, function() hideAll() abaConfig.Visible = true askConfig() end)

-- Lógica de Desbloqueio
loginBtn.MouseButton1Click:Connect(function()
    if passInput.Text == SENHA_PRINCIPAL then
        loginFrame:Destroy()
        mainFrame.Visible = true
    else
        loginBtn.Text = "SENHA INCORRETA"
        task.wait(1)
        loginBtn.Text = "LOGAR"
    end
end)

-- Fechar
local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 30, 0, 30)
close.Position = UDim2.new(1, -35, 0, 5)
close.Text = "X"
close.TextColor3 = Color3.new(1,0,0)
close.BackgroundTransparency = 1
close.Parent = mainFrame
close.MouseButton1Click:Connect(function() screenGui:Destroy() end)

-- SISTEMA JJS CHAT (FIXED)
local ext = {"UM", "DOIS", "TRÊS", "QUATRO", "CINCO", "SEIS", "SETE", "OITO", "NOVE", "DEZ", "ONZE", "DOZE", "TREZE", "QUATORZE", "QUINZE"}
startBtn.MouseButton1Click:Connect(function()
    local n = tonumber(jjsInput.Text)
    if n then
        startBtn.Text = "RODANDO..."
        startBtn.BackgroundColor3 = Color3.fromRGB(150, 100, 0)
        for i = 1, n do
            local m = (ext[i] or tostring(i)) .. " !"
            local chat = game:GetService("TextChatService")
            if chat.ChatVersion == Enum.ChatVersion.TextChatService then
                chat.TextChannels.RBXGeneral:SendAsync(m)
            else
                game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(m, "All")
            end
            task.wait(2.2)
        end
        startBtn.Text = "EXECUTAR"
        startBtn.BackgroundColor3 = Color3.fromRGB(0, 180, 100)
    end
end)
