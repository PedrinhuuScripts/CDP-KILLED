local sg = game:GetService("StarterGui")
local lp = game.Players.LocalPlayer

-- Função de notificação (Visual que você pediu)
local function notify(title, text, color)
    sg:SetCore("SendNotification", {
        Title = title,
        Text = text,
        Duration = 5,
        -- Ícone opcional, se quiser pode remover
    })
end

-- Essa função varre o jogador inteiro procurando qualquer número > 0
local function nuclearSweep()
    local foundSomething = false
    
    -- 1. Varredura de Objetos (NumberValue, IntValue)
    -- GetDescendants pega TUDO: filhos, netos, bisnetos...
    for _, obj in pairs(lp:GetDescendants()) do
        if obj:IsA("NumberValue") or obj:IsA("IntValue") or obj:IsA("DoubleConstrainedValue") then
            if obj.Value > 0 then
                -- Filtro de segurança: ignora configurações gráficas ou de câmera comuns
                if not obj.Name:lower():find("camera") and not obj.Name:lower():find("sensitivity") then
                    obj.Value = 0
                    foundSomething = true
                end
            end
        end
    end
    
    -- 2. Varredura de Atributos (Sistema novo do Roblox)
    local attributes = lp:GetAttributes()
    for name, value in pairs(attributes) do
        if type(value) == "number" and value > 0 then
            lp:SetAttribute(name, 0)
            foundSomething = true
        end
    end
    
    return foundSomething
end


-- EXECUÇÃO DO SISTEMA
notify("🟡 PEDRINHUU CDP", "Iniciando varredura profunda...", "")

task.wait(math.random(2, 4)) -- Pequeno delay para "simular" processamento

-- Tenta limpar
local sucesso = nuclearSweep()

if sucesso then
    notify("🟢 PEDRINHUU CDP", "Valores encontrados e zerados!")
    notify("🟠 PEDRINHUU CDP", "Finalizando processo...")
    
    task.wait(2)
    
    notify("🟢 PEDRINHUU CDP", "Você esta sem CDP agora!!")
else
    -- Se mesmo varrendo tudo não achou, então o sistema é 100% Server-Side
    -- Ou a variável está dentro de um script privado (inacessível)
    notify("🔴 PEDRINHUU CDP", "Nenhuma CDP detectada na memória do cliente!") 
end
