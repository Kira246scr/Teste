--[[ 
    CLUR HUB v8 - ASSIS PRIVATE
    SENHA: Clurscript3 | CONFIG: DvloperAssis
]]

local SENHA_PRINCIPAL = "Clurscript3"
local SENHA_CONFIG = "DvloperAssis"
local DISCORD_LINK = "https://discord.gg/zraSa5W2Qg"

local Player = game.Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")

if PlayerGui:FindFirstChild("ClurHubAssis") then PlayerGui.ClurHubAssis:Destroy() end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ClurHubAssis"
screenGui.Parent = PlayerGui
screenGui.ResetOnSpawn = false

-- FUNÇÃO PARA O EFEITO DE "ONDA DE BOLINHAS" NAS BORDAS
local function aplicarEfeitoOnda(frame)
    local particleContainer = Instance.new("Frame")
    particleContainer.Size = UDim2.new(1, 0, 1, 0)
    particleContainer.BackgroundTransparency = 1
    particleContainer.ClipsDescendants = true
    particleContainer.Parent = frame

    for i = 1, 15 do
        local dot = Instance.new("Frame")
        dot.Size = UDim2.new(0, 3, 0, 3)
        dot.BackgroundColor3 = i % 2 == 0 and Color3.new(1,1,1) or Color3.fromRGB(150, 150, 150)
        dot.BorderSizePixel = 0
        dot.Parent = particleContainer
        Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)

        task.spawn(function()
            local t = 0
            while task.wait() do
                t = t + 0.05
                local x = (math.sin(t + i) * 0.45) + 0.5
                local y = (math.cos(t * 0.8 + i) * 0.45) + 0.5
                dot.Position = UDim2.new(x, 0, y, 0)
            end
        end)
    end
end

-- TELA DE LOGIN
local loginFrame = Instance.new("Frame")
loginFrame.Size = UDim2.new(0, 420, 0, 320)
loginFrame.Position = UDim2.new(0.5, -210, 0.5, -160)
loginFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 12)
loginFrame.Active = true
loginFrame.Draggable = true
loginFrame.Parent = screenGui
Instance.new("UICorner", loginFrame)
aplicarEfeitoOnda(loginFrame)

-- Borda Neon com Linha
local stroke = Instance.new("UIStroke")
stroke.Thickness = 2
stroke.Color = Color3.fromRGB(100, 100, 100)
stroke.Parent = loginFrame

local loginTitle = Instance.new("TextLabel")
loginTitle.Size = UDim2.new(1, 0, 0, 70)
loginTitle.Text = "CLUR HUB"
loginTitle.TextColor3 = Color3.new(1,1,1)
loginTitle.Font = Enum.Font.GothamBold
loginTitle.TextSize = 28
loginTitle.BackgroundTransparency = 1
loginTitle.Parent = loginFrame

local passBox = Instance.new("TextBox")
passBox.Size = UDim2.new(0.8, 0, 0, 50)
passBox.Position = UDim2.new(0.1, 0, 0.35, 0)
passBox.Text = ""
passBox.PlaceholderText = ""
passBox.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
passBox.TextColor3 = Color3.new(1,1,1)
passBox.Parent = loginFrame
Instance.new("UICorner", passBox)
Instance.new("UIStroke", passBox).Color = Color3.fromRGB(80, 80, 80)

local loginBtn = Instance.new("TextButton")
loginBtn.Size = UDim2.new(0.8, 0, 0, 50)
loginBtn.Position = UDim2.new(0.1, 0, 0.6, 0)
loginBtn.Text = "DESBLOQUEAR"
loginBtn.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
loginBtn.TextColor3 = Color3.new(1,1,1)
loginBtn.Font = Enum.Font.GothamBold
loginBtn.Parent = loginFrame
Instance.new("UICorner", loginBtn)
Instance.new("UIStroke", loginBtn).Color = Color3.fromRGB(255, 255, 255)

-- BOTÃO DISCORD (IMAGEM + NAVEGADOR)
local discordBtn = Instance.new("ImageButton")
discordBtn.Size = UDim2.new(0, 55, 0, 55)
discordBtn.Position = UDim2.new(0.5, -27, 0.82, 0)
discordBtn.Image = "rbxassetid://15623048952" -- Ícone Real do Discord
discordBtn.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
discordBtn.Parent = loginFrame
Instance.new("UICorner", discordBtn).CornerRadius = UDim.new(1, 0)

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
    local request = (syn and syn.request) or (http and http.request) or http_request or request
    if request then
        request({Url = DISCORD_LINK, Method = "GET"})
    else
        setclipboard(DISCORD_LINK)
    end
end)

-- MENU PRINCIPAL
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 550, 0, 400)
mainFrame.Position = UDim2.new(0.5, -275, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 12)
mainFrame.Visible = false
mainFrame.Parent = screenGui
Instance.new("UICorner", mainFrame)
local mainStroke = Instance.new("UIStroke", mainFrame)
mainStroke.Thickness = 2.5
mainStroke.Color = Color3.fromRGB(60, 60, 60)
aplicarEfeitoOnda(mainFrame)

-- Sidebar
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 150, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(18, 18, 22)
sidebar.Parent = mainFrame
Instance.new("UICorner", sidebar)

local assisTxt = Instance.new("TextLabel")
assisTxt.Size = UDim2.new(1,0,0,30)
assisTxt.Position = UDim2.new(0,0,1,-30)
assisTxt.Text = "By: Assis"
assisTxt.TextColor3 = Color3.new(0.6,0.6,0.6)
assisTxt.BackgroundTransparency = 1
assisTxt.Parent = sidebar

-- Container
local container = Instance.new("Frame")
container.Size = UDim2.new(1, -165, 1, -50)
container.Position = UDim2.new(0, 155, 0, 45)
container.BackgroundTransparency = 1
container.Parent = mainFrame

local function hideAll()
    for _, v in pairs(container:GetChildren()) do v.Visible = false end
end

-- ABA JJs
local abaJJs = Instance.new("Frame")
abaJJs.Size = UDim2.new(1,0,1,0)
abaJJs.BackgroundTransparency = 1
abaJJs.Parent = container

local jjsInput = Instance.new("TextBox")
jjsInput.Size = UDim2.new(0.8, 0, 0, 50)
jjsInput.Position = UDim2.new(0.1, 0, 0.2, 0)
jjsInput.Text = ""
jjsInput.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
jjsInput.TextColor3 = Color3.new(1,1,1)
jjsInput.Parent = abaJJs
Instance.new("UICorner", jjsInput)
Instance.new("UIStroke", jjsInput).Color = Color3.fromRGB(100, 100, 100)

local startBtn = Instance.new("TextButton")
startBtn.Size = UDim2.new(0.8, 0, 0, 55)
startBtn.Position = UDim2.new(0.1, 0, 0.5, 0)
startBtn.Text = "INICIAR"
startBtn.BackgroundColor3 = Color3.fromRGB(0, 150, 80)
startBtn.TextColor3 = Color3.new(1,1,1)
startBtn.Font = Enum.Font.GothamBold
startBtn.Parent = abaJJs
Instance.new("UICorner", startBtn)
Instance.new("UIStroke", startBtn).Color = Color3.new(1,1,1)

-- ABA TEMAS (FOTOS REAIS)
local abaTemas = Instance.new("Frame")
abaTemas.Size = UDim2.new(1,0,1,0)
abaTemas.BackgroundTransparency = 1
abaTemas.Visible = false
abaTemas.Parent = container

local overlay = Instance.new("Frame")
overlay.Size = UDim2.new(1,0,1,0)
overlay.BackgroundTransparency = 1
overlay.Parent = mainFrame

local function setTema(tipo)
    overlay:ClearAllChildren()
    if tipo == "Carnaval" then
        mainStroke.Color = Color3.fromRGB(255, 200, 0)
        local img = Instance.new("ImageLabel")
        img.Size = UDim2.new(0, 150, 0, 150)
        img.Position = UDim2.new(0.5, -75, 0.5, -75)
        img.Image = "rbxassetid://12555314742" -- Foto Máscara
        img.BackgroundTransparency = 1
        img.ImageTransparency = 0.6
        img.Parent = overlay
    elseif tipo == "Pascoa" then
        mainStroke.Color = Color3.fromRGB(0, 255, 120)
        for i = 1, 4 do
            local img = Instance.new("ImageLabel")
            img.Size = UDim2.new(0, 50, 0, 50)
            img.Image = "rbxassetid://13501235316" -- Foto Ovinho Real
            img.BackgroundTransparency = 1
            img.Position = (i==1 and UDim2.new(0,10,0,10)) or (i==2 and UDim2.new(1,-60,0,10)) or (i==3 and UDim2.new(0,10,1,-60)) or UDim2.new(1,-60,1,-60)
            img.Parent = overlay
        end
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
    Instance.new("UIStroke", b).Color = Color3.fromRGB(100, 100, 100)
    b.MouseButton1Click:Connect(function() setTema(tp) end)
end

tBtn("Tema Normal (Cinza Neon)", 20, "Normal")
tBtn("Tema Carnaval (Foto Máscara)", 75, "Carnaval")
tBtn("Tema Páscoa (Foto Ovos)", 130, "Pascoa")

-- Sidebar Nav
local function nav(txt, y, f)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.85, 0, 0, 40)
    b.Position = UDim2.new(0.07, 0, 0, y)
    b.Text = txt
    b.Parent = sidebar
    Instance.new("UICorner", b)
    Instance.new("UIStroke", b).Color = Color3.fromRGB(100, 100, 100)
    b.MouseButton1Click:Connect(f)
end

nav("JJs", 60, function() hideAll() abaJJs.Visible = true end)
nav("Temas", 110, function() hideAll() abaTemas.Visible = true end)
nav("Config", 160, function() hideAll() end)

-- Login Logic
loginBtn.MouseButton1Click:Connect(function()
    if passBox.Text == SENHA_PRINCIPAL then loginFrame:Destroy() mainFrame.Visible = true end
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

-- JJs Sistema
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
