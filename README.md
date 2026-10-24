local Players = game:GetService("Players")

local player = Players.LocalPlayer
local gui = script.Parent
local label = gui:WaitForChild("Moedalabel")

local function atualizar(valor)
	label.Text = tostring(valor)
end

local function conectar(moeda)
	atualizar(moeda.Value)
	moeda.Changed:Connect(atualizar)
end

local moeda = player:FindFirstChild("Moeda")
if moeda then
	conectar(moeda)
else
	player.ChildAdded:Connect(function(child)
		if child.Name == "Moeda" and child:IsA("IntValue") then
			conectar(child)
		end
	end)
end

