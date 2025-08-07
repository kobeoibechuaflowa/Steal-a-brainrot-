-- Steal a Brainrot | Tele Lên Trời (Y=75) - Fix bị kéo lại khi trộm
-- by ChatGPT

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer

-- UI setup
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "SkyDropUI"

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 220, 0, 80)
MainFrame.Position = UDim2.new(0.5, -110, 0.2, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.BackgroundTransparency = 0.1
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = true

local toggleButton = Instance.new("TextButton", MainFrame)
toggleButton.Size = UDim2.new(1, -20, 0, 40)
toggleButton.Position = UDim2.new(0, 10, 0, 10)
toggleButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
toggleButton.TextColor3 = Color3.new(1, 1, 1)
toggleButton.Text = "Tele Lên Trời (Fix Rơi Lại Base)"
toggleButton.Font = Enum.Font.Gotham
toggleButton.TextScaled = true

local hideButton = Instance.new("TextButton", MainFrame)
hideButton.Size = UDim2.new(1, -20, 0, 20)
hideButton.Position = UDim2.new(0, 10, 0, 55)
hideButton.BackgroundColor3 = Color3.fromRGB(80, 0, 0)
hideButton.TextColor3 = Color3.new(1, 1, 1)
hideButton.Text = "Ẩn UI"
hideButton.Font = Enum.Font.Gotham
hideButton.TextScaled = true

-- Nút hiện lại UI
local showButton = Instance.new("TextButton", ScreenGui)
showButton.Size = UDim2.new(0, 100, 0, 30)
showButton.Position = UDim2.new(0, 10, 0, 10)
showButton.BackgroundColor3 = Color3.fromRGB(0, 170, 100)
showButton.TextColor3 = Color3.new(1, 1, 1)
showButton.Text = "Hiện UI"
showButton.Font = Enum.Font.Gotham
showButton.TextScaled = true

-- Teleport bằng Tween để tránh server kéo lại
local function smoothTeleportY(yHeight)
	local char = player.Character
	if not char or not char:FindFirstChild("HumanoidRootPart") then return end
	local hrp = char.HumanoidRootPart

	local targetCFrame = CFrame.new(hrp.Position.X, yHeight, hrp.Position.Z)
	local tweenInfo = TweenInfo.new(0.4, Enum.EasingStyle.Linear)

	local tween = TweenService:Create(hrp, tweenInfo, {CFrame = targetCFrame})
	tween:Play()
end

-- Khi bấm nút → chỉ teleport lên trời (rơi tự do), tránh bị kéo về
toggleButton.MouseButton1Click:Connect(function()
	smoothTeleportY(75) -- Y = 75, rơi tự do ngắn
end)

-- Nút ẩn/hiện
hideButton.MouseButton1Click:Connect(function()
	MainFrame.Visible = false
end)

showButton.MouseButton1Click:Connect(function()
	MainFrame.Visible = true
end)
