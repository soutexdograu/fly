-- Cria uma tela GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Cria um botão retangular
local Button = Instance.new("TextButton")
Button.Size = UDim2.new(0, 200, 0, 50)
Button.Position = UDim2.new(0, 10, 0, 10)
Button.Text = "Voar"
Button.Parent = ScreenGui

-- Variáveis para controlar o estado de voo
local flying = false
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local mouse = player:GetMouse()

-- Função para ativar/desativar o voo
local function toggleFly()
    flying = not flying
    if flying then
        humanoid.PlatformStand = true
    else
        humanoid.PlatformStand = false
    end
end

-- Adiciona a função ao botão
Button.MouseButton1Click:Connect(toggleFly)

-- Função para controlar o movimento durante o voo
local function fly()
    while flying do
        character:TranslateBy(mouse.Hit.lookVector * 0.1)
        wait(0.1)
    end
end

-- Inicia a função de movimento no voo
fly()
