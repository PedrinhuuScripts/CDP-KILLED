-- Esse script tenta zerar os valores de tempo locais assim que você entra
-- Ele simula que você está 30 horas (108.000 segundos) no futuro

local tempoAdiantado = 30 * 3600 -- 30 horas em segundos
local player = game.Players.LocalPlayer

print("Tentando burlar CDP ao entrar...")

-- Função para procurar e "limpar" os valores de Cooldown
local function limparCooldowns()
    -- Procura em pastas comuns de dados do jogador
    local alvos = {player:FindFirstChild("Data"), player:FindFirstChild("leaderstats"), player:FindFirstChild("Cooldowns")}
    
    for _, pasta in pairs(alvos) do
        if pasta then
            for _, valor in pairs(pasta:GetChildren()) do
                if valor:IsA("NumberValue") or valor:IsA("IntValue") then
                    -- Subtrai o tempo ou zera o valor
                    valor.Value = 0 
                    print("Zerei o valor de: " .. valor.Name)
                end
            end
        end
    end
end

-- Executa imediatamente
limparCooldowns()

-- Se o kick for baseado em uma UI (tela) que aparece, tentamos deletar a tela de kick
player.PlayerGui.ChildAdded:Connect(function(child)
    if child.Name:lower():find("kick") or child.Name:lower():find("aviso") then
        child:Destroy()
        print("Tentei deletar a interface de Kick!")
    end
end)
