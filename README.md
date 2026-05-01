--// MINI GUI PERFIL - Muestra el nombre real del usuario

local Players = game:GetService("Players")
local player = Players.LocalPlayer

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "PerfilPersonal"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = player:WaitForChild("PlayerGui")

-- GUI Principal
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 260, 0, 90)
MainFrame.Position = UDim2.new(0.5, -130, 0.5, -45)
MainFrame.BackgroundColor3 = Color3.fromRGB(22, 22, 28)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 12)

-- Foto de Perfil (Izquierda)
local ProfileImage = Instance.new("ImageLabel")
ProfileImage.Size = UDim2.new(0, 70, 0, 70)
ProfileImage.Position = UDim2.new(0, 12, 0.5, -35)
ProfileImage.BackgroundTransparency = 1
ProfileImage.Parent = MainFrame
Instance.new("UICorner", ProfileImage).CornerRadius = UDim.new(1, 0)

-- Nombre del usuario real (Derecha)
local UsernameLabel = Instance.new("TextLabel")
UsernameLabel.Size = UDim2.new(0, 150, 0, 40)
UsernameLabel.Position = UDim2.new(0, 95, 0.5, -20)
UsernameLabel.BackgroundTransparency = 1
UsernameLabel.Text = player.Name  -- ← Aquí muestra el nombre real
UsernameLabel.TextColor3 = Color3.new(1, 1, 1)
UsernameLabel.TextScaled = true
UsernameLabel.TextXAlignment = Enum.TextXAlignment.Left
UsernameLabel.Font = Enum.Font.GothamBold
UsernameLabel.Parent = MainFrame

-- Botón "-" para Cerrar
local MinimizeBtn = Instance.new("TextButton")
MinimizeBtn.Size = UDim2.new(0, 26, 0, 26)
MinimizeBtn.Position = UDim2.new(1, -34, 0, 8)
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(200, 40, 40)
MinimizeBtn.Text = "−"
MinimizeBtn.TextColor3 = Color3.new(1,1,1)
MinimizeBtn.TextScaled = true
MinimizeBtn.Font = Enum.Font.GothamBold
MinimizeBtn.Parent = MainFrame
Instance.new("UICorner", MinimizeBtn).CornerRadius = UDim.new(0, 8)

-- === MINI CÍRCULO MOVIBLE ===
local MiniCircle = Instance.new("ImageLabel")
MiniCircle.Size = UDim2.new(0, 52, 0, 52)
MiniCircle.Position = UDim2.new(0.08, 0, 0.75, 0)
MiniCircle.BackgroundTransparency = 1
MiniCircle.Visible = false
MiniCircle.Active = true
MiniCircle.Draggable = true
MiniCircle.Parent = ScreenGui

Instance.new("UICorner", MiniCircle).CornerRadius = UDim.new(1, 0)

-- Botón invisible para mejor detección de clicks
local OpenButton = Instance.new("TextButton")
OpenButton.Size = UDim2.new(1, 0, 1, 0)
OpenButton.BackgroundTransparency = 1
OpenButton.Text = ""
OpenButton.Parent = MiniCircle

-- Cargar foto de perfil real
local userId = player.UserId
local content, ready = Players:GetUserThumbnailAsync(userId, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size420x420)

if ready then
    ProfileImage.Image = content
    MiniCircle.Image = content
end

-- Funcionalidad de abrir y cerrar
MinimizeBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    MiniCircle.Visible = true
end)

OpenButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    MiniCircle.Visible = false
end)

print("✅ GUI Personal cargada correctamente - Mostrando: " .. player.Name)
