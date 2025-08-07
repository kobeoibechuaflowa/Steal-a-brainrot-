local RunService = game:GetService("RunService")
local noClipEnabled = false

local function setNoClip(enable)
    local char = player.Character
    if not char then return end
    for _, part in pairs(char:GetChildren()) do
        if part:IsA("BasePart") then
            part.CanCollide = not enable
        end
    end
end

local noClipConnection

toggleButton.MouseButton1Click:Connect(function()
    noClipEnabled = not noClipEnabled
    if noClipEnabled then
        setNoClip(true)
        -- Tele lên trời
        smoothTeleportY(75)

        -- Giữ NoClip liên tục để tránh bị server kéo lại
        noClipConnection = RunService.Stepped:Connect(function()
            setNoClip(true)
        end)
    else
        if noClipConnection then
            noClipConnection:Disconnect()
            noClipConnection = nil
        end
        setNoClip(false)
    end
end)
