--[[ 
    CLUR HUB v7 - ASSIS PREMIUM EDITION
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

-- Funções Visuais
local function createCorner(p, r) Instance.new("UICorner", p).CornerRadius = r or UDim.new(0, 10) end

local function createNeonLine(parent, color)
    local line = Instance.new("UIStroke")
    line.Thickness = 2.5
    line.Color = color or Color3.fromRGB(60, 60, 60)
    line.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    line.Parent = parent
    return line
end

-- TELA DE LOGIN
local loginFrame = Instance.new("Frame")
loginFrame.Size = UDim2.new(0, 420, 0, 320)
loginFrame.Position = UDim2.new(0.5, -210, 0.5, -160)
loginFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
loginFrame.Active = true
loginFrame.Draggable = true
loginFrame.Parent = screenGui
createCorner(loginFrame)
local loginNeon = createNeonLine(loginFrame, Color3.fromRGB(88, 101, 242))

local loginTitle = Instance.new("TextLabel")
loginTitle.Size = UDim2.new(1, 0, 0, 80)
loginTitle.Text = "CLUR HUB"
loginTitle.TextColor3 = Color3.new(1,1,1)
loginTitle.Font = Enum.Font.GothamBold
loginTitle.TextSize = 30
loginTitle.BackgroundTransparency = 1
loginTitle.Parent = loginFrame

local passInput = Instance.new("TextBox")
passInput.Size = UDim2.new(0.8, 0, 0, 50)
passInput.Position = UDim2.new(0.1, 0, 0.35, 0)
passInput.Text = ""
passInput.PlaceholderText = "INSIRA A SENHA"
passInput.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
passInput.TextColor3 = Color3.new(1,1,1)
passInput.Parent = loginFrame
createCorner(passInput)

local loginBtn = Instance.new("TextButton")
loginBtn.Size = UDim2.new(0.8, 0, 0, 55)
loginBtn.Position = UDim2.new(0.1, 0, 0.6, 0)
loginBtn.Text = "DESBLOQUEAR"
loginBtn.BackgroundColor3 = Color3.fromRGB(88, 101, 242)
loginBtn.TextColor3 = Color3.new(1,1,1)
loginBtn.Font = Enum.Font.GothamBold
loginBtn.Parent = loginFrame
createCorner(loginBtn)

-- BOTÃO DISCORD COM ICONE E NOME NO HOVER
local discordBtn = Instance.new("ImageButton")
discordBtn.Size = UDim2.new(0, 50, 0, 50)
discordBtn.Position = UDim2.new(0.5, -25, 0.82, 0)
discordBtn.Image = "rbxassetid://15623048952" -- Ícone Discord Real
discordBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
discordBtn.Parent = loginFrame
createCorner(discordBtn, UDim.new(1, 0))

local dcHover = Instance.new("TextLabel")
dcHover.Size = UDim2.new(0, 100, 0, 20)
dcHover.Position = UDim2.new(0.5, -50, -0.6, 0)
dcHover.Text = "DISCORD"
dcHover.TextColor3 = Color3.new(1,1,1)
dcHover.BackgroundTransparency = 0.2
dcHover.BackgroundColor3 = Color3.new(0,0,0)
dcHover.Font = Enum.Font.GothamBold
dcHover.Visible = false
dcHover.Parent = discordBtn
createCorner(dcHover, UDim.new(0,5))

discordBtn.MouseEnter:Connect(function() dcHover.Visible = true end)
discordBtn.MouseLeave:Connect(function() dcHover.Visible = false end)
discordBtn.MouseButton1Click:Connect(function()
    if request then request({Url = DISCORD_LINK, Method = "GET"}) else setclipboard(DISCORD_LINK) end
end)

-- HUB PRINCIPAL
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 550, 0, 400)
mainFrame.Position = UDim2.new(0.5, -275, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
mainFrame.Visible = false
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui
createCorner(mainFrame)
local mainNeon = createNeonLine(mainFrame, Color3.fromRGB(60, 60, 60)) -- Linha Normal

-- Sidebar e Conteúdo
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 150, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
sidebar.Parent = mainFrame
createCorner(sidebar)

local container = Instance.new("Frame")
container.Size = UDim2.new(1, -160, 1, -50)
container.Position = UDim2.new(0, 155, 0, 45)
container.BackgroundTransparency = 1
container.Parent = mainFrame

local function hideAll() for _, v in pairs(container:GetChildren()) do v.Visible = false end end

-- IMAGENS DOS TEMAS
local temaOverlay = Instance.new("Frame")
temaOverlay.Size = UDim2.new(1, 0, 1, 0)
temaOverlay.BackgroundTransparency = 1
temaOverlay.ZIndex = 0
temaOverlay.Parent = mainFrame

local function applyTema(tipo)
    temaOverlay:ClearAllChildren()
    if tipo == "Normal" then
        mainNeon.Color = Color3.fromRGB(60, 60, 60)
    elseif tipo == "Carnaval" then
        mainNeon.Color = Color3.fromRGB(255, 200, 0) -- Neon Dourado
        local img = Instance.new("ImageLabel")
        img.Size = UDim2.new(0, 100, 0, 100)
        img.Position = UDim2.new(0.5, -50, 0.4, -50)
        img.Image = "rbxassetid://12555314742" -- Foto Máscara
        img.BackgroundTransparency = 1
        img.ImageTransparency = 0.5
        img.Parent = temaOverlay
    elseif tipo == "Pascoa" then
        mainNeon.Color = Color3.fromRGB(0, 255, 150) -- Neon Verde Água
        for i = 1, 4 do
            local img = Instance.new("ImageLabel")
            img.Size = UDim2.new(0, 40, 0, 40)
            img.Image = "rbxassetid://13501235316" -- Foto Ovinho
            img.BackgroundTransparency = 1
            img.Position = (i==1 and UDim2.new(0,5,0,5)) or (i==2 and UDim2.new(1,-45,0,5)) or (i==3 and UDim2.new(0,5,1,-45)) or UDim2.new(1,-45,1,-45)
            img.Parent = temaOverlay
        end
    end
end

-- ABAS (JJs, Temas, Config)
local abaJJs = Instance.new("Frame")
abaJJs.Size = UDim2.new(1,0,1,0)
abaJJs.BackgroundTransparency = 1
abaJJs.Parent = container

local jjsInput = Instance.new("TextBox")
jjsInput.Size = UDim2.new(0.8,0,0,50)
jjsInput.Position = UDim2.new(0.1,0,0.2,0)
jjsInput.Text = ""
jjsInput.PlaceholderText = "QUANTIDADE JJs"
jjsInput.BackgroundColor3 = Color3.fromRGB(30,30,30)
jjsInput.TextColor3 = Color3.new(1,1,1)
jjsInput.Parent = abaJJs
createCorner(jjsInput)

local startBtn = Instance.new("TextButton")
startBtn.Size = UDim2.new(0.8,0,0,55)
startBtn.Position = UDim2.new(0.1,0,0.5,0)
startBtn.Text = "INICIAR"
startBtn.BackgroundColor3 = Color3.fromRGB(0, 180, 100)
startBtn.TextColor3 = Color3.new(1,1,1)
startBtn.Font = Enum.Font.GothamBold
startBtn.Parent = abaJJs
createCorner(startBtn)

-- Aba Temas
local abaTemas = Instance.new("Frame")
abaTemas.Size = UDim2.new(1,0,1,0)
abaTemas.BackgroundTransparency = 1
abaTemas.Visible = false
abaTemas.Parent = container

local function createTemaBtn(txt, y, tipo)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.9,0,0,45)
    b.Position = UDim2.new(0.05,0,0,y)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(40,40,40)
    b.TextColor3 = Color3.new(1,1,1)
    b.Parent = abaTemas
    createCorner(b)
    b.MouseButton1Click:Connect(function() applyTema(tipo) end)
end

createTemaBtn("Tema Normal (Neon)", 20, "Normal")
createTemaBtn("Tema Carnaval (Máscara)", 75, "Carnaval")
createTemaBtn("Tema Páscoa (Ovos)", 130, "Pascoa")

-- Lógica Sidebar
local function nav(txt, y, f)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.85,0,0,40)
    b.Position = UDim2.new(0.07,0,0,y)
    b.Text = txt
    b.Parent = sidebar
    createCorner(b)
    b.MouseButton1Click:Connect(f)
end

nav("JJs", 60, function() hideAll() abaJJs.Visible = true end)
nav("Temas", 110, function() hideAll() abaTemas.Visible = true end)
nav("Config", 160, function() hideAll() end) -- Adicionar lógica de senha depois

-- LOGIN
loginBtn.MouseButton1Click:Connect(function()
    if passInput.Text == SENHA_PRINCIPAL then loginFrame:Destroy() mainFrame.Visible = true end
end)

-- FECHAR
local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 30, 0, 30)
close.Position = UDim2.new(1,-35,0,5)
close.Text = "X"
close.TextColor3 = Color3.new(1,0,0)
close.BackgroundTransparency = 1
close.Parent = mainFrame
close.MouseButton1Click:Connect(function() screenGui:Destroy() end)

-- CHAT JJS
local ext = {"UM", "DOIS", "TRÊS", "QUATRO", "CINCO", "SEIS", "SETE", "OITO", "NOVE", "DEZ", "ONZE", "DOZE", "TREZE", "QUATORZE", "QUINZE"}
startBtn.MouseButton1Click:Connect(function()
    local n = tonumber(jjsInput.Text)
    if n then
        for i = 1, n do
            local m = (ext[i] or tostring(i)) .. " !"
            local ts = game:GetService("TextChatService")
            if ts.ChatVersion == Enum.ChatVersion.TextChatService then
                ts.TextChannels.RBXGeneral:SendAsync(m)
            else
                game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(m, "All")
            end
            task.wait(2.2)
        end
    end
end)

local credits = Instance.new("TextLabel")
credits.Size = UDim2.new(1,0,0,30)
credits.Position = UDim2.new(0,0,1,-30)
credits.Text = "By: Assis"
credits.BackgroundTransparency = 1
credits.TextColor3 = Color3.new(0.6,0.6,0.6)
credits.Parent = sidebar
