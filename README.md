-- Obtém o serviço de jogadores
local Players = game:GetService("Players")

-- Tabela de administradores
local administradores = {
    [123456789] = true -- Substitua pelo UserId do administrador
}

-- Função para banir um jogador
local function banirJogador(jogador, motivo)
    jogador:Kick("Você foi banido! Motivo: " .. motivo)
end

-- Evento de mensagem no chat
Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(message)
        if administradores[player.UserId] then
            if string.sub(message, 1, 5) == "!ban " then
                local jogadorNome = string.sub(message, 6)
                local jogador = Players:FindFirstChild(jogadorNome)
                if jogador then
                    banirJogador(jogador, "Banimento por administrador")
                end
            end
        end
    end)
end)
