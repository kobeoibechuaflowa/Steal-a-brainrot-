-- Steal a Brainrot | Tele Lên Trời (Rơi tự do) + Tele Xuống + UI Toggle
-- by ChatGPT

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local toggled = false

-- Tạo UI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "SkyDropUI"

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 220, 0, 100)
MainFrame.Position = UDim2.new(0.5, -110, 0.2, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BackgroundTransparency = 0.1
MainFrame.Active = true
MainFrame.Draggable = true

local toggleButton = Instance.new("TextButton", MainFrame)
toggleButton.Size = UDim2.new(1, -20, 0, 40)
toggleButton.Position = UDim2.new(0, 10, 0, 10)
toggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
toggleButton.TextColor3 = Color3.new(1, 1, 1)
toggleButton.Text = "Tele Lên Trời (Rơi)"
toggleButton.Font = Enum.Font.Gotham
toggleButton.TextScaled = true

local hideButton = Instance.new("TextButton", MainFrame)
hideButton.Size = UDim2.new(1, -20, 0, 30)
hideButton.Position = UDim2.new(0, 10, 0, 60)
hideButton.BackgroundColor3 = Color3.fromRGB(80, 0, 0)
hideButton.TextColor3 = Color3.new(1, 1, 1)
hideButton.Text = "Ẩn/Hiện UI (Click)"
hideButton.Font = Enum.Font.Gotham
hideButton.TextScaled = true

-- Nút điều khiển
toggleButton.MouseButton1Click:Connect(function()
	local char = player.Character
	if not char or not char:FindFirstChild("HumanoidRootPart") then return end
	local hrp = char.HumanoidRootPart

	toggled = not toggled

	if toggled then
		-- Tele lên trời cao → cho rơi tự do
		hrp.CFrame = CFrame.new(hrp.Position.X, 999, hrp.Position.Z)
		toggleButton.Text = "Tele Xuống Đất"
	else
		-- Tele xuống gần mặt đất, ngoài base
		local offsetX = math.random(-100, 100)
		local offsetZ = math.random(-100, 100)
		hrp.CFrame = CFrame.new(hrp.Position.X + offsetX, 25, hrp.Position.Z + offsetZ)
		toggleButton.Text = "Tele Lên Trời (Rơi)"
	end
end)

-- Ẩn/hiện UI
hideButton.MouseButton1Click:Connect(function()
	MainFrame.Visible = not MainFrame.Visible
end)
