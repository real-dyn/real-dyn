local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
local frame = Instance.new("Frame", screenGui)
local infJumpToggle = Instance.new("TextButton", frame)
local speedLabel = Instance.new("TextLabel", frame)
local speedInput = Instance.new("TextBox", frame)
local jumpPowerLabel = Instance.new("TextLabel", frame)
local jumpPowerInput = Instance.new("TextBox", frame)
local openCloseButton = Instance.new("TextButton", screenGui)
local creditLabel = Instance.new("TextLabel", frame)

-- GUI Setup
screenGui.Name = "ScriptCreationGUI"
screenGui.ResetOnSpawn = false

frame.Size = UDim2.new(0, 400, 0, 300)
frame.Position = UDim2.new(0.5, -200, 0.5, -150)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.Active = true
frame.Draggable = true

infJumpToggle.Size = UDim2.new(0, 150, 0, 30)
infJumpToggle.Position = UDim2.new(0, 20, 0, 70)
infJumpToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
infJumpToggle.TextColor3 = Color3.fromRGB(255, 255, 255)
infJumpToggle.Text = "Infinite Jump: OFF"
infJumpToggle.TextSize = 14

speedLabel.Size = UDim2.new(0, 100, 0, 30)
speedLabel.Position = UDim2.new(0, 20, 0, 120)
speedLabel.Text = "Enter Speed:"
speedLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
speedLabel.BackgroundTransparency = 1
speedLabel.TextSize = 14

speedInput.Size = UDim2.new(0, 150, 0, 30)
speedInput.Position = UDim2.new(0, 130, 0, 120)
speedInput.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
speedInput.TextColor3 = Color3.fromRGB(255, 255, 255)
speedInput.Text = "16"
speedInput.TextSize = 14

jumpPowerLabel.Size = UDim2.new(0, 150, 0, 30)
jumpPowerLabel.Position = UDim2.new(0, 20, 0, 170)
jumpPowerLabel.Text = "Enter Jump Power:"
jumpPowerLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
jumpPowerLabel.BackgroundTransparency = 1
jumpPowerLabel.TextSize = 14

jumpPowerInput.Size = UDim2.new(0, 150, 0, 30)
jumpPowerInput.Position = UDim2.new(0, 130, 0, 170)
jumpPowerInput.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
jumpPowerInput.TextColor3 = Color3.fromRGB(255, 255, 255)
jumpPowerInput.Text = "50"
jumpPowerInput.TextSize = 14

openCloseButton.Size = UDim2.new(0, 150, 0, 30)
openCloseButton.Position = UDim2.new(0, 20, 0, 20)
openCloseButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
openCloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
openCloseButton.Text = "Close GUI"
openCloseButton.TextSize = 14
openCloseButton.Active = true
openCloseButton.Draggable = true

creditLabel.Size = UDim2.new(0, 360, 0, 30)
creditLabel.Position = UDim2.new(0, 20, 0, 250)
creditLabel.Text = "Made by vovanormaldos2"
creditLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
creditLabel.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
creditLabel.BorderSizePixel = 0
creditLabel.TextSize = 14
creditLabel.TextXAlignment = Enum.TextXAlignment.Center

-- Infinite Jump Logic
local infJump = false
infJumpToggle.MouseButton1Click:Connect(function()
	infJump = not infJump
	infJumpToggle.Text = infJump and "Infinite Jump: ON" or "Infinite Jump: OFF"
end)

game:GetService("UserInputService").JumpRequest:Connect(function()
	if infJump then
		local character = player.Character or player.CharacterAdded:Wait()
		if character then
			local humanoid = character:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
			end
		end
	end
end)

-- Speed Input Logic
speedInput.FocusLost:Connect(function(enterPressed)
	if enterPressed then
		local speed = tonumber(speedInput.Text)
		if speed then
			local character = player.Character or player.CharacterAdded:Wait()
			local humanoid = character:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.WalkSpeed = speed
			end
		end
	end
end)

-- Jump Power Input Logic
jumpPowerInput.FocusLost:Connect(function(enterPressed)
	if enterPressed then
		local jumpPower = tonumber(jumpPowerInput.Text)
		if jumpPower then
			local character = player.Character or player.CharacterAdded:Wait()
			local humanoid = character:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid.UseJumpPower = true
				humanoid.JumpPower = jumpPower
			end
		end
	end
end)

-- Open/Close Button Logic
local guiVisible = true
openCloseButton.MouseButton1Click:Connect(function()
	guiVisible = not guiVisible
	frame.Visible = guiVisible
	openCloseButton.Text = guiVisible and "Close GUI" or "Open GUI"
end)
