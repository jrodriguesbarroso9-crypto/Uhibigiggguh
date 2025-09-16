-- Cria um botão na tela
local ScreenGui = Instance.new("ScreenGui")
local Button = Instance.new("TextButton")

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

Button.Size = UDim2.new(0, 200, 0, 50)
Button.Position = UDim2.new(0.5, -100, 0.8, 0) -- Meio da tela embaixo
Button.Text = "Ativar NoClip"
Button.Parent = ScreenGui

-- Variável de controle
local noclipAtivo = false

-- Função para ativar/desativar noclip
Button.MouseButton1Click:Connect(function()
	noclipAtivo = not noclipAtivo
	if noclipAtivo then
		Button.Text = "Desativar NoClip"
	else
		Button.Text = "Ativar NoClip"
	end
end)

-- Loop para aplicar o efeito
game:GetService("RunService").Stepped:Connect(function()
	if noclipAtivo then
		local character = game.Players.LocalPlayer.Character
		if character then
			for _, part in pairs(character:GetDescendants()) do
				if part:IsA("BasePart") then
					part.CanCollide = false
				end
			end
		end
	end
end)
