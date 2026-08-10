--[[
========================================================
        APEX COMMUNITY V15
        Created by Vex
        FOR YOUR OWN ROBLOX STUDIO GAME
========================================================
]]

--------------------------------------------------------
-- SERVICES
--------------------------------------------------------

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Lighting = game:GetService("Lighting")
local TweenService = game:GetService("TweenService")

local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

--------------------------------------------------------
-- CLEAN OLD GUI
--------------------------------------------------------

for _, name in ipairs({
	"ApexCommunityV14",
	"ApexCommunityV15",
	"ApexKeySystem",
	"ApexCommunityPanel"
}) do
	local old = PlayerGui:FindFirstChild(name)
	if old then
		old:Destroy()
	end
end

--------------------------------------------------------
-- COLORS
--------------------------------------------------------

local C = {
	BG = Color3.fromRGB(10, 8, 17),
	Header = Color3.fromRGB(24, 16, 37),
	Card = Color3.fromRGB(25, 18, 40),
	Hover = Color3.fromRGB(38, 28, 55),
	Track = Color3.fromRGB(55, 44, 70),

	Orange = Color3.fromRGB(255, 145, 10),
	Orange2 = Color3.fromRGB(255, 190, 65),

	Green = Color3.fromRGB(60, 220, 125),
	Red = Color3.fromRGB(220, 55, 70),

	White = Color3.fromRGB(245, 242, 250),
	Text = Color3.fromRGB(232, 227, 240),
	Muted = Color3.fromRGB(155, 145, 175)
}

--------------------------------------------------------
-- SETTINGS
--------------------------------------------------------

local Settings = {
	WallHop = false,

	Speed = 16,
	Jump = 50,

	WallDistance = 4.5,
	WallPower = 55,
	WallPush = 8,
	MovementPreserve = 0.9,
	WallCooldown = 0.18,

	ESP = false,
	VisualHitbox = false,
	FPSBoost = false
}

--------------------------------------------------------
-- CHARACTER
--------------------------------------------------------

local Character
local Humanoid
local Root

local function setupCharacter(char)
	Character = char
	Humanoid = char:WaitForChild("Humanoid")
	Root = char:WaitForChild("HumanoidRootPart")

	Humanoid.UseJumpPower = true
	Humanoid.WalkSpeed = Settings.Speed
	Humanoid.JumpPower = Settings.Jump
end

if Player.Character then
	setupCharacter(Player.Character)
end

Player.CharacterAdded:Connect(setupCharacter)

--------------------------------------------------------
-- KEY SYSTEM
-- NOTHING ELSE IS CREATED BEFORE AUTHENTICATION
--------------------------------------------------------

local KeyGui = Instance.new("ScreenGui")
KeyGui.Name = "ApexKeySystem"
KeyGui.ResetOnSpawn = false
KeyGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
KeyGui.DisplayOrder = 999
KeyGui.Parent = PlayerGui

local KeyFrame = Instance.new("Frame")
KeyFrame.Size = UDim2.fromOffset(300, 185)
KeyFrame.AnchorPoint = Vector2.new(0.5, 0.5)
KeyFrame.Position = UDim2.fromScale(0.5, 0.5)
KeyFrame.BackgroundColor3 = C.BG
KeyFrame.BorderSizePixel = 0
KeyFrame.Parent = KeyGui

Instance.new("UICorner", KeyFrame).CornerRadius = UDim.new(0, 13)

local KeyStroke = Instance.new("UIStroke")
KeyStroke.Color = Color3.fromRGB(85, 60, 110)
KeyStroke.Transparency = 0.2
KeyStroke.Thickness = 1
KeyStroke.Parent = KeyFrame

local KeyHeader = Instance.new("Frame")
KeyHeader.Size = UDim2.new(1, 0, 0, 45)
KeyHeader.BackgroundColor3 = C.Header
KeyHeader.BorderSizePixel = 0
KeyHeader.Parent = KeyFrame

Instance.new("UICorner", KeyHeader).CornerRadius = UDim.new(0, 13)

local KeyTitle = Instance.new("TextLabel")
KeyTitle.Size = UDim2.new(1, -24, 1, 0)
KeyTitle.Position = UDim2.fromOffset(12, 0)
KeyTitle.BackgroundTransparency = 1
KeyTitle.Text = "APEX • ENTER KEY"
KeyTitle.TextColor3 = C.Orange
KeyTitle.TextSize = 13
KeyTitle.Font = Enum.Font.GothamBold
KeyTitle.TextXAlignment = Enum.TextXAlignment.Left
KeyTitle.Parent = KeyHeader

local KeyBox = Instance.new("TextBox")
KeyBox.Size = UDim2.new(1, -24, 0, 40)
KeyBox.Position = UDim2.fromOffset(12, 60)
KeyBox.BackgroundColor3 = C.Card
KeyBox.BorderSizePixel = 0
KeyBox.PlaceholderText = "Enter key here..."
KeyBox.Text = ""
KeyBox.TextColor3 = C.Text
KeyBox.PlaceholderColor3 = C.Muted
KeyBox.TextSize = 11
KeyBox.Font = Enum.Font.GothamMedium
KeyBox.ClearTextOnFocus = false
KeyBox.TextXAlignment = Enum.TextXAlignment.Left
KeyBox.Parent = KeyFrame

Instance.new("UICorner", KeyBox).CornerRadius = UDim.new(0, 9)

local KeyBoxStroke = Instance.new("UIStroke")
KeyBoxStroke.Color = Color3.fromRGB(70, 50, 90)
KeyBoxStroke.Transparency = 0.35
KeyBoxStroke.Parent = KeyBox

local SubmitBtn = Instance.new("TextButton")
SubmitBtn.Size = UDim2.new(1, -24, 0, 40)
SubmitBtn.Position = UDim2.fromOffset(12, 115)
SubmitBtn.BackgroundColor3 = C.Orange
SubmitBtn.BorderSizePixel = 0
SubmitBtn.Text = "SUBMIT"
SubmitBtn.TextColor3 = C.White
SubmitBtn.TextSize = 11
SubmitBtn.Font = Enum.Font.GothamBold
SubmitBtn.AutoButtonColor = false
SubmitBtn.Parent = KeyFrame

Instance.new("UICorner", SubmitBtn).CornerRadius = UDim.new(0, 9)

local KeyStatus = Instance.new("TextLabel")
KeyStatus.Size = UDim2.new(1, -24, 0, 18)
KeyStatus.Position = UDim2.fromOffset(12, 160)
KeyStatus.BackgroundTransparency = 1
KeyStatus.Text = "Enter your access key"
KeyStatus.TextColor3 = C.Muted
KeyStatus.TextSize = 8
KeyStatus.Font = Enum.Font.Gotham
KeyStatus.TextXAlignment = Enum.TextXAlignment.Center
KeyStatus.Parent = KeyFrame

--------------------------------------------------------
-- KEY VERIFICATION
--------------------------------------------------------

local authenticated = false
local checking = false

local function verifyKey()
	if checking or authenticated then
		return
	end

	checking = true

	local entered = KeyBox.Text
	entered = string.gsub(entered, "^%s+", "")
	entered = string.gsub(entered, "%s+$", "")

	if string.lower(entered) == "apex" then

		authenticated = true

		KeyStatus.Text = "ACCESS GRANTED"
		KeyStatus.TextColor3 = C.Green

		SubmitBtn.Text = "LOADING..."
		SubmitBtn.BackgroundColor3 = C.Green

		task.wait(0.25)

		-- Destroy key screen BEFORE creating the main UI
		KeyGui:Destroy()

		------------------------------------------------
		-- MAIN APEX UI STARTS HERE
		------------------------------------------------

	else

		KeyBox.Text = ""
		KeyStatus.Text = "INCORRECT KEY"
		KeyStatus.TextColor3 = C.Red

		KeyBox.PlaceholderText = "Try again..."

		task.delay(1.2, function()
			if KeyStatus and KeyStatus.Parent then
				KeyStatus.Text = "Enter your access key"
				KeyStatus.TextColor3 = C.Muted
				KeyBox.PlaceholderText = "Enter key here..."
			end
		end)
	end

	checking = false
end

SubmitBtn.MouseButton1Click:Connect(verifyKey)

--------------------------------------------------------
-- KEYBOARD FIX
--------------------------------------------------------

KeyBox.FocusLost:Connect(function(enterPressed)
	if enterPressed then
		verifyKey()
	end
end)

UIS.InputBegan:Connect(function(input, processed)

	if authenticated then
		return
	end

	if processed then
		return
	end

	if input.KeyCode == Enum.KeyCode.Return
		or input.KeyCode == Enum.KeyCode.KeypadEnter then

		if KeyBox:IsFocused() then
			verifyKey()
		end
	end
end)

--------------------------------------------------------
-- KEEP KEY SCREEN ACTIVE
--------------------------------------------------------

KeyBox:CaptureFocus()

--------------------------------------------------------
-- WAIT FOR AUTHENTICATION
--------------------------------------------------------

repeat
	task.wait()
until authenticated

--------------------------------------------------------
-- MAIN GUI
-- CREATED ONLY AFTER CORRECT KEY
--------------------------------------------------------

local Gui = Instance.new("ScreenGui")
Gui.Name = "ApexCommunityV15"
Gui.ResetOnSpawn = false
Gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
Gui.Parent = PlayerGui

--------------------------------------------------------
-- MAIN WINDOW
--------------------------------------------------------

local Main = Instance.new("Frame")
Main.Size = UDim2.fromOffset(280, 410)
Main.AnchorPoint = Vector2.new(0.5, 0.5)
Main.Position = UDim2.fromScale(0.5, 0.5)
Main.BackgroundColor3 = C.BG
Main.BorderSizePixel = 0
Main.Parent = Gui

Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 13)

local Stroke = Instance.new("UIStroke")
Stroke.Color = Color3.fromRGB(85, 60, 110)
Stroke.Transparency = 0.25
Stroke.Parent = Main

--------------------------------------------------------
-- HEADER
--------------------------------------------------------

local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 54)
Header.BackgroundColor3 = C.Header
Header.BorderSizePixel = 0
Header.Parent = Main

Instance.new("UICorner", Header).CornerRadius = UDim.new(0, 13)

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -65, 0, 24)
Title.Position = UDim2.fromOffset(13, 5)
Title.BackgroundTransparency = 1
Title.Text = "APEX COMMUNITY"
Title.TextColor3 = C.Orange
Title.TextSize = 14
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Header

local Subtitle = Instance.new("TextLabel")
Subtitle.Size = UDim2.new(1, -65, 0, 17)
Subtitle.Position = UDim2.fromOffset(13, 29)
Subtitle.BackgroundTransparency = 1
Subtitle.Text = "V15 • Created by Vex"
Subtitle.TextColor3 = C.Muted
Subtitle.TextSize = 8
Subtitle.Font = Enum.Font.Gotham
Subtitle.TextXAlignment = Enum.TextXAlignment.Left
Subtitle.Parent = Header

local Close = Instance.new("TextButton")
Close.Size = UDim2.fromOffset(28, 28)
Close.Position = UDim2.new(1, -37, 0, 13)
Close.BackgroundColor3 = C.Red
Close.BorderSizePixel = 0
Close.Text = "×"
Close.TextColor3 = C.White
Close.TextSize = 17
Close.Font = Enum.Font.GothamBold
Close.Parent = Header

Instance.new("UICorner", Close).CornerRadius = UDim.new(0, 8)

--------------------------------------------------------
-- STATUS
--------------------------------------------------------

local Status = Instance.new("TextLabel")
Status.Size = UDim2.new(1, -24, 0, 20)
Status.Position = UDim2.fromOffset(12, 58)
Status.BackgroundTransparency = 1
Status.Text = "● SYSTEM READY"
Status.TextColor3 = C.Green
Status.TextSize = 9
Status.Font = Enum.Font.GothamBold
Status.TextXAlignment = Enum.TextXAlignment.Left
Status.Parent = Main

local function setStatus(text, color)
	Status.Text = "● " .. text
	Status.TextColor3 = color
end

--------------------------------------------------------
-- SCROLL
--------------------------------------------------------

local Scroll = Instance.new("ScrollingFrame")
Scroll.Size = UDim2.new(1, -10, 1, -88)
Scroll.Position = UDim2.fromOffset(5, 83)
Scroll.BackgroundTransparency = 1
Scroll.BorderSizePixel = 0
Scroll.ScrollBarThickness = 3
Scroll.ScrollBarImageColor3 = C.Orange
Scroll.AutomaticCanvasSize = Enum.AutomaticSize.Y
Scroll.CanvasSize = UDim2.new()
Scroll.Parent = Main

local Layout = Instance.new("UIListLayout")
Layout.Padding = UDim.new(0, 5)
Layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
Layout.Parent = Scroll

--------------------------------------------------------
-- DRAGGING
--------------------------------------------------------

local function draggable(object, handle)

	local dragging = false
	local dragStart
	local startPosition

	handle.InputBegan:Connect(function(input)

		if input.UserInputType == Enum.UserInputType.MouseButton1
			or input.UserInputType == Enum.UserInputType.Touch then

			dragging = true
			dragStart = input.Position
			startPosition = object.Position

			input.Changed:Connect(function()

				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end

			end)
		end
	end)

	UIS.InputChanged:Connect(function(input)

		if not dragging then
			return
		end

		if input.UserInputType == Enum.UserInputType.MouseMovement
			or input.UserInputType == Enum.UserInputType.Touch then

			local delta = input.Position - dragStart

			object.Position = UDim2.new(
				startPosition.X.Scale,
				startPosition.X.Offset + delta.X,

				startPosition.Y.Scale,
				startPosition.Y.Offset + delta.Y
			)
		end
	end)
end

draggable(Main, Header)

--------------------------------------------------------
-- REOPEN BUTTON
--------------------------------------------------------

local Reopen = Instance.new("TextButton")
Reopen.Size = UDim2.fromOffset(52, 52)
Reopen.AnchorPoint = Vector2.new(0, 0.5)
Reopen.Position = UDim2.new(0, 12, 0.5, 0)
Reopen.BackgroundColor3 = C.Orange
Reopen.BorderSizePixel = 0
Reopen.Text = "A"
Reopen.TextColor3 = C.White
Reopen.TextSize = 19
Reopen.Font = Enum.Font.GothamBold
Reopen.Visible = false
Reopen.Parent = Gui

Instance.new("UICorner", Reopen).CornerRadius = UDim.new(1, 0)

local ReopenStroke = Instance.new("UIStroke")
ReopenStroke.Color = C.Orange2
ReopenStroke.Transparency = 0.25
ReopenStroke.Parent = Reopen

draggable(Reopen, Reopen)

Close.MouseButton1Click:Connect(function()
	Main.Visible = false
	Reopen.Visible = true
end)

Reopen.MouseButton1Click:Connect(function()
	Main.Visible = true
	Reopen.Visible = false
end)

--------------------------------------------------------
-- CONTROLLERS
--------------------------------------------------------

local Controllers = {}
local SliderRefreshers = {}

--------------------------------------------------------
-- TOGGLE CREATOR
--------------------------------------------------------

local function createToggle(text, default, callback)

	local Button = Instance.new("TextButton")
	Button.Size = UDim2.new(1, -4, 0, 40)
	Button.BackgroundColor3 = C.Card
	Button.BorderSizePixel = 0
	Button.Text = ""
	Button.AutoButtonColor = false
	Button.Parent = Scroll

	Instance.new("UICorner", Button).CornerRadius = UDim.new(0, 9)

	local Label = Instance.new("TextLabel")
	Label.Size = UDim2.new(1, -70, 1, 0)
	Label.Position = UDim2.fromOffset(12, 0)
	Label.BackgroundTransparency = 1
	Label.Text = text
	Label.TextColor3 = C.Text
	Label.TextSize = 10
	Label.Font = Enum.Font.GothamMedium
	Label.TextXAlignment = Enum.TextXAlignment.Left
	Label.Parent = Button

	local Toggle = Instance.new("Frame")
	Toggle.Size = UDim2.fromOffset(42, 21)
	Toggle.Position = UDim2.new(1, -53, 0.5, -10)
	Toggle.BackgroundColor3 = C.Track
	Toggle.BorderSizePixel = 0
	Toggle.Parent = Button

	Instance.new("UICorner", Toggle).CornerRadius = UDim.new(1, 0)

	local Knob = Instance.new("Frame")
	Knob.Size = UDim2.fromOffset(15, 15)
	Knob.Position = UDim2.fromOffset(3, 3)
	Knob.BackgroundColor3 = C.White
	Knob.BorderSizePixel = 0
	Knob.Parent = Toggle

	Instance.new("UICorner", Knob).CornerRadius = UDim.new(1, 0)

	local enabled = default

	local function update()

		local position
		local color

		if enabled then
			position = UDim2.new(1, -18, 0, 3)
			color = C.Orange
		else
			position = UDim2.fromOffset(3, 3)
			color = C.Track
		end

		TweenService:Create(
			Toggle,
			TweenInfo.new(0.12),
			{BackgroundColor3 = color}
		):Play()

		TweenService:Create(
			Knob,
			TweenInfo.new(0.12),
			{Position = position}
		):Play()

		callback(enabled)
	end

	Button.MouseButton1Click:Connect(function()
		enabled = not enabled
		update()
	end)

	Controllers[text] = function(value)
		enabled = value
		update()
	end

	update()

	return Button
end

--------------------------------------------------------
-- SLIDER CREATOR
--------------------------------------------------------

local function createSlider(
	text,
	min,
	max,
	default,
	enabledFunction,
	callback
)

	local Frame = Instance.new("Frame")
	Frame.Size = UDim2.new(1, -4, 0, 58)
	Frame.BackgroundColor3 = C.Card
	Frame.BorderSizePixel = 0
	Frame.Parent = Scroll

	Instance.new("UICorner", Frame).CornerRadius = UDim.new(0, 9)

	local Label = Instance.new("TextLabel")
	Label.Size = UDim2.new(1, -70, 0, 20)
	Label.Position = UDim2.fromOffset(12, 2)
	Label.BackgroundTransparency = 1
	Label.Text = text
	Label.TextColor3 = C.Text
	Label.TextSize = 10
	Label.Font = Enum.Font.GothamMedium
	Label.TextXAlignment = Enum.TextXAlignment.Left
	Label.Parent = Frame

	local Value = Instance.new("TextLabel")
	Value.Size = UDim2.fromOffset(55, 20)
	Value.Position = UDim2.new(1, -65, 0, 2)
	Value.BackgroundTransparency = 1
	Value.Text = tostring(default)
	Value.TextColor3 = C.Orange2
	Value.TextSize = 9
	Value.Font = Enum.Font.GothamBold
	Value.TextXAlignment = Enum.TextXAlignment.Right
	Value.Parent = Frame

	local Bar = Instance.new("Frame")
	Bar.Size = UDim2.new(1, -24, 0, 6)
	Bar.Position = UDim2.fromOffset(12, 39)
	Bar.BackgroundColor3 = C.Track
	Bar.BorderSizePixel = 0
	Bar.Active = true
	Bar.Parent = Frame

	Instance.new("UICorner", Bar).CornerRadius = UDim.new(1, 0)

	local percentDefault =
		math.clamp((default - min) / (max - min), 0, 1)

	local Fill = Instance.new("Frame")
	Fill.BorderSizePixel = 0
	Fill.BackgroundColor3 = C.Orange
	Fill.Size = UDim2.new(percentDefault, 0, 1, 0)
	Fill.Parent = Bar

	Instance.new("UICorner", Fill).CornerRadius = UDim.new(1, 0)

	local Knob = Instance.new("Frame")
	Knob.Size = UDim2.fromOffset(13, 13)
	Knob.AnchorPoint = Vector2.new(0.5, 0.5)
	Knob.Position = UDim2.new(percentDefault, 0, 0.5, 0)
	Knob.BackgroundColor3 = C.White
	Knob.BorderSizePixel = 0
	Knob.Parent = Bar

	Instance.new("UICorner", Knob).CornerRadius = UDim.new(1, 0)

	local dragging = false

	local function setValue(percent)

		if not enabledFunction() then
			return
		end

		percent = math.clamp(percent, 0, 1)

		local value = min + (max - min) * percent
		value = math.floor(value * 10 + 0.5) / 10

		Fill.Size = UDim2.new(percent, 0, 1, 0)
		Knob.Position = UDim2.new(percent, 0, 0.5, 0)

		Value.Text = tostring(value)

		callback(value)
	end

	local function updateInput(inputPosition)

		local width = Bar.AbsoluteSize.X

		if width <= 0 then
			return
		end

		local percent =
			(inputPosition.X - Bar.AbsolutePosition.X) / width

		setValue(percent)
	end

	Bar.InputBegan:Connect(function(input)

		if input.UserInputType == Enum.UserInputType.MouseButton1
			or input.UserInputType == Enum.UserInputType.Touch then

			if enabledFunction() then
				dragging = true
				updateInput(input.Position)
			end
		end
	end)

	UIS.InputChanged:Connect(function(input)

		if not dragging then
			return
		end

		if input.UserInputType == Enum.UserInputType.MouseMovement
			or input.UserInputType == Enum.UserInputType.Touch then

			updateInput(input.Position)
		end
	end)

	UIS.InputEnded:Connect(function(input)

		if input.UserInputType == Enum.UserInputType.MouseButton1
			or input.UserInputType == Enum.UserInputType.Touch then

			dragging = false
		end
	end)

	local function refresh()

		local active = enabledFunction()

		Frame.BackgroundColor3 =
			active and C.Card or Color3.fromRGB(18, 14, 27)

		Bar.BackgroundColor3 =
			active and C.Track or Color3.fromRGB(35, 30, 42)

		Fill.BackgroundColor3 =
			active and C.Orange or Color3.fromRGB(80, 75, 85)

		Knob.BackgroundColor3 =
			active and C.White or Color3.fromRGB(100, 95, 105)

		Value.TextColor3 =
			active and C.Orange2 or C.Muted
	end

	table.insert(SliderRefreshers, refresh)

	return refresh
end

--------------------------------------------------------
-- SPEED
-- NEW VERSION YOU PROVIDED
--------------------------------------------------------

local targetSpeedForce = 16

createToggle(
	"Speed",
	false,

	function(state)

		if state then
			setStatus("SPEED ENABLED", C.Green)
		else
			targetSpeedForce = 16

			if Humanoid then
				Humanoid.WalkSpeed = 16
			end

			setStatus("SPEED OFF", C.Muted)
		end
	end
)

createSlider(
	"Speed Value",
	16,
	300,
	16,

	function()
		return Controllers["Speed"] ~= nil
	end,

	function(value)
		targetSpeedForce = value
		Settings.Speed = value
	end
)

--------------------------------------------------------
-- JUMP
-- NEW VERSION YOU PROVIDED
--------------------------------------------------------

local targetJump = 50

createToggle(
	"Jump",
	false,

	function(state)

		if state then
			setStatus("JUMP ENABLED", C.Green)
		else
			targetJump = 50

			if Humanoid then
				Humanoid.JumpPower = 50
			end

			setStatus("JUMP OFF", C.Muted)
		end
	end
)

createSlider(
	"Jump Value",
	50,
	300,
	50,

	function()
		return Controllers["Jump"] ~= nil
	end,

	function(value)
		targetJump = value
		Settings.Jump = value
	end
)

--------------------------------------------------------
-- WALL HOP
--------------------------------------------------------

createToggle(
	"Wall Hop",
	false,

	function(state)

		Settings.WallHop = state

		if state then
			setStatus("WALL HOP ENABLED", C.Green)
		else
			setStatus("SYSTEM READY", C.Muted)
		end
	end
)

--------------------------------------------------------
-- WALL SETTINGS
--------------------------------------------------------

createSlider(
	"Wall Distance",
	2,
	8,
	4.5,
	function()
		return true
	end,
	function(value)
		Settings.WallDistance = value
	end
)

createSlider(
	"Wall Power",
	35,
	90,
	55,
	function()
		return true
	end,
	function(value)
		Settings.WallPower = value
	end
)

createSlider(
	"Wall Push",
	0,
	20,
	8,
	function()
		return true
	end,
	function(value)
		Settings.WallPush = value
	end
)

createSlider(
	"Movement Preserve",
	0.4,
	1,
	0.9,
	function()
		return true
	end,
	function(value)
		Settings.MovementPreserve = value
	end
)

createSlider(
	"Wall Cooldown",
	0.08,
	0.4,
	0.18,
	function()
		return true
	end,
	function(value)
		Settings.WallCooldown = value
	end
)

--------------------------------------------------------
-- WALL RAYCAST
--------------------------------------------------------

local RayParams = RaycastParams.new()
RayParams.FilterType = Enum.RaycastFilterType.Exclude
RayParams.IgnoreWater = true

local function updateRayFilter()

	if Character then
		RayParams.FilterDescendantsInstances = {
			Character
		}
	end
end

local function getWall()

	if not Character or not Root or not Humanoid then
		return nil
	end

	updateRayFilter()

	local origin = Root.Position
	local directions = {}

	local moveDirection = Humanoid.MoveDirection

	if moveDirection.Magnitude > 0.05 then
		table.insert(directions, moveDirection.Unit)
	end

	local camera = workspace.CurrentCamera

	if camera then

		local look = camera.CFrame.LookVector

		local flatLook = Vector3.new(
			look.X,
			0,
			look.Z
		)

		if flatLook.Magnitude > 0.05 then
			table.insert(directions, flatLook.Unit)
		end
	end

	local forward = Root.CFrame.LookVector
	local right = Root.CFrame.RightVector

	table.insert(directions, forward)
	table.insert(directions, -forward)
	table.insert(directions, right)
	table.insert(directions, -right)

	local closestWall
	local closestDistance = math.huge

	for _, direction in ipairs(directions) do

		local result = workspace:Raycast(
			origin,
			direction * Settings.WallDistance,
			RayParams
		)

		if result
			and result.Instance
			and result.Instance.CanCollide
			and math.abs(result.Normal.Y) < 0.45 then

			local distance =
				(result.Position - origin).Magnitude

			if distance < closestDistance then
				closestDistance = distance
				closestWall = result
			end
		end
	end

	return closestWall
end

--------------------------------------------------------
-- WALL HOP
--------------------------------------------------------

local LastWallHop = 0

local function performWallHop()

	if not Settings.WallHop then
		return false
	end

	if not Character or not Humanoid or not Root then
		return false
	end

	if Humanoid.Health <= 0 then
		return false
	end

	local now = os.clock()

	if now - LastWallHop < Settings.WallCooldown then
		return false
	end

	local wall = getWall()

	if not wall then
		return false
	end

	local normal = Vector3.new(
		wall.Normal.X,
		0,
		wall.Normal.Z
	)

	if normal.Magnitude < 0.05 then
		return false
	end

	normal = normal.Unit

	local velocity = Root.AssemblyLinearVelocity

	local horizontal = Vector3.new(
		velocity.X,
		0,
		velocity.Z
	)

	local intoWall = horizontal:Dot(normal)

	if intoWall < 0 then
		horizontal =
			horizontal - normal * intoWall
	end

	horizontal *= Settings.MovementPreserve

	horizontal += normal * Settings.WallPush

	if horizontal.Magnitude > 60 then
		horizontal =
			horizontal.Unit * 60
	end

	local newY =
		math.max(Settings.WallPower, velocity.Y)

	Root.AssemblyLinearVelocity = Vector3.new(
		horizontal.X,
		newY,
		horizontal.Z
	)

	LastWallHop = now

	Humanoid:ChangeState(
		Enum.HumanoidStateType.Jumping
	)

	return true
end

--------------------------------------------------------
-- JUMP REQUEST / WALL HOP
--------------------------------------------------------

UIS.JumpRequest:Connect(function()

	if not Settings.WallHop then
		return
	end

	if not Character or not Humanoid or not Root then
		return
	end

	if Humanoid.FloorMaterial == Enum.Material.Air then
		performWallHop()
		return
	end

	task.delay(0.07, function()

		if not Character or not Humanoid or not Root then
			return
		end

		if Humanoid.Health <= 0 then
			return
		end

		if Humanoid.FloorMaterial == Enum.Material.Air then
			performWallHop()
		end
	end)
end)

--------------------------------------------------------
-- ESP
--------------------------------------------------------

local ESPObjects = {}

local function removeESP()

	for _, object in pairs(ESPObjects) do
		if object then
			object:Destroy()
		end
	end

	table.clear(ESPObjects)
end

local function updateESP()

	if not Settings.ESP then
		removeESP()
		return
	end

	for _, other in ipairs(Players:GetPlayers()) do

		if other ~= Player and other.Character then

			if not ESPObjects[other.Character] then

				local highlight = Instance.new("Highlight")

				highlight.Name = "ApexESP"
				highlight.FillColor = C.Orange
				highlight.OutlineColor = C.Orange2
				highlight.FillTransparency = 0.82
				highlight.OutlineTransparency = 0.05
				highlight.DepthMode =
					Enum.HighlightDepthMode.AlwaysOnTop

				highlight.Parent = other.Character

				ESPObjects[other.Character] = highlight
			end
		end
	end
end

createToggle(
	"ESP",
	false,

	function(state)

		Settings.ESP = state

		if not state then
			removeESP()
		end
	end
)

--------------------------------------------------------
-- VISUAL HITBOX
--------------------------------------------------------

local HitboxObjects = {}

local function removeHitboxes()

	for _, object in pairs(HitboxObjects) do
		if object then
			object:Destroy()
		end
	end

	table.clear(HitboxObjects)
end

local function updateHitboxes()

	if not Settings.VisualHitbox then
		removeHitboxes()
		return
	end

	for _, other in ipairs(Players:GetPlayers()) do

		if other ~= Player and other.Character then

			local root =
				other.Character:FindFirstChild("HumanoidRootPart")

			if root and not HitboxObjects[other.Character] then

				local box = Instance.new("SelectionBox")

				box.Name = "ApexVisualHitbox"
				box.Adornee = root
				box.LineThickness = 0.04
				box.Color3 = C.Orange
				box.SurfaceTransparency = 1
				box.Parent = root

				HitboxObjects[other.Character] = box
			end
		end
	end
end

createToggle(
	"Visual Hitbox",
	false,

	function(state)

		Settings.VisualHitbox = state

		if not state then
			removeHitboxes()
		end
	end
)

--------------------------------------------------------
-- FPS BOOST
--------------------------------------------------------

local SavedShadows = Lighting.GlobalShadows
local SavedFog = Lighting.FogEnd
local SavedParticles = {}

local function enableBoost()

	Settings.FPSBoost = true

	SavedShadows = Lighting.GlobalShadows
	SavedFog = Lighting.FogEnd

	Lighting.GlobalShadows = false
	Lighting.FogEnd = 100000

	table.clear(SavedParticles)

	for _, object in ipairs(workspace:GetDescendants()) do

		if object:IsA("ParticleEmitter")
			or object:IsA("Trail")
			or object:IsA("Smoke")
			or object:IsA("Fire") then

			SavedParticles[object] = object.Enabled
			object.Enabled = false
		end
	end

	setStatus("FPS BOOST ENABLED", C.Green)
end

local function disableBoost()

	Settings.FPSBoost = false

	Lighting.GlobalShadows = SavedShadows
	Lighting.FogEnd = SavedFog

	for object, state in pairs(SavedParticles) do

		if object and object.Parent then
			object.Enabled = state
		end
	end

	table.clear(SavedParticles)

	setStatus("SYSTEM READY", C.Green)
end

createToggle(
	"FPS Boost",
	false,

	function(state)

		if state then
			enableBoost()
		else
			disableBoost()
		end
	end
)

--------------------------------------------------------
-- RESET
--------------------------------------------------------

local Reset = Instance.new("TextButton")

Reset.Size = UDim2.new(1, -4, 0, 38)
Reset.BackgroundColor3 = Color3.fromRGB(38, 25, 55)
Reset.BorderSizePixel = 0
Reset.Text = "RESET SETTINGS"
Reset.TextColor3 = C.Text
Reset.TextSize = 9
Reset.Font = Enum.Font.GothamBold
Reset.Parent = Scroll

Instance.new("UICorner", Reset).CornerRadius = UDim.new(0, 9)

Reset.MouseButton1Click:Connect(function()

	Settings.WallHop = false
	Settings.Speed = 16
	Settings.Jump = 50

	Settings.WallDistance = 4.5
	Settings.WallPower = 55
	Settings.WallPush = 8
	Settings.MovementPreserve = 0.9
	Settings.WallCooldown = 0.18

	Settings.ESP = false
	Settings.VisualHitbox = false

	targetSpeedForce = 16
	targetJump = 50

	if Humanoid then
		Humanoid.WalkSpeed = 16
		Humanoid.JumpPower = 50
	end

	if Settings.FPSBoost then
		disableBoost()
	end

	removeESP()
	removeHitboxes()

	for _, name in ipairs({
		"Speed",
		"Jump",
		"Wall Hop",
		"ESP",
		"Visual Hitbox",
		"FPS Boost"
	}) do

		if Controllers[name] then
			Controllers[name](false)
		end
	end

	for _, refresh in ipairs(SliderRefreshers) do
		refresh()
	end

	setStatus("SETTINGS RESET", C.Orange)
end)

--------------------------------------------------------
-- PERFORMANCE DISPLAY
--------------------------------------------------------

local Stats = Instance.new("Frame")

Stats.Size = UDim2.fromOffset(135, 72)
Stats.Position = UDim2.fromOffset(10, 10)
Stats.BackgroundColor3 = C.BG
Stats.BackgroundTransparency = 0.08
Stats.BorderSizePixel = 0
Stats.Visible = false
Stats.Parent = Gui

Instance.new("UICorner", Stats).CornerRadius = UDim.new(0, 9)

local FPS = Instance.new("TextLabel")
FPS.Size = UDim2.new(1, -12, 0, 20)
FPS.Position = UDim2.fromOffset(6, 4)
FPS.BackgroundTransparency = 1
FPS.Text = "FPS: --"
FPS.TextColor3 = C.Green
FPS.TextSize = 9
FPS.Font = Enum.Font.GothamBold
FPS.TextXAlignment = Enum.TextXAlignment.Left
FPS.Parent = Stats

local GPS = Instance.new("TextLabel")
GPS.Size = UDim2.new(1, -12, 0, 20)
GPS.Position = UDim2.fromOffset(6, 25)
GPS.BackgroundTransparency = 1
GPS.Text = "POS: --"
GPS.TextColor3 = C.Text
GPS.TextSize = 8
GPS.Font = Enum.Font.Gotham
GPS.TextXAlignment = Enum.TextXAlignment.Left
GPS.Parent = Stats

local Boost = Instance.new("TextLabel")
Boost.Size = UDim2.new(1, -12, 0, 18)
Boost.Position = UDim2.fromOffset(6, 46)
Boost.BackgroundTransparency = 1
Boost.Text = "BOOST: OFF"
Boost.TextColor3 = C.Muted
Boost.TextSize = 8
Boost.Font = Enum.Font.GothamBold
Boost.TextXAlignment = Enum.TextXAlignment.Left
Boost.Parent = Stats

--------------------------------------------------------
-- FPS LOOP
--------------------------------------------------------

local frames = 0
local lastFPS = os.clock()
local currentFPS = 60

RunService.RenderStepped:Connect(function(deltaTime)

	frames += 1

	local now = os.clock()

	if now - lastFPS >= 0.5 then

		currentFPS =
			math.floor(frames / (now - lastFPS))

		frames = 0
		lastFPS = now
	end

	----------------------------------------------------
	-- NEW SPEED ENGINE
	----------------------------------------------------

	if Humanoid and Root then

		Humanoid.UseJumpPower = true

		if targetJump ~= 50 then
			Humanoid.JumpPower = targetJump
		end

		if targetSpeedForce > 16 then

			Humanoid.WalkSpeed = targetSpeedForce

			if Humanoid.MoveDirection.Magnitude > 0 then

				local targetVelocity =
					Humanoid.MoveDirection * targetSpeedForce

				Root.AssemblyLinearVelocity =
					Vector3.new(
						targetVelocity.X,
						Root.AssemblyLinearVelocity.Y,
						targetVelocity.Z
					)

				local extraCFrameOffset =
					Humanoid.MoveDirection
					* (targetSpeedForce - 16)
					* deltaTime

				Root.CFrame =
					Root.CFrame + extraCFrameOffset
			end
		else
			Humanoid.WalkSpeed = 16
		end
	end

	----------------------------------------------------
	-- PERFORMANCE DISPLAY
	----------------------------------------------------

	if Settings.FPSBoost then

		Stats.Visible = true

		FPS.Text = "FPS: " .. tostring(currentFPS)
		Boost.Text = "BOOST: ON"
		Boost.TextColor3 = C.Green

		if Root then

			local p = Root.Position

			GPS.Text = string.format(
				"POS: %.0f, %.0f, %.0f",
				p.X,
				p.Y,
				p.Z
			)
		end

	else
		Stats.Visible = false
	end

	----------------------------------------------------
	-- ESP
	----------------------------------------------------

	if Settings.ESP then
		updateESP()
	end

	----------------------------------------------------
	-- HITBOX
	----------------------------------------------------

	if Settings.VisualHitbox then
		updateHitboxes()
	end
end)

--------------------------------------------------------
-- PLAYER CLEANUP
--------------------------------------------------------

Players.PlayerRemoving:Connect(function(player)

	local char = player.Character

	if not char then
		return
	end

	if ESPObjects[char] then
		ESPObjects[char]:Destroy()
		ESPObjects[char] = nil
	end

	if HitboxObjects[char] then
		HitboxObjects[char]:Destroy()
		HitboxObjects[char] = nil
	end
end)

--------------------------------------------------------
-- START
--------------------------------------------------------

setStatus("SYSTEM READY", C.Green)

print("[APEX COMMUNITY V15] Loaded")
print("[APEX COMMUNITY] Created by Vex")
