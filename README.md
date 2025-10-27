local HttpService = game:GetService("HttpService")

-- Coloque seu link do webhook aqui:
local webhookUrl = "https://discord.com/api/webhooks/1432163980847218798/9sTdOInP1cBKsgP8wQ9HQ2zZOKNxXJB0lqR_bZ_ensEcHIxfMcgbFOxHf3RqgQPeo8pe"

-- Função para enviar o link do servidor ao webhook
local function enviarLinkParaWebhook(linkServidor)
    local payload = HttpService:JSONEncode({servidor_link = linkServidor})
    local success, response = pcall(function()
        return HttpService:PostAsync(webhookUrl, payload, Enum.HttpContentType.ApplicationJson)
    end)
    if success then
        print("Link enviado com sucesso ao webhook!")
    else
        warn("Falha ao enviar o link:", response)
    end
end

-- Exemplo de como pedir o link ao usuário via comando no chat:
game.Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(msg)
        if string.sub(msg, 1, 10) == "!servidor " then
            local linkServidor = string.sub(msg, 11)
            enviarLinkParaWebhook(linkServidor)
            player:Kick("Seu link foi enviado ao webhook!") -- Opcional: kicka o jogador após enviar
        end
    end)
end)
