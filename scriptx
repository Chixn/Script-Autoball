local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local DropBall = ReplicatedStorage.Remotes:WaitForChild("DropBall")
local LocalPlayer = Players.LocalPlayer
local VirtualUser = game:service("VirtualUser")

-- Anti AFK
LocalPlayer.Idled:connect(function()
	VirtualUser:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
	wait(1)
	VirtualUser:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
end)

-- UI Setup
local ScreenGui = Instance.new("ScreenGui", game:GetService("CoreGui"))
ScreenGui.Name = "AutoDropUI"

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 200, 0, 120)
Frame.Position = UDim2.new(0, 20, 0, 100)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.Visible = true
Frame.Active = true
Frame.Draggable = true

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.BackgroundTransparency = 1
Title.Text = " 🏐Auto Drop Ball"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 20

local Toggle = Instance.new("TextButton", Frame)
Toggle.Size = UDim2.new(1, -20, 0, 40)
Toggle.Position = UDim2.new(0, 10, 0, 40)
Toggle.BackgroundColor3 = Color3.fromRGB(50, 150, 50)
Toggle.TextColor3 = Color3.new(1, 1, 1)
Toggle.Font = Enum.Font.SourceSans
Toggle.TextSize = 18
Toggle.Text = "✅ Auto Drop: ON"

local isDropping = true

-- Toggle Button
Toggle.MouseButton1Click:Connect(function()
	isDropping = not isDropping
	if isDropping then
		Toggle.Text = "✅ Auto Drop: ON"
		Toggle.BackgroundColor3 = Color3.fromRGB(50, 150, 50)
	else
		Toggle.Text = "❌ Auto Drop: OFF"
		Toggle.BackgroundColor3 = Color3.fromRGB(150, 50, 50)
	end
end)

-- Auto Drop Loop
task.spawn(function()
	while true do
		if isDropping then
			pcall(function()
				DropBall:FireServer()
			end)
		end
		wait(0.1)
	end
end)

-- Hotkey (RightShift) to toggle UI
game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	if input.KeyCode == Enum.KeyCode.RightShift then
		Frame.Visible = not Frame.Visible
	end
end)
