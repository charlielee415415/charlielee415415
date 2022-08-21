local spamming = false
local player = game.Players.LocalPlayer
local char = player.Character
repeat wait() char = player.Character until char
char.Archivable = true
local old = char:Clone()
function reset()
	local charr = player.Character
	local framer = char:FindFirstChild("HumanoidRootPart")
	local frame
	if framer then
		frame = framer.CFrame
	end
	if charr then
		local new = old:Clone()
		if new then
			new.Parent = workspace
			char:Remove()
			player.Character = new
			char = player.Character
			workspace.CurrentCamera.CameraSubject = new:WaitForChild("Humanoid")
			player.Character:SetPrimaryPartCFrame(frame)
		end
	end
end
function spam()
	spamming = true
	while wait() do
		if spamming == true then
			for i,v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
				if v:IsA("SpecialMesh") then v:Destroy() end
			end
			for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
				if v:IsA("Accessory") then
					v.Parent = game.Workspace
				end
			end
			--reset()
			game.ReplicatedStorage.RemoteEvents.AvatarOriginalCharacter:FireServer()
		else
			break
		end
	end
end
local mouse = player:GetMouse()
if mouse then
	mouse.KeyDown:Connect(function(key)
		if key:lower() == "q" then
			if spamming == false then 
				spamming = true 
			else 
				if spamming == true then 
					spamming = false
				end
			end
		end
	end)
end
