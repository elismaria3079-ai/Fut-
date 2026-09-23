-- LocalScript dentro de StarterGui

local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "AutoGKGui"
screenGui.Parent = playerGui

-- Criar Botão
local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 200, 0, 50)
button.Position = UDim2.new(0.5, -100, 0.8, 0) -- centralizado embaixo
button.Text = "Ativar Auto GK"
button.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.Parent = screenGui

-- Controle
local ativo = false

-- Função de Auto GK
local function autoGK()
    local character = player.Character or player.CharacterAdded:Wait()
    local rootPart = character:WaitForChild("HumanoidRootPart")

    -- Procurar bola no jogo
    local bola = workspace:FindFirstChild("SoccerBall") -- nome típico da bola no Futebol Clássico
    if not bola then return end

    while ativo do
        -- Move o goleiro em direção à bola na horizontal (X/Z)
        local posBola = bola.Position
        local posGK = rootPart.Position

        -- Ajusta posição do goleiro para alinhar com a bola
        local novoX = posBola.X
        local novoZ = posGK.Z -- mantém linha do gol
        rootPart.CFrame = CFrame.new(novoX, posGK.Y, novoZ)

        wait(0.2)
    end
end

-- Clique no botão
button.MouseButton1Click:Connect(function()
    ativo = not ativo
    if ativo then
        button.Text = "Desativar Auto GK"
        autoGK()
    else
        button.Text = "Ativar Auto GK"
    end
end)
