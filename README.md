-- Mik Scripts Hub 🔥 - Script para Blox Fruits -- Tema: Azul com Raios -- Funções: Auto Farm, Teleport, Fruit Sniper, etc. -- Criado por: [Seu Nome ou Pseudônimo] -- Data: 17/03/2025

local MikHub = Instance.new("ScreenGui") MikHub.Name = "MikScriptsHub" MikHub.Parent = game.CoreGui

-- Função para criar a janela principal (Launcher Azul) local function criarJanela() local Frame = Instance.new("Frame") Frame.Size = UDim2.new(0, 400, 0, 300) Frame.Position = UDim2.new(0.5, -200, 0.5, -150) Frame.BackgroundColor3 = Color3.fromRGB(0, 102, 204) -- Azul escuro Frame.BorderSizePixel = 2 Frame.BorderColor3 = Color3.fromRGB(255, 255, 0) -- Borda amarela (raios) Frame.Parent = MikHub

-- Título do Hub
local Titulo = Instance.new("TextLabel")
Titulo.Size = UDim2.new(1, 0, 0, 50)
Titulo.Position = UDim2.new(0, 0, 0, 0)
Titulo.BackgroundColor3 = Color3.fromRGB(0, 51, 153) -- Azul mais escuro
Titulo.Text = "Mik Scripts Hub 🔥"
Titulo.TextColor3 = Color3.fromRGB(255, 255, 255)
Titulo.Font = Enum.Font.SourceSansBold
Titulo.TextSize = 24
Titulo.Parent = Frame

-- Efeito de "raios" (simulado com bordas e gradiente simples)
local RaioEffect = Instance.new("UIGradient")
RaioEffect.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(0, 102, 204)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(255, 255, 0)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(0, 102, 204))
})
RaioEffect.Parent = Frame
end

-- Funções padrão do Hub local function autoFarm() local player = game.Players.LocalPlayer local character = player.Character or player.CharacterAdded:Wait() local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

while task.wait(1) do
    for _, mob in pairs(game.Workspace.Enemies:GetChildren()) do
        if mob:FindFirstChild("Humanoid") and mob.Humanoid.Health > 0 then
            humanoidRootPart.CFrame = mob.HumanoidRootPart.CFrame * CFrame.new(0, 0, -5)
            game:GetService("VirtualUser"):Click()
            task.wait(0.5)
        end
    end
end
end

local function teleportToIsland() local islands = { ["Windmill"] = CFrame.new(979, 16, 1412), ["Marine Start"] = CFrame.new(-2600, 6, 2050), ["Middle Town"] = CFrame.new(-655, 7, 1532) } local player = game.Players.LocalPlayer local character = player.Character or player.CharacterAdded:Wait() local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

humanoidRootPart.CFrame = islands["Middle Town"] -- Exemplo: teleporta para Middle Town
end

local function fruitSniper() while task.wait(1) do for _, fruit in pairs(game.Workspace:GetChildren()) do if fruit.Name:find("Fruit") then local player = game.Players.LocalPlayer local character = player.Character or player.CharacterAdded:Wait() local humanoidRootPart = character:WaitForChild("HumanoidRootPart") humanoidRootPart.CFrame = fruit.Handle.CFrame task.wait(0.5) end end end end

-- Botões para ativar as funções local function criarBotoes() local Frame = MikHub:FindFirstChild("Frame")

local BotaoFarm = Instance.new("TextButton")
BotaoFarm.Size = UDim2.new(0, 150, 0, 40)
BotaoFarm.Position = UDim2.new(0, 20, 0, 70)
BotaoFarm.BackgroundColor3 = Color3.fromRGB(0, 153, 255)
BotaoFarm.Text = "Auto Farm"
BotaoFarm.TextColor3 = Color3.fromRGB(255, 255, 255)
BotaoFarm.Font = Enum.Font.SourceSans
BotaoFarm.TextSize = 18
BotaoFarm.Parent = Frame
BotaoFarm.MouseButton1Click:Connect(function()
    spawn(autoFarm)
    print("Auto Farm ativado!")
end)

local BotaoTeleport = Instance.new("TextButton")
BotaoTeleport.Size = UDim2.new(0, 150, 0, 40)
BotaoTeleport.Position = UDim2.new(0, 20, 0, 120)
BotaoTeleport.BackgroundColor3 = Color3.fromRGB(0, 153, 255)
BotaoTeleport.Text = "Teleport"
BotaoTeleport.TextColor3 = Color3.fromRGB(255, 255, 255)
BotaoTeleport.Font = Enum.Font.SourceSans
BotaoTeleport.TextSize = 18
BotaoTeleport.Parent = Frame
BotaoTeleport.MouseButton1Click:Connect(function()
    teleportToIsland()
    print("Teleportado!")
end)

local BotaoFruit = Instance.new("TextButton")
BotaoFruit.Size = UDim2.new(0, 150, 0, 40)
BotaoFruit.Position = UDim2.new(0, 20, 0, 170)
BotaoFruit.BackgroundColor3 = Color3.fromRGB(0, 153, 255)
BotaoFruit.Text = "Fruit Sniper"
BotaoFruit.TextColor3 = Color3.fromRGB(255, 255, 255)
BotaoFruit.Font = Enum.Font.SourceSans
BotaoFruit.TextSize = 18
BotaoFruit.Parent = Frame
BotaoFruit.MouseButton1Click:Connect(function()
    spawn(fruitSniper)
    print("Fruit Sniper ativado!")
end)
end

-- Inicializar o Hub criarJanela() criarBotoes()

print("Mik Scripts Hub 🔥 carregado com sucesso!")
