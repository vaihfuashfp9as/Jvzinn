local ESPEnabled = false  -- Variável para controlar o estado do ESP
local ESPObjects = {}  -- Armazena referências aos objetos ESP para facilitar a remoção

-- Função para ativar o ESP com linhas
local function activateESP()
    for _, player in ipairs(game.Players:GetPlayers()) do
        if player ~= Player and player.Team ~= Player.Team then
            local character = player.Character
            if character and character:FindFirstChild("HumanoidRootPart") then
                -- Cria uma linha que conecta o HumanoidRootPart do personagem ao centro da tela
                local line = Drawing.new("Line")
                line.Color = Color3.new(1, 0, 0)  -- Cor da linha (vermelha)
                line.Thickness = 1.5
                line.Transparency = 1
                ESPObjects[player.Name] = line  -- Armazena a linha criada

                -- Atualiza a posição da linha constantemente
                game:GetService("RunService").RenderStepped:Connect(function()
                    if character and character:FindFirstChild("HumanoidRootPart") then
                        local screenPosition, onScreen = workspace.CurrentCamera:WorldToViewportPoint(character.HumanoidRootPart.Position)
                        if onScreen then
                            line.Visible = true
                            line.From = Vector2.new(workspace.CurrentCamera.ViewportSize.X / 2, workspace.CurrentCamera.ViewportSize.Y)
                            line.To = Vector2.new(screenPosition.X, screenPosition.Y)
                        else
                            line.Visible = false
                        end
                    else
                        line.Visible = false
                    end
                end)
            end
        end
    end
end

-- Função para desativar o ESP
local function deactivateESP()
    for _, line in pairs(ESPObjects) do
        line:Remove()  -- Remove as linhas de desenho
    end
    ESPObjects = {}  -- Limpa a tabela
end

-- Adiciona o botão de toggle no Tab3 para controlar o ESP
Tab3:AddToggle({
    Name = "Toggle ESP",
    Default = false,
    Callback = function(state)
        ESPEnabled = state
        if ESPEnabled then
            activateESP()
        else
            deactivateESP()
        end
    end
})
