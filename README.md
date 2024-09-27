--Abaixo esatrá a lib da nossa Ui
local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/7yhx/Gabiscriptsfrontlineshacks/main/source.lua"))()
/main/source.lua"))()

local UI = Lib:Create{
   Theme = "Dark", -- or any other theme
   Size = UDim2.new(0, 555, 0, 400) -- default
}

local Main = UI:Tab{
   Name = "inicio"
}

local Divider = Main:Divider{
   Name = "inicio shit"
}

local QuitDivider = Main:Divider{
   Name = "sair"
}





-- Definindo as cores das equipes
local teamColors = {
    ["Amiga"] = Color3.fromRGB(0, 0, 255), -- Azul
    ["Inimiga"] = Color3.fromRGB(255, 0, 0) -- Vermelho
}

-- Variável para controlar o estado do script
local scriptAtivo = true

-- Função para mudar a cor das equipes
local function mudarCorEquipe()
    if scriptAtivo then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Team.Name == "Amiga" then
                player.TeamColor = teamColors["Amiga"]
            elseif player.Team.Name == "Inimiga" then
                player.TeamColor = teamColors["Inimiga"]
            end
        end
    end
end

-- Conectando a função ao evento de mudança de equipe
game.Players.PlayerAdded:Connect(function(player)
    player:GetPropertyChangedSignal("Team"):Connect(mudarCorEquipe)
end)

-- Função para ativar/desativar o script com a tecla "P"
local UserInputService = game:GetService("UserInputService")

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if input.KeyCode == Enum.KeyCode.P and not gameProcessed then
        scriptAtivo = not scriptAtivo
        if scriptAtivo then
            print("Script ativado")
        else
            print("Script desativado")
        end
    end
end)

-- Chamando a função inicialmente para definir as cores
mudarCorEquipe()
