local StarterGui = game:GetService("StarterGui")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local function notificar(titulo, texto)
    StarterGui:SetCore("SendNotification", {
        Title = titulo,
        Text = texto,
        Duration = 5
    })
end

local tempoAdiantado = 30 * 3600 

notificar("🟡 PEDRINHUU CDP", "Ativando Sistema...")

task.wait(math.random(3, 5))

local burlado = false

for _, obj in pairs(LocalPlayer:GetDescendants()) do
    if obj:IsA("NumberValue") or obj:IsA("IntValue") then
        if obj.Value > 0 then
            obj.Value = math.max(0, obj.Value - tempoAdiantado)
            burlado = true
        end
    end
end

local atributos = LocalPlayer:GetAttributes()
for nome, valor in pairs(atributos) do
    if type(valor) == "number" and valor > 0 then
        LocalPlayer:SetAttribute(nome, math.max(0, valor - tempoAdiantado))
        burlado = true
    end
end

if burlado then
    notificar("🟢 PEDRINHUU CDP", "Sistema Ativado!")
    notificar("🟠 PEDRINHUU CDP", "Retirando sua CDP...")
    
    task.wait(math.random(3, 6))
    
    notificar("🟢 PEDRINHUU CDP", "Você esta sem CDP agora!!")
else
    notificar("🔴 PEDRINHUU CDP", "Você não possui CDP ou ela ja foi burlada!")
end
