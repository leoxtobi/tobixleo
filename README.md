loadstring(game:HttpGet("https://raw.githubusercontent.com/s2shubowner/Bypasser/main/bypass"))()
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

local Window = Rayfield:CreateWindow({
   Name = "moa  | VIP",
   Icon = nil, -- No icon
   LoadingTitle = "Loading..",
   LoadingSubtitle = "by vip_leo",
   Theme = { -- Pure Yellow & Black Theme
      TextColor = Color3.fromRGB(255, 255, 0), -- Bright Yellow Text

      Background = Color3.fromRGB(0, 0, 0), -- Pure Black Background
      Topbar = Color3.fromRGB(0, 0, 0), -- Black Topbar
      Shadow = Color3.fromRGB(0, 0, 0), -- Black Shadow

      NotificationBackground = Color3.fromRGB(0, 0, 0), -- Black Notification Background
      NotificationActionsBackground = Color3.fromRGB(255, 255, 0), -- Yellow Notification Actions

      TabBackground = Color3.fromRGB(0, 0, 0), -- Black Tab Background
      TabStroke = Color3.fromRGB(255, 255, 0), -- Yellow Tab Border
      TabBackgroundSelected = Color3.fromRGB(255, 255, 0), -- Yellow Selected Tab
      TabTextColor = Color3.fromRGB(255, 255, 0), -- Yellow Tab Text
      SelectedTabTextColor = Color3.fromRGB(0, 0, 0), -- Black Text on Selected Tab

      ElementBackground = Color3.fromRGB(0, 0, 0), -- Black Element Background
      ElementBackgroundHover = Color3.fromRGB(0, 0, 0), -- Hover stays Black
      SecondaryElementBackground = Color3.fromRGB(0, 0, 0), -- Fully Black Secondary Elements
      ElementStroke = Color3.fromRGB(255, 255, 0), -- Yellow Element Border
      SecondaryElementStroke = Color3.fromRGB(255, 255, 0), -- Yellow Border on Secondary Element

      SliderBackground = Color3.fromRGB(255, 255, 0), -- Yellow Slider Background
      SliderProgress = Color3.fromRGB(255, 255, 0), -- Yellow Slider Progress
      SliderStroke = Color3.fromRGB(255, 255, 0), -- Yellow Slider Stroke

      ToggleBackground = Color3.fromRGB(0, 0, 0), -- Black Toggle Background
      ToggleEnabled = Color3.fromRGB(255, 255, 0), -- Yellow When Enabled
      ToggleDisabled = Color3.fromRGB(0, 0, 0), -- Black When Disabled
      ToggleEnabledStroke = Color3.fromRGB(255, 255, 0), -- Yellow Border When Enabled
      ToggleDisabledStroke = Color3.fromRGB(0, 0, 0), -- Black Border When Disabled
      ToggleEnabledOuterStroke = Color3.fromRGB(255, 255, 0), -- Yellow Outer Stroke When Enabled
      ToggleDisabledOuterStroke = Color3.fromRGB(0, 0, 0), -- Black Outer Stroke When Disabled

      DropdownSelected = Color3.fromRGB(255, 255, 0), -- Yellow Selected Dropdown
      DropdownUnselected = Color3.fromRGB(0, 0, 0), -- Black Unselected Dropdown

      InputBackground = Color3.fromRGB(0, 0, 0), -- Black Input Background
      InputStroke = Color3.fromRGB(255, 255, 0), -- Yellow Input Stroke
      PlaceholderColor = Color3.fromRGB(255, 255, 0) -- Yellow Placeholder Text
   },

   DisableRayfieldPrompts = false,
   DisableBuildWarnings = false,

   ConfigurationSaving = {
      Enabled = False,
      FolderName = "YellowBlackThemeHub",
      FileName = "BigHub"
   },

   Discord = {
      Enabled = true,
      Invite = "https://discord.gg/yREt6GkR8V",
      RememberJoins = true
   },

KeySystem = false, -- Set this to true to use our key system
   KeySettings = {
      Title = "Untitled",
      Subtitle = "Key System",
      Note = "contact vip_leo", -- Use this to tell the user how to get a key
      FileName = "Key", -- It is recommended to use something unique as other scripts using Rayfield may overwrite your key file
      SaveKey = false, -- The user's key will be saved, but if you change the key, they will be unable to use your script
      GrabKeyFromSite = false, -- If this is true, set Key below to the RAW site you would like Rayfield to get the key from
      Key = {"SCP1"},
   }
})

local MainTab = Window:CreateTab("Main", 4483362458) -- Title, Image
local MainSection = MainTab:CreateSection("Card")

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local VirtualInputManager = game:GetService("VirtualInputManager")
local player = Players.LocalPlayer

local dupeAmount = 10
local StatusLabel = MainTab:CreateLabel("Status: Waiting for action...")

-- Notification function with error handling
local function notify(message, time, type)
    local success, err = pcall(function()
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = type or "Info",
            Text = message,
            Duration = time or 5,
        })
    end)

    if not success then
        warn("Notification failed: " .. err)
    end
end

-- Textbox for Duplication Amount
MainTab:CreateInput({
    Name = "Amount",
    PlaceholderText = "Amount",
    RemoveTextAfterFocusLost = false,
    Flag = "DupeAmount",
    Callback = function(value)
        dupeAmount = tonumber(value) or 10
        if dupeAmount <= 0 then
            dupeAmount = 10  -- Fallback value
            StatusLabel.Text = "Invalid amount, defaulting to 10."
        end
    end
})

-- Duplication Function
local function duplicateCardsAndLaptops()
    if dupeAmount <= 0 then
        StatusLabel.Text = "Invalid amount!"
        return
    end

    StatusLabel.Text = "Buying cards & laptops..."

    -- Open Dealer UI
    fireclickdetector(game.Workspace["Streetz War"].Anonymous.ClickDetector)
    wait(0) -- Wait to ensure the UI is open
    player.PlayerGui:WaitForChild("DealerGui")
    local shopGui = player.PlayerGui.DealerGui.ShopFrame
    shopGui.Visible = true
    player.PlayerGui.DealerGui.Frame.Visible = false
    game:GetService("RunService"):Set3dRenderingEnabled(false)

    -- Position player correctly
    repeat wait() until player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    player.Character.HumanoidRootPart.CFrame = CFrame.new(-55, 4.5, 170)

    wait(0.5)

    -- Click buttons for purchasing
    local cardButton = shopGui["Blank Card"]
    local laptopButton = shopGui["laptop"]

    for i = 1, dupeAmount do
        task.wait()
        -- Click the card button
        if cardButton.Visible then
            local cardPos = cardButton.AbsolutePosition
            VirtualInputManager:SendMouseButtonEvent(cardPos.X + 150, cardPos.Y + 60, 0, true, game, 0)
            task.wait(0.1)
            VirtualInputManager:SendMouseButtonEvent(cardPos.X + 150, cardPos.Y + 60, 0, false, game, 0)
        end

        task.wait(0.1)

        -- Click the laptop button
        if laptopButton.Visible then
            local laptopPos = laptopButton.AbsolutePosition
            VirtualInputManager:SendMouseButtonEvent(laptopPos.X + 150, laptopPos.Y + 60, 0, true, game, 0)
            task.wait(0.1)
            VirtualInputManager:SendMouseButtonEvent(laptopPos.X + 150, laptopPos.Y + 60, 0, false, game, 0)
        end
    end

    game:GetService("RunService"):Set3dRenderingEnabled(true)

    -- Close the UI
    local exitButton = shopGui.exit
    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, true, game, 0)
    wait()
    VirtualInputManager:SendMouseButtonEvent(exitButton.AbsolutePosition.X + 300, exitButton.AbsolutePosition.Y + 65, 0, false, game, 0)

    -- Move player to next step
    player.Character.HumanoidRootPart.CFrame = CFrame.new(954, 4.7, -61)
    wait(4)

    -- Process Laptops
    StatusLabel.Text = "Processing laptops..."
    local laptopCount = 0
    for _, v in pairs(player.Backpack:GetChildren()) do
        if v.Name == "Laptop" then
            laptopCount = laptopCount + 1
        end
    end

    for i = 1, laptopCount - 1 do
        spawn(function()
            local args = { true, "NEW123" }
            ReplicatedStorage.Assets.Other.GiverPunchmade:InvokeServer(unpack(args))
        end)
    end

    wait(4)
    player.Backpack.Laptop.Parent = player.Character
    wait(4)

    -- Process Cards
    StatusLabel.Text = "Processing cards..."
    local cardCount = 0
    for _, v in pairs(player.Backpack:GetChildren()) do
        if v.Name == "Loaded Card" then
            cardCount = cardCount + 1
        end
    end

    for i = 1, cardCount do
        spawn(function()
            local args = { false, "NEW123" }
            ReplicatedStorage.Assets.Other.GiverPunchmade:InvokeServer(unpack(args))
        end)
    end

    wait(1)
    StatusLabel.Text = "Duplication Complete!"
    player.Character.Humanoid:UnequipTools()
end


MainTab:CreateButton({
        Name = "Duplication Card & Laptop",
    Callback = function()
        duplicateCardsAndLaptops()
    
        end
})

local MainSection = MainTab:CreateSection("Ssfe Dupe")

local Button = MainTab:CreateButton({
   Name = "Safe Dupe",
   Callback = function()
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(108145, -443, 206)

local safeButton = workspace:WaitForChild("Safe")

-- Function to simulate clicking the safe to open it
local function openSafe()
    if safeButton and safeButton:IsA("Part") then
        -- Check if the safe is a button-like part with a ClickDetector
        local clickDetector = safeButton:FindFirstChildOfClass("ClickDetector")
        if clickDetector then
            -- Simulate a click on the button
            clickDetector.MouseClick:Fire(game.Players.LocalPlayer)
            print("Safe is opened via simulated click!")
        else
            -- If no ClickDetector, use FireServer for RemoteEvents (if that's your case)
            safeButton:FireServer()  -- Adjust this based on your game logic
            print("Safe is opened using FireServer!")
        end
    else
        warn("Safe button not found or invalid part!")
    end
end

-- Create the teleport button
local teleportButton = MainTab:CreateButton({
    Name = "Teleport and Open Safe", 
    Callback = function()
        -- Teleport to the specified location
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = teleportLocation

        -- Wait for a brief moment to ensure the player is at the location
        wait(1)  -- Adjust the wait time if necessary

        -- Simulate pressing the button to open the safe
        openSafe()
    end
})

-- Finalize the window and make sure it's visible
Rayfield:Finalize()

print("Rayfield UI loaded and window finalized.")      

   end,
})

local VisualsTab = Window:CreateTab("Visuals", 4483362458)  -- Fixed typo: 'VisulasTab' to 'VisualsTab'
local VisualsSection = VisualsTab:CreateSection("Player Features")

-- Function to update the character GUI
local function updateCharacterGui(field, text)
    local character = game.Players.LocalPlayer.Character
    if character and character:WaitForChild("Head") then
        local nameGui = character.Head:WaitForChild("NameGui"):WaitForChild("Main")
        if nameGui then
            local guiElement = nameGui:WaitForChild(field)
            if guiElement then
                guiElement.Text = text
            end
        end
    end
end

-- Initialize variables to store player input
local lastplayername = nil
local lastplayerlvl  = nil
local lastplayeremoji = nil

-- Input for Custom Name in Rayfield
VisualsTab:CreateInput({
    Name = "Custom Name",
    PlaceholderText = "Enter Name...",
    RemoveTextAfterFocusLost = false,
    Callback = function(text)
        lastplayername = text
        updateCharacterGui("Name", text)
    end
})

-- Input for Custom Level in Rayfield
VisualsTab:CreateInput({
    Name = "Custom Level",
    PlaceholderText = "Enter Level...",
    RemoveTextAfterFocusLost = false,
    Callback = function(text)
        lastplayerlvl = text
        updateCharacterGui("Level", "LVL " .. text)
    end
})

-- Input for Custom Emoji in Rayfield
VisualsTab:CreateInput({
    Name = "Custom Emoji",
    PlaceholderText = "Enter Emoji...",
    RemoveTextAfterFocusLost = false,
    Callback = function(text)
        lastplayeremoji = text
        updateCharacterGui("Extras", "[" .. text .. "]")
    end
})

-- Button to apply changes in Rayfield
VisualsTab:CreateButton({
    Name = "Apply Changes",
    Callback = function()
        -- Apply name
        if lastplayername then
            updateCharacterGui("Name", lastplayername)
        end
        -- Apply level
        if lastplayerlvl then
            updateCharacterGui("Level", "LVL " .. lastplayerlvl)
        end
        -- Apply emoji
        if lastplayeremoji then
            updateCharacterGui("Extras", "[" .. lastplayeremoji .. "]")
        end

        -- Notify the user
        Rayfield:Notify({
            Title = "Updated",
            Content = "Updated By Streetzwars.com",
            Duration = 5
        })
    end
})



local AimTab = Window:CreateTab("Aim", 4483362458) -- Title, Image
local AimSection = AimTab:CreateSection("Weapon Features")

local Toggle = AimTab:CreateToggle({
    Name = "Tool Stealing",
    CurrentValue = false,
    Flag = "ToolStealing",
    Callback = function(Value)
        _G.ToolStealing = Value
        
        while _G.ToolStealing do
            game:GetService("RunService").RenderStepped:Wait()
            
            local tool = game.Workspace:FindFirstChildOfClass("Tool")
            if tool then
                game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
            end
        end
    end
})

local Toggle = AimTab:CreateToggle({
    Name = "Infinite Ammo",
    CurrentValue = false,
    Flag = "InfiniteAmmo",
    Callback = function(state)
        _G.infiniteAmmo = state

        task.spawn(function()
            while _G.infiniteAmmo do
                local player = game.Players.LocalPlayer
                local tool = player.Character and player.Character:FindFirstChildOfClass("Tool")

                if tool and tool:FindFirstChild("Stuff") then
                    local ammoValues = tool.Stuff.Values
                    ammoValues.CurrentAmmo.MaxValue = 1000000000
                    ammoValues.StoredAmmo.MaxValue = 10000000000
                    ammoValues.CurrentAmmo.Value = 10000000000000000000000
                    ammoValues.StoredAmmo.Value = 10000000000000
                end

                task.wait(0.5) -- Prevents excessive loops
            end
        end)
    end
})

local Toggle = AimTab:CreateToggle({
    Name = "Zero Recoil",
    CurrentValue = false,
    Flag = "ZeroRecoil", 
    Callback = function(state)
        _G.zeroRecoil = state
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()

        local function removeRecoil()
            local tool = character:FindFirstChildOfClass("Tool")

            if tool and tool:FindFirstChild("Recoil") then
                tool.Recoil.Value = 0
            end
            if tool and tool:FindFirstChild("CameraShake") then
                tool.CameraShake.Value = 0
            end
            if tool and tool:FindFirstChild("Rotation") then
                tool.Rotation.Value = 0
            end
        end

        task.spawn(function()
            while _G.zeroRecoil do
                removeRecoil()
                wait(0.1) -- Prevent overloading the loop
            end
        end)
    end
})

local Toggle = AimTab:CreateToggle({
    Name = "Modify Weapon",
    CurrentValue = false,
    Flag = "ChangeToolColor", 
    Callback = function(state)
        _G.changeToolColor = state
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()

        -- Function to change the tool color to yellow
        local function changeToolColorToYellow()
            local tool = character:FindFirstChildOfClass("Tool")  -- Find the first tool

            -- Check if tool exists and has a handle
            if tool and tool:FindFirstChild("Handle") then
                -- Change the tool's handle color to yellow
                tool.Handle.BrickColor = BrickColor.new("Bright yellow")
            end
        end

        -- Toggle the color change on and off
        task.spawn(function()
            while _G.changeToolColor do
                changeToolColorToYellow()
                wait(0.1) -- Prevent overloading the loop
            end
        end)
    end
})

local AimSection = AimTab:CreateSection("Aimbot")

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local localPlayer = Players.LocalPlayer
local mouse = localPlayer:GetMouse()
local camera = workspace.CurrentCamera

_G.aimbotSystemEnabled = false

local aimCircleRadius = 100
local aimbotEnabled = false
local circleColor = Color3.new(1, 1, 0) -- Yellow

local aimCircle = nil

local function createAimCircle()
    if not aimCircle then
        aimCircle = Drawing.new("Circle")
        aimCircle.Visible = false
        aimCircle.Color = circleColor
        aimCircle.Thickness = 2
        aimCircle.Radius = aimCircleRadius
        aimCircle.Filled = false
    end
end

local function destroyAimCircle()
    if aimCircle then
        aimCircle:Remove()
        aimCircle = nil
    end
end

local function isPlayerInAimCircle(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local rootPart = character.HumanoidRootPart
        local screenPos, onScreen = workspace.CurrentCamera:WorldToScreenPoint(rootPart.Position)
        if onScreen then
            local mousePos = Vector2.new(mouse.X, mouse.Y)
            local distFromMouse = (mousePos - Vector2.new(screenPos.X, screenPos.Y)).Magnitude
            return distFromMouse <= aimCircleRadius, distFromMouse
        end
    end
    return false, math.huge
end

local function getClosestPlayer()
    local closestPlayer = nil
    local closestDistance = aimCircleRadius

    for _, player in pairs(Players:GetPlayers()) do
        if player ~= localPlayer then
            local character = player.Character
            if character and character:FindFirstChild("Humanoid") and character.Humanoid.Health > 0 then
                local inCircle, distance = isPlayerInAimCircle(player)
                if inCircle and distance < closestDistance then
                    closestDistance = distance
                    closestPlayer = player
                end
            end
        end
    end

    return closestPlayer
end

local function aimAtTarget(player)
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Head") then
        local head = character.Head
        camera.CFrame = CFrame.new(camera.CFrame.Position, head.Position)
    end
end

UserInputService.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 and _G.aimbotSystemEnabled then
        aimbotEnabled = true
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton2 then
        aimbotEnabled = false
    end
end)

RunService.RenderStepped:Connect(function()
    if not _G.aimbotSystemEnabled then
        destroyAimCircle()
        return
    end

    if not aimCircle then
        createAimCircle()
    end

    aimCircle.Position = Vector2.new(mouse.X, mouse.Y + 40)
    aimCircle.Visible = true

    if aimbotEnabled then
        local closestPlayer = getClosestPlayer()
        if closestPlayer then
            aimAtTarget(closestPlayer)
        end
    end
end)

local Toggle = AimTab:CreateToggle({
    Name = "Aimbot",
    CurrentValue = false,
    Flag = "Aimbot",
    Callback = function(Value)
        _G.aimbotSystemEnabled = Value
        if not _G.aimbotSystemEnabled then
            destroyAimCircle()
        end
    end
})

local Toggle = AimTab:CreateToggle({
   Name = "Aimlock ",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Value)
        local Area = game:GetService("Workspace")
local RunService = game:GetService("RunService")
local UIS = game:GetService("UserInputService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local MyCharacter = LocalPlayer.Character
local MyRoot = MyCharacter:FindFirstChild("HumanoidRootPart")
local MyHumanoid = MyCharacter:FindFirstChild("Humanoid")
local Mouse = LocalPlayer:GetMouse()
local MyView = Area.CurrentCamera


local AutoLockActive = false
local LockDistance = 100 -- Maximum distance to lock onto players
local Epitaph = .045 -- Prediction for moving players (larger value means more prediction)


local function FindNearestPlayer()
    local dist = math.huge
    local Target = nil
    for _, v in pairs(Players:GetPlayers()) do
        if v ~= LocalPlayer and v.Character:FindFirstChild("Humanoid") and v.Character:FindFirstChild("Humanoid").Health > 0 and v.Character:FindFirstChild("HumanoidRootPart") then
            local TheirCharacter = v.Character
            local CharacterRoot, Visible = MyView:WorldToViewportPoint(TheirCharacter.HumanoidRootPart.Position)
            if Visible then
                local RealMag = (Vector2.new(Mouse.X, Mouse.Y) - Vector2.new(CharacterRoot.X, CharacterRoot.Y)).Magnitude
                if RealMag < dist and RealMag < LockDistance then
                    dist = RealMag
                    Target = TheirCharacter
                end
            end
        end
    end
    return Target
end


local function AutoLockCamera()
    if AutoLockActive then
        local Target = FindNearestPlayer()
        if Target then
            local FuturePosition = Target.HumanoidRootPart.CFrame + (Target.HumanoidRootPart.Velocity * Epitaph)
            MyView.CFrame = CFrame.lookAt(MyView.CFrame.Position, FuturePosition.Position) -- Lock camera to the target's future position
        end
    end
end


local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local ToggleButton = Instance.new("TextButton")
ToggleButton.Size = UDim2.new(0, 200, 0, 50)
ToggleButton.Position = UDim2.new(0.5, -100, 0.9, -25)
ToggleButton.Text = "Enable AutoLock"
ToggleButton.Parent = ScreenGui
ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)

ToggleButton.MouseButton1Click:Connect(function()
    AutoLockActive = not AutoLockActive -- Toggle the AutoLock state
    if AutoLockActive then
        ToggleButton.Text = "Disable AutoLock"
        ToggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Change to red when active
    else
        ToggleButton.Text = "Enable AutoLock"
        ToggleButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0) -- Change to green when inactive
    end
end)


RunService.RenderStepped:Connect(function()
    AutoLockCamera()
end)


game.StarterGui:SetCore("SendNotification", {
    Title = "AutoLock Active",
    Text = "Auto AimLock script is now active.",
    Duration = 5,
})  
   end,
})

local camera = workspace.CurrentCamera
local entities = game:GetService("Players")
local localplayer = entities.LocalPlayer 
local runservice = game:GetService("RunService")

local esp_settings = {
    enabled = true,
    skel = true,
    skel_col = Color3.fromRGB(255,255,255)
}

local function draw(player, character)
    local skel_parts = {}
    local part_names = {"head", "torso", "leftarm", "rightarm", "leftleg", "rightleg"}
    
    for _, name in ipairs(part_names) do
        skel_parts[name] = Drawing.new("Line")
        skel_parts[name].Visible = false
        skel_parts[name].Thickness = 1.5
        skel_parts[name].Color = esp_settings.skel_col
    end
    
    local function update()
        local connection
        connection = runservice.RenderStepped:Connect(function()
            if character and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Humanoid") and character:FindFirstChild("Humanoid").Health > 0 then
                local root_2d, on_screen = camera:WorldToViewportPoint(character.HumanoidRootPart.Position)
                if on_screen and character.Humanoid.RigType == Enum.HumanoidRigType.R6 and esp_settings.enabled then
                    local head_2d = camera:WorldToViewportPoint(character.Head.Position)
                    local torso_upper_2d = camera:WorldToViewportPoint(character.Torso.Position + Vector3.new(0,1,0))
                    local torso_lower_2d = camera:WorldToViewportPoint(character.Torso.Position + Vector3.new(0,-1,0))
                    local leftarm_2d = camera:WorldToViewportPoint(character["Left Arm"].Position + Vector3.new(0,-1,0))
                    local rightarm_2d = camera:WorldToViewportPoint(character["Right Arm"].Position + Vector3.new(0,-1,0))
                    local leftleg_2d = camera:WorldToViewportPoint(character["Left Leg"].Position + Vector3.new(0,-1,0))
                    local rightleg_2d = camera:WorldToViewportPoint(character["Right Leg"].Position + Vector3.new(0,-1,0))
                    
                    skel_parts.head.From, skel_parts.head.To = Vector2.new(head_2d.X, head_2d.Y), Vector2.new(torso_upper_2d.X, torso_upper_2d.Y)
                    skel_parts.torso.From, skel_parts.torso.To = Vector2.new(torso_upper_2d.X, torso_upper_2d.Y), Vector2.new(torso_lower_2d.X, torso_lower_2d.Y)
                    skel_parts.leftarm.From, skel_parts.leftarm.To = Vector2.new(torso_upper_2d.X, torso_upper_2d.Y), Vector2.new(leftarm_2d.X, leftarm_2d.Y)
                    skel_parts.rightarm.From, skel_parts.rightarm.To = Vector2.new(torso_upper_2d.X, torso_upper_2d.Y), Vector2.new(rightarm_2d.X, rightarm_2d.Y)
                    skel_parts.leftleg.From, skel_parts.leftleg.To = Vector2.new(torso_lower_2d.X, torso_lower_2d.Y), Vector2.new(leftleg_2d.X, leftleg_2d.Y)
                    skel_parts.rightleg.From, skel_parts.rightleg.To = Vector2.new(torso_lower_2d.X, torso_lower_2d.Y), Vector2.new(rightleg_2d.X, rightleg_2d.Y)
                    
                    for _, part in pairs(skel_parts) do
                        part.Visible = esp_settings.skel
                    end
                else
                    for _, part in pairs(skel_parts) do
                        part.Visible = false
                    end
                end
            else
                connection:Disconnect()
                for _, part in pairs(skel_parts) do
                    part.Visible = false
                end
            end
        end)
    end
    coroutine.wrap(update)()
end

local function playeradded(player)
    if player.Character then
        coroutine.wrap(draw)(player, player.Character)
    end
    player.CharacterAdded:Connect(function(character)
        coroutine.wrap(draw)(player, character)
    end)
end

for _, player in ipairs(entities:GetPlayers()) do
    if player ~= localplayer then
        playeradded(player)
    end
end

entities.PlayerAdded:Connect(playeradded)


local Toggle = AimTab:CreateToggle({
    Name = "Skeleton ESP",
    CurrentValue = true,
    Flag = "ESP_Toggle",
    Callback = function(value)
        end
    })

-- Initialize Tabs and Sections
local TeleportsTab = Window:CreateTab("Teleports", 4483362458) -- Title, Image
local TeleportsSection2 = TeleportsTab:CreateSection("Teleports | Location")
local PlayerTab = Window:CreateTab("Player", 4483362458) -- Title, Image
local PlayerSection = PlayerTab:CreateSection("Player Features")

-- Teleport Locations
local teleportLocations = {
    {Name = "🚗dealership", Position = CFrame.new(842, 5, -7)},
    {Name = "🏩Apartments 2", Position = CFrame.new(739, 4, 199)},
    {Name = "🏨Apartments 1", Position = CFrame.new(4, 4, 52)},
    {Name = "🧹Paki Shop", Position = CFrame.new(-101, 4, 18)},
    {Name = "📦Box Job", Position = CFrame.new(-118, 4, 300)},
    {Name = "🍕Pizza Job", Position = CFrame.new(166, 5, 49)},
    {Name = "🏪Thrift Store", Position = CFrame.new(-42, 4, 36)},
    {Name = "🥊Boxing", Position = CFrame.new(259, 5, -100)},
    {Name = "🏆Casino", Position = CFrame.new(159, 5, 246)},
    {Name = "💎Ice Box", Position = CFrame.new(-11354, 4, 288)},
    {Name = "🤭Suit Shop", Position = CFrame.new(43, 4, -329)},
    {Name = "🏥Hospital", Position = CFrame.new(42, 4, -261)},
    {Name = "🔫Gun Store", Position = CFrame.new(-51807, 4, -11)},
    {Name = "🥷Bank Tools Etc", Position = CFrame.new(-142, 4, 189)},
    {Name = "💳Blanc Card Dealer", Position = CFrame.new(226, 4, -543)},
    {Name = "🍍TNT Locker", Position = CFrame.new(269, 5, 132)},
    {Name = "🩸ATB Locker", Position = CFrame.new(93, 4, -703)},
    {Name = "🩶SG Locker", Position = CFrame.new(188, 4, -395)},
    {Name = "💙KAO Locker", Position = CFrame.new(328, 7, 82)},
    {Name = "💙AF Locker", Position = CFrame.new(162, 5, 518)},
    {Name = "🧡EOS Locker", Position = CFrame.new(374, 22, 409)},
    {Name = "💚AOD Locker", Position = CFrame.new(6, 5, 509)},
    {Name = "❤️LAC Locker", Position = CFrame.new(-166, 4, -773)},
    {Name = "💙P9 Locker", Position = CFrame.new(459, 7, 160)},
    {Name = "💙TPL Locker", Position = CFrame.new(318, 7, 230)},
    {Name = "💛RGD Locker", Position = CFrame.new(599, 7, 223)},
    {Name = "NGF Locker", Position = CFrame.new(571, 20, 174)},
    {Name = "💙DF Locker", Position = CFrame.new(870, 5, 498)},
    {Name = "🎄Wheel Spin", Position = CFrame.new(142, 4, 91)}
}

local locationNames = {}

-- Populate location names
for _, location in pairs(teleportLocations) do
    table.insert(locationNames, location.Name)
end

local selectedLocation = teleportLocations[1] -- Default location

-- Dropdown for selecting teleport location
local Dropdown = TeleportsTab:CreateDropdown({
    Name = "Select Teleport Location",
    Options = locationNames,
    CurrentOption = {locationNames[1]}, -- Default selected option
    MultipleOptions = false,
    Flag = "TeleportLocationDropdown", -- Flag for config saving
    Callback = function(Options)
        -- Update selected location based on dropdown selection
        for _, location in pairs(teleportLocations) do
            if location.Name == Options[1] then
                selectedLocation = location
                break
            end
        end
    end
})

-- Button to teleport to selected location
local TeleportButton = TeleportsTab:CreateButton({
    Name = "Teleport",
    Callback = function()
        if selectedLocation then
            -- Teleport player to selected location
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = selectedLocation.Position
        else
            warn("No location selected!")
        end
    end
})

-- Other UI Elements (Player Tab)
local Toggle = PlayerTab:CreateToggle({
   Name = "Change Username",
   CurrentValue = false,
   Flag = "Toggle1", -- A flag is the identifier for the configuration file
   Callback = function(Value)
        local PlayerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")
        local targetUsernameLabel = nil

        local function findAndChangeUsername()
            for _, v in ipairs(PlayerGui:GetDescendants()) do
                if v:IsA("TextLabel") and v.Text:find(game.Players.LocalPlayer.Name) then
                    targetUsernameLabel = v
                    v.Text = "@Crime🔫"  -- Change the username to the desired text
                    v.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  -- Highlight the label in red
                    v.BorderSizePixel = 2
                    v.BorderColor3 = Color3.fromRGB(255, 255, 255)
                    print("Username label found and changed:", v:GetFullName())
                    break
                end
            end
        end

        findAndChangeUsername()
   end,
})

-- Disable Camera Shake Toggle
local Toggle = PlayerTab:CreateToggle({
    Name = "Disable Camera Shake",
    CurrentValue = false,
    Flag = "DisableCameraShake",
    Callback = function(state)
        local char = game:GetService("Players").LocalPlayer.Character
        if char and char:FindFirstChild("CharacterScripts") then
            char.CharacterScripts.Enabled = not state
        end
    end
})

-- Respawn where Died Toggle
local respawnLocation = nil  -- Initialize the respawn location variable

local Toggle = PlayerTab:CreateToggle({
    Name = "Respawn Where Died",
    CurrentValue = false,
    Flag = "Toggle1", -- A flag to store the toggle state
    Callback = function(Value)
        -- If the toggle is enabled, set up the respawn functionality
        if Value then
            -- Set the respawn point to the location where the player dies
            game.Players.PlayerAdded:Connect(function(player)
                player.CharacterAdded:Connect(function(character)
                    local humanoid = character:WaitForChild("Humanoid")

                    humanoid.Died:Connect(function()
                        respawnLocation = character:WaitForChild("HumanoidRootPart").Position
                        wait(5)  -- Delay before respawning the player (optional)

                        -- Destroy the character and respawn
                        character:Destroy()
                        wait(1)

                        -- Load a new character and position it at the respawn location
                        local newCharacter = player:LoadCharacter()
                        newCharacter:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(respawnLocation)
                    end)
                end)
            end)
        else
            -- Disable respawn functionality when the toggle is turned off
            game.Players.PlayerAdded:Connect(function(player)
                player.CharacterAdded:Connect(function(character)
                    local humanoid = character:WaitForChild("Humanoid")

                    humanoid.Died:Disconnect() -- Disconnect the respawn logic
                end)
            end)
        end
    end
})

-- Walk Speed Slider
local Slider = PlayerTab:CreateSlider({
   Name = "Walkspeed",
   Range = {0, 300},
   Increment = 1,
   Suffix = "Speed",
   CurrentValue = 16,
   Flag = "Slider1",
   Callback = function(Value)
        local character = game.Players.LocalPlayer.Character
        if character and character:FindFirstChild("Humanoid") then
            local humanoid = character.Humanoid
            humanoid.WalkSpeed = Value
        else
            warn("Character or Humanoid not found!")
        end
   end,
})

-- Jump Height Slider
local Slider = PlayerTab:CreateSlider({
   Name = "JumpHeight",
   Range = {0, 300},
   Increment = 1,
   Suffix = "Height",
   CurrentValue = 16,
   Flag = "Slider1", -- A flag is the identifier for the configuration file
   Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value
   end,
})

-- Infinite Jump Toggle
local InfiniteJumpEnabled = false
PlayerTab:CreateToggle({
    Name = "Infinite Jump",
    Default = false,  -- Set to true if you want it enabled by default
    Callback = function(state)
        InfiniteJumpEnabled = state
    end
})

local MiscTab = Window:CreateTab("Misc", 4483362458) -- Title, Image
local MiscSection = MiscTab:CreateSection("Socials")

local Button = MiscTab:CreateButton({
   Name = "Copy Discord Link",
   Callback = function()
        local textToCopy = "Discord.gg/dkshub" 

button.MouseButton1Click:Connect(function()
    if setclipboard then
        setclipboard(textToCopy)
        print("Text copied to clipboard!")
    else
        warn("Your executor does not support setclipboard.")
    end
end)
   end,
})

Rayfield.KeySystem.OnKeyAccepted = function(enteredKey)
    keyUsed = enteredKey
end

MiscTab:CreateButton({
    Name = "Copy Script Key",
    Callback = function()
        if keyUsed ~= "" then
            if setclipboard then
                setclipboard(keyUsed)
            end
        else
            warn("No key has been entered yet!")
        end
    end
})

local Label = MiscTab:CreateLabel("HWID: Loading...", 4483362458, Color3.fromRGB(255, 255, 255), false)

local function getHWID()

    return game.Players.LocalPlayer.UserId
end

local hwid = getHWID()
Label:SetText("HWID: " .. tostring(hwid))

local MiscSection = MiscTab:CreateSection("Ui Settings")

local themes = {
    {Name = "Default", Color = Color3.fromRGB(255, 255, 255)},
    {Name = "Red", Color = Color3.fromRGB(255, 0, 0)},
    {Name = "Green", Color = Color3.fromRGB(0, 255, 0)},
    {Name = "Blue", Color = Color3.fromRGB(0, 0, 255)},
    {Name = "Purple", Color = Color3.fromRGB(128, 0, 128)},
}

local Dropdown = MiscTab:CreateDropdown({
    Name = "Select Ui Theme",
    List = {"Default", "Red", "Green", "Blue", "Purple"},
    Callback = function(selectedTheme)
        
        for _, theme in ipairs(themes) do
            if theme.Name == selectedTheme then
               
                Rayfield:SetTheme(theme.Color)
                break
            end
        end
    end
})

local ChangeNameButton = MiscTab:CreateButton({
    Name = "Discord.gg/dkshub Ui",
    Callback = function()

        Rayfield:SetWindowTitle("discord.gg/dkshub")
    end
})

local MiscSection = MiscTab:CreateSection("Other Weapon Features")

local stickyAimEnabled = false

local StickyAimToggle = MiscTab:CreateToggle({
    Name = "Silent Aim",
    CurrentValue = false,
    Callback = function(value)
        stickyAimEnabled = value
    end
})


local function getClosestEnemy()
    local closestEnemy = nil
    local shortestDistance = math.huge

    
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            local character = player.Character
            if character and character:FindFirstChild("HumanoidRootPart") then
                local distance = (game.Players.LocalPlayer.Character.HumanoidRootPart.Position - character.HumanoidRootPart.Position).Magnitude
                if distance < shortestDistance then
                    shortestDistance = distance
                    closestEnemy = character
                end
            end
        end
    end
    return closestEnemy
end


local function stickyAim()
    if stickyAimEnabled then
        local closestEnemy = getClosestEnemy()
        if closestEnemy then
            local enemyPosition = closestEnemy.HumanoidRootPart.Position
            
            workspace.CurrentCamera.CFrame = CFrame.lookAt(workspace.CurrentCamera.CFrame.Position, enemyPosition)
        end
    end
end


game:GetService("RunService").Heartbeat:Connect(function()
    stickyAim()
end)

local Dropdown = MiscTab:CreateDropdown({
   Name = "Aim Part",
   Options = {"Head","Body" , "Legs"},
   CurrentOption = {"Select"},
   MultipleOptions = false,
   Flag = "Dropdown1", -- A flag is the identifier for the configuration file, make sure every element has a different flag if you're using configuration saving to ensure no overlaps
   Callback = function(Options)

   end
})

local skeletonESPEnabled = false

local ESPToggle = MiscTab:CreateToggle({
    Name = "Skeleton ESP",
    CurrentValue = false,
    Callback = function(value)
        skeletonESPEnabled = value
        if skeletonESPEnabled then
            for _, player in pairs(game:GetService("Players"):GetPlayers()) do
                if player.Name ~= game.Players.LocalPlayer.Name then
                    DrawESP(player)
                end
            end
        end
    end
})

local Player = game:GetService("Players").LocalPlayer
local Mouse = Player:GetMouse()
local Camera = game:GetService("Workspace").CurrentCamera

local function DrawLine()
    local l = Drawing.new("Line")
    l.Visible = false
    l.From = Vector2.new(0, 0)
    l.To = Vector2.new(1, 1)
    l.Color = Color3.fromRGB(255, 255, 0)
    l.Thickness = 1
    l.Transparency = 1
    return l
end

local function DrawESP(plr)
    repeat wait() until plr.Character ~= nil and plr.Character:FindFirstChild("Humanoid") ~= nil
    local limbs = {}
    local R15 = (plr.Character.Humanoid.RigType == Enum.HumanoidRigType.R15) and true or false
    if R15 then 
        limbs = {
            -- Spine
            Head_UpperTorso = DrawLine(),
            UpperTorso_LowerTorso = DrawLine(),
            -- Left Arm
            UpperTorso_LeftUpperArm = DrawLine(),
            LeftUpperArm_LeftLowerArm = DrawLine(),
            LeftLowerArm_LeftHand = DrawLine(),
            -- Right Arm
            UpperTorso_RightUpperArm = DrawLine(),
            RightUpperArm_RightLowerArm = DrawLine(),
            RightLowerArm_RightHand = DrawLine(),
            -- Left Leg
            LowerTorso_LeftUpperLeg = DrawLine(),
            LeftUpperLeg_LeftLowerLeg = DrawLine(),
            LeftLowerLeg_LeftFoot = DrawLine(),
            -- Right Leg
            LowerTorso_RightUpperLeg = DrawLine(),
            RightUpperLeg_RightLowerLeg = DrawLine(),
            RightLowerLeg_RightFoot = DrawLine(),
        }
    else 
        limbs = {
            Head_Spine = DrawLine(),
            Spine = DrawLine(),
            LeftArm = DrawLine(),
            LeftArm_UpperTorso = DrawLine(),
            RightArm = DrawLine(),
            RightArm_UpperTorso = DrawLine(),
            LeftLeg = DrawLine(),
            LeftLeg_LowerTorso = DrawLine(),
            RightLeg = DrawLine(),
            RightLeg_LowerTorso = DrawLine()
        }
    end
    local function Visibility(state)
        for i, v in pairs(limbs) do
            v.Visible = state
        end
    end

    local function Colorize(color)
        for i, v in pairs(limbs) do
            v.Color = color
        end
    end

    local function UpdaterR15()
        local connection
        connection = game:GetService("RunService").RenderStepped:Connect(function()
            if plr.Character ~= nil and plr.Character:FindFirstChild("Humanoid") ~= nil and plr.Character:FindFirstChild("HumanoidRootPart") ~= nil and plr.Character.Humanoid.Health > 0 then
                local HUM, vis = Camera:WorldToViewportPoint(plr.Character.HumanoidRootPart.Position)
                if vis then
                    -- Head
                    local H = Camera:WorldToViewportPoint(plr.Character.Head.Position)
                    if limbs.Head_UpperTorso.From ~= Vector2.new(H.X, H.Y) then
                        --Spine
                        local UT = Camera:WorldToViewportPoint(plr.Character.UpperTorso.Position)
                        local LT = Camera:WorldToViewportPoint(plr.Character.LowerTorso.Position)
                        -- Left Arm
                        local LUA = Camera:WorldToViewportPoint(plr.Character.LeftUpperArm.Position)
                        local LLA = Camera:WorldToViewportPoint(plr.Character.LeftLowerArm.Position)
                        local LH = Camera:WorldToViewportPoint(plr.Character.LeftHand.Position)
                        -- Right Arm
                        local RUA = Camera:WorldToViewportPoint(plr.Character.RightUpperArm.Position)
                        local RLA = Camera:WorldToViewportPoint(plr.Character.RightLowerArm.Position)
                        local RH = Camera:WorldToViewportPoint(plr.Character.RightHand.Position)
                        -- Left leg
                        local LUL = Camera:WorldToViewportPoint(plr.Character.LeftUpperLeg.Position)
                        local LLL = Camera:WorldToViewportPoint(plr.Character.LeftLowerLeg.Position)
                        local LF = Camera:WorldToViewportPoint(plr.Character.LeftFoot.Position)
                        -- Right leg
                        local RUL = Camera:WorldToViewportPoint(plr.Character.RightUpperLeg.Position)
                        local RLL = Camera:WorldToViewportPoint(plr.Character.RightLowerLeg.Position)
                        local RF = Camera:WorldToViewportPoint(plr.Character.RightFoot.Position)

                        --Head
                        limbs.Head_UpperTorso.From = Vector2.new(H.X, H.Y)
                        limbs.Head_UpperTorso.To = Vector2.new(UT.X, UT.Y)

                        --Spine
                        limbs.UpperTorso_LowerTorso.From = Vector2.new(UT.X, UT.Y)
                        limbs.UpperTorso_LowerTorso.To = Vector2.new(LT.X, LT.Y)

                        -- Left Arm
                        limbs.UpperTorso_LeftUpperArm.From = Vector2.new(UT.X, UT.Y)
                        limbs.UpperTorso_LeftUpperArm.To = Vector2.new(LUA.X, LUA.Y)

                        limbs.LeftUpperArm_LeftLowerArm.From = Vector2.new(LUA.X, LUA.Y)
                        limbs.LeftUpperArm_LeftLowerArm.To = Vector2.new(LLA.X, LLA.Y)

                        limbs.LeftLowerArm_LeftHand.From = Vector2.new(LLA.X, LLA.Y)
                        limbs.LeftLowerArm_LeftHand.To = Vector2.new(LH.X, LH.Y)

                        -- Right Arm
                        limbs.UpperTorso_RightUpperArm.From = Vector2.new(UT.X, UT.Y)
                        limbs.UpperTorso_RightUpperArm.To = Vector2.new(RUA.X, RUA.Y)

                        limbs.RightUpperArm_RightLowerArm.From = Vector2.new(RUA.X, RUA.Y)
                        limbs.RightUpperArm_RightLowerArm.To = Vector2.new(RLA.X, RLA.Y)

                        limbs.RightLowerArm_RightHand.From = Vector2.new(RLA.X, RLA.Y)
                        limbs.RightLowerArm_RightHand.To = Vector2.new(RH.X, RH.Y)

                        -- Left Leg
                        limbs.LowerTorso_LeftUpperLeg.From = Vector2.new(LT.X, LT.Y)
                        limbs.LowerTorso_LeftUpperLeg.To = Vector2.new(LUL.X, LUL.Y)

                        limbs.LeftUpperLeg_LeftLowerLeg.From = Vector2.new(LUL.X, LUL.Y)
                        limbs.LeftUpperLeg_LeftLowerLeg.To = Vector2.new(LLL.X, LLL.Y)

                        limbs.LeftLowerLeg_LeftFoot.From = Vector2.new(LLL.X, LLL.Y)
                        limbs.LeftLowerLeg_LeftFoot.To = Vector2.new(LF.X, LF.Y)

                        -- Right Leg
                        limbs.LowerTorso_RightUpperLeg.From = Vector2.new(LT.X, LT.Y)
                        limbs.LowerTorso_RightUpperLeg.To = Vector2.new(RUL.X, RUL.Y)

                        limbs.RightUpperLeg_RightLowerLeg.From = Vector2.new(RUL.X, RUL.Y)
                        limbs.RightUpperLeg_RightLowerLeg.To = Vector2.new(RLL.X, RLL.Y)

                        limbs.RightLowerLeg_RightFoot.From = Vector2.new(RLL.X, RLL.Y)
                        limbs.RightLowerLeg_RightFoot.To = Vector2.new(RF.X, RF.Y)
                    end

                    if limbs.Head_UpperTorso.Visible ~= true then
                        Visibility(true)
                    end
                else 
                    if limbs.Head_UpperTorso.Visible ~= false then
                        Visibility(false)
                    end
                end
            else 
                if limbs.Head_UpperTorso.Visible ~= false then
                    Visibility(false)
                end
                if game.Players:FindFirstChild(plr.Name) == nil then 
                    for i, v in pairs(limbs) do
                        v:Remove()
                    end
                    connection:Disconnect()
                end
            end
        end)
    end

    if R15 then
        coroutine.wrap(UpdaterR15)()
    else 
        coroutine.wrap(UpdaterR6)()
    end
end

for i, v in pairs(game:GetService("Players"):GetPlayers()) do
    if v.Name ~= Player.Name then
        DrawESP(v)
    end
end

game.Players.PlayerAdded:Connect(function(newplr)
    if newplr.Name ~= Player.Name then
        DrawESP(newplr)
    end
end)

local Rayfield = require(game.ReplicatedStorage:WaitForChild("Rayfield")) -- Assuming you have Rayfield UI setup correctly.
local Player = game:GetService("Players").LocalPlayer
local Camera = game:GetService("Workspace").CurrentCamera
local PlayerService = game:GetService("Players")

local Toggle = MiscTab:CreateToggle({
    Name = "Name Esp",
    CurrentValue = false,
    Flag = "showPlayerNames",
    Callback = function(value)
        ShowPlayerNames(value)
    end
})

local function CreateNameTag(player)
   
    local nameTag = Instance.new("BillboardGui")
    nameTag.Adornee = player.Character:WaitForChild("Head")
    nameTag.Size = UDim2.new(0, 200, 0, 50)
    nameTag.StudsOffset = Vector3.new(0, 2, 0)
    nameTag.AlwaysOnTop = true
    nameTag.Parent = player.Character:WaitForChild("Head")
    
    local nameLabel = Instance.new("TextLabel")
    nameLabel.Text = player.Name
    nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    nameLabel.TextStrokeTransparency = 0.8
    nameLabel.BackgroundTransparency = 1
    nameLabel.Size = UDim2.new(1, 0, 1, 0)
    nameLabel.Parent = nameTag

    return nameTag
end

local function ShowPlayerNames(state)
    for _, player in pairs(PlayerService:GetPlayers()) do
        if player.Character and player.Character:FindFirstChild("Head") then
            local nameTag = player.Character:FindFirstChild("Head"):FindFirstChild("BillboardGui")
            if state then
                if not nameTag then
                    CreateNameTag(player)
                end
            else
                if nameTag then
                    nameTag:Destroy()
                end
            end
        end
    end
end


ShowPlayerNames(ToggleButton:Get())


PlayerService.PlayerAdded:Connect(function(player)
    if player.Character and player.Character:FindFirstChild("Head") then
        ShowPlayerNames(ToggleButton:Get())  -- Toggle based on the current UI button state
    end
end)


PlayerService.PlayerRemoving:Connect(function(player)
    if player.Character and player.Character:FindFirstChild("Head") then
        local nameTag = player.Character:FindFirstChild("Head"):FindFirstChild("BillboardGui")
        if nameTag then
            nameTag:Destroy()
        end
    end
end)

local SettingsTab = Window:CreateTab("Settings", 4483362458) -- Title, Image
local SettingsSection = SettingsTab:CreateSection("Information")

local Label = SettingsTab:CreateLabel("Key: Lifetime", 4483362458, Color3.fromRGB(255, 255, 255), false) -- Title, Icon, Color, IgnoreTheme

local Label = SettingsTab:CreateLabel(
    "Username: " .. game.Players.LocalPlayer.Name, -- Title (Text showing player's username)
    nil, -- No icon (nil means no icon is used)
    Color3.fromRGB(255, 255, 255), -- Text Color
    false -- Ignore Theme (set to false if you want it to follow the theme)
)

local Label = SettingsTab:CreateLabel("Credits: abdd", 4483362458, Color3.fromRGB(255, 255, 255), false) -- Title, Icon, Color, IgnoreTheme

local SettingsSection = SettingsTab:CreateSection("Player Features")

local Rayfield = require(game:GetService("ReplicatedStorage").Rayfield) 
local Players = game:GetService("Players")

local playerteleport = nil
local playerList = {}


local function updatePlayerList()
    playerList = {}
    for _, player in ipairs(Players:GetPlayers()) do
        table.insert(playerList, player.Name)
    end
    PlayerDropdown:UpdateOptions(playerList)
end


local PlayerDropdown = SettingsTab:CreateDropdown({
    Name = "Select Player",
    Options = playerList,
    Callback = function(selected)
        playerteleport = selected
    end
})


Players.PlayerAdded:Connect(function()
    updatePlayerList()
end)


Players.PlayerRemoving:Connect(function()
    updatePlayerList()
end)


local Button = SettingsTab:CreateButton({
    Name = "Teleport to Player",
    Callback = function()
        if playerteleport then
            local player = Players:FindFirstChild(playerteleport)
            if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
            else
                Rayfield:Notify({
                    Title = "Error",
                    Content = "Player not found or not loaded.",
                    Duration = 4,
                    Type = "Error"
                })
            end
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "No player selected to teleport.",
                Duration = 4,
                Type = "Error"
            })
        end
    end
})


updatePlayerList()

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local PayAmount = 0 -- Default amount

-- Create TextBox for amount input
local AmountInput = SettingsTab:CreateInput({
    Name = "Pay Cash",
    PlaceholderText = "Enter amount...",
    RemoveTextAfterFocusLost = false,
    Callback = function(value)
        PayAmount = tonumber(value) or 0 -- Convert input to a number
        if PayAmount <= 0 then
            Rayfield:Notify({
                Title = "Error",
                Content = "Please enter a valid amount!",
                Duration = 3,
                Type = "Error"
            })
        end
    end
})

-- Create Button to send /pay command
local PayButton = SettingsTab:CreateButton({
    Name = "/pay Command",
    Callback = function()
        if PayAmount > 0 then
            -- Simulate typing "/pay {amount}"
            local message = "/pay " .. PayAmount
            local ChatBox = LocalPlayer:FindFirstChild("PlayerGui"):FindFirstChild("Chat"):FindFirstChild("Frame"):FindFirstChild("ChatBarParentFrame"):FindFirstChild("Frame"):FindFirstChild("BoxFrame"):FindFirstChild("Frame"):FindFirstChild("ChatBar")

            if ChatBox then
                ChatBox.Text = message
                game:GetService("VirtualInputManager"):SendKeyEvent(true, Enum.KeyCode.Return, false, game) -- Simulate Enter key
            else
                Rayfield:Notify({
                    Title = "Error",
                    Content = "ChatBox not found! Make sure the chat is enabled.",
                    Duration = 4,
                    Type = "Error"
                })
            end
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "Enter a valid amount before sending!",
                Duration = 3,
                Type = "Error"
            })
        end
    end
})

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local DropButton = SettingsTab:CreateButton({
    Name = "/drop",
    Callback = function()
        local ChatBox = LocalPlayer:FindFirstChild("PlayerGui")
            :FindFirstChild("Chat")
            :FindFirstChild("Frame")
            :FindFirstChild("ChatBarParentFrame")
            :FindFirstChild("Frame")
            :FindFirstChild("BoxFrame")
            :FindFirstChild("Frame")
            :FindFirstChild("ChatBar")

        if ChatBox then
            ChatBox.Text = "/drop" -- Auto types /drop
            game:GetService("VirtualInputManager"):SendKeyEvent(true, Enum.KeyCode.Return, false, game) -- Simulates Enter key
        else
            Rayfield:Notify({
                Title = "Error",
                Content = "ChatBox not found! Make sure the chat is enabled.",
                Duration = 4,
                Type = "Error"
            })
        end
    end
})
