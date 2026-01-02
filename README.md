--[[ 
    CLUR HUB v11 - ASSIS PRIVATE
    SENHA: Clurscript3 | CONFIG: DvloperAssis
]]

local SENHA_PRINCIPAL = "Clurscript3"
local DISCORD_LINK = "https://discord.gg/zraSa5W2Qg"

local Player = game.Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local RunService = game:GetService("RunService")
local TextChatService = game:GetService("TextChatService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

if PlayerGui:FindFirstChild("ClurHubAssis") then PlayerGui.ClurHubAssis:Destroy() end

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ClurHubAssis"
screenGui.Parent = PlayerGui
screenGui.ResetOnSpawn = false

-- FUNÇÃO: CRIAR VÁRIAS BOLINHAS NAS LINHAS (TRAÇADO)
local function createManyOrbitParticles(frame)
    for i = 1, 30 do -- Aumentado para 30 bolinhas nas linhas
        local dot = Instance.new("Frame")
        dot.Size = UDim2.new(0, 3, 0, 3)
        dot.BackgroundColor3 = (i % 2 == 0) and Color3.new(1, 1, 1) or Color3.fromRGB(200, 200, 200)
        dot.ZIndex = 10
        dot.Parent = frame
        Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)

        task.spawn(function()
            local t = (i * (math.pi * 2 / 30))
            while frame and frame.Parent do
                t = t + 0.015
                local x = math.clamp(math.cos(t) * 1.2, -0.5, 0.5) + 0.5
                local y = math.clamp(math.sin(t) * 1.2, -0.5, 0.5) + 0.5
                dot.Position = UDim2.new(x, -1, y, -1)
                RunService.RenderStepped:Wait()
            end
        end)
    end
end

-- FUNÇÃO: BOLINHAS CAINDO NO FUNDO
local function createFallingParticles(frame)
    local container = Instance.new("Frame")
    container.Size = UDim2.new(1, 0, 1, 0)
    container.BackgroundTransparency = 1
    container.ClipsDescendants = true
    container.ZIndex = 1
    container.Parent = frame

    for i = 1, 25 do
        local p = Instance.new("Frame")
        p.Size = UDim2.new(0, 2, 0, 2)
        p.BackgroundColor3 = Color3.new(1, 1, 1)
        p.BackgroundTransparency = 0.5
        p.Parent = container
        Instance.new("UICorner", p).CornerRadius = UDim.new(1, 0)

        task.spawn(function()
            p.Position = UDim2.new(math.random(), 0, math.random(), 0)
            while frame and frame.Parent do
                local newY = p.Position.Y.Scale + 0.002
                if newY > 1 then newY = -0.05 end
                p.Position = UDim2.new(p.Position.X.Scale, 0, newY, 0)
                RunService.RenderStepped:Wait()
            end
        end)
    end
end

-- MENU PRINCIPAL (MÓVEL)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 550, 0, 400)
mainFrame.Position = UDim2.new(0.5, -275, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 12)
mainFrame.Active = true -- Permite interação
mainFrame.Draggable = true -- Permite arrastar
mainFrame.Visible = false
mainFrame.Parent = screenGui
Instance.new("UICorner", mainFrame)

-- Camada da Foto do Tema
local themeDisplay = Instance.new("ImageLabel")
themeDisplay.Size = UDim2.new(0.6, 0, 0.6, 0)
themeDisplay.Position = UDim2.new(0.5, -0.3, 0.5, -0.3)
themeDisplay.AnchorPoint = Vector2.new(0.5, 0.5)
themeDisplay.Position = UDim2.new(0.65, 0, 0.5, 0)
themeDisplay.BackgroundTransparency = 1
themeDisplay.ImageTransparency = 0.8
themeDisplay.ZIndex = 2
themeDisplay.Parent = mainFrame

local mainStroke = Instance.new("UIStroke", mainFrame)
mainStroke.Thickness = 2
mainStroke.Color = Color3.fromRGB(80, 80, 80)

createFallingParticles(mainFrame)
createManyOrbitParticles(mainFrame)

-- Sidebar e Container
local sidebar = Instance.new("Frame")
sidebar.Size = UDim2.new(0, 150, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(15, 15, 18)
sidebar.ZIndex = 3
sidebar.Parent = mainFrame
Instance.new("UICorner", sidebar)

local container = Instance.new("Frame")
container.Size = UDim2.new(1, -160, 1, -60)
container.Position = UDim2.new(0, 155, 0, 50)
container.BackgroundTransparency = 1
container.ZIndex = 4
container.Parent = mainFrame

-- ABA JJs (CORRIGIDA)
local abaJJs = Instance.new("Frame")
abaJJs.Size = UDim2.new(1,0,1,0)
abaJJs.BackgroundTransparency = 1
abaJJs.Parent = container

local jjsInput = Instance.new("TextBox")
jjsInput.Size = UDim2.new(0.9, 0, 0, 45)
jjsInput.PlaceholderText = "QUANTIDADE DE JJs"
jjsInput.Text = ""
jjsInput.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
jjsInput.TextColor3 = Color3.new(1,1,1)
jjsInput.Parent = abaJJs
Instance.new("UICorner", jjsInput)

local startBtn = Instance.new("TextButton")
startBtn.Size = UDim2.new(0.9, 0, 0, 50)
startBtn.Position = UDim2.new(0, 0, 0.3, 0)
startBtn.Text = "INICIAR JJs"
startBtn.BackgroundColor3 = Color3.fromRGB(0, 150, 80)
startBtn.TextColor3 = Color3.new(1,1,1)
startBtn.Parent = abaJJs
Instance.new("UICorner", startBtn)

-- LÓGICA DO CHAT JJs
local ext = {"UM", "DOIS", "TRÊS", "QUATRO", "CINCO", "SEIS", "SETE", "OITO", "NOVE", "DEZ"}
startBtn.MouseButton1Click:Connect(function()
    local qtd = tonumber(jjsInput.Text)
    if qtd then
        for i = 1, qtd do
            local msg = (ext[i] or tostring(i)) .. " !"
            if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
                TextChatService.TextChannels.RBXGeneral:SendAsync(msg)
            else
                ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(msg, "All")
            end
            task.wait(2.5)
        end
    end
end)

-- ABA TEMAS (COM FOTOS)
local abaTemas = Instance.new("Frame")
abaTemas.Size = UDim2.new(1,0,1,0)
abaTemas.BackgroundTransparency = 1
abaTemas.Visible = false
abaTemas.Parent = container

local function aplicarTema(nome)
    if nome == "Carnaval" then
        themeDisplay.Image = "rbxassetid://12555314742"
        mainStroke.Color = Color3.fromRGB(255, 0, 150)
    elseif nome == "Pascoa" then
        themeDisplay.Image = "rbxassetid://13501235316"
        mainStroke.Color = Color3.fromRGB(0, 255, 120)
    else
        themeDisplay.Image = ""
        mainStroke.Color = Color3.fromRGB(80, 80, 80)
    end
end

local function criarBotaoTema(txt, y, t)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.9, 0, 0, 40)
    b.Position = UDim2.new(0, 0, 0, y)
    b.Text = txt
    b.BackgroundColor3 = Color3.fromRGB(40, 40, 45)
    b.TextColor3 = Color3.new(1,1,1)
    b.Parent = abaTemas
    Instance.new("UICorner", b)
    b.MouseButton1Click:Connect(function() aplicarTema(t) end)
end

criarBotaoTema("Tema Normal", 0, "Normal")
criarBotaoTema("Tema Carnaval", 50, "Carnaval")
criarBotaoTema("Tema Páscoa", 100, "Pascoa")

-- NAVEGAÇÃO
local function nav(txt, y, f)
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(0.8, 0, 0, 40)
    b.Position = UDim2.new(0.1, 0, 0, y)
    b.Text = txt
    b.Parent = sidebar
    Instance.new("UICorner", b)
    b.MouseButton1Click:Connect(f)
end

nav("JJs", 60, function() abaJJs.Visible = true abaTemas.Visible = false end)
nav("Temas", 110, function() abaJJs.Visible = false abaTemas.Visible = true end)

-- LOGIN (PARA TESTAR RÁPIDO)
local loginFrame = Instance.new("Frame")
loginFrame.Size = UDim2.new(0, 350, 0, 250)
loginFrame.Position = UDim2.new(0.5, -175, 0.5, -125)
loginFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
loginFrame.Active = true
loginFrame.Draggable = true
loginFrame.Parent = screenGui
Instance.new("UICorner", loginFrame)

local pass = Instance.new("TextBox")
pass.Size = UDim2.new(0.8, 0, 0, 40)
pass.Position = UDim2.new(0.1, 0, 0.3, 0)
pass.PlaceholderText = "SENHA"
pass.Parent = loginFrame

local btn = Instance.new("TextButton")
btn.Size = UDim2.new(0.8, 0, 0, 40)
btn.Position = UDim2.new(0.1, 0, 0.6, 0)
btn.Text = "ENTRAR"
btn.Parent = loginFrame

btn.MouseButton1Click:Connect(function()
    if pass.Text == SENHA_PRINCIPAL then
        loginFrame:Destroy()
        mainFrame.Visible = true
    end
end)
