local Library = loadstring(game:HttpGet("https://pastebin.com/raw/KNBp0LRy"), "Coastified UI")()
local Window = Library:NewWindow("Last Pirate")
repeat wait() until game:IsLoaded()
game:GetService("Players").LocalPlayer.Idled:connect(function()
game:GetService("VirtualUser"):ClickButton2(Vector2.new())
end)

local Section = Window:NewSection("AutoFarm")

local PlayerTP1
local TweenService = game:GetService("TweenService")

local Dropdown = Section:CreateDropdown("Select Mobs!", {"Bandit [Lv:5]", "Pirates [Lv:15]", "BagyPirates [Lv:30]", "Clown Pirate [Lv:60]", "BlackCoat Pirate [Lv:100]", "Revolutionary Troop [Lv:150]", "Marines [Lv:200]"}, 0, function(t)
    PlayerTP1 = t
end)

local Toggle = Section:CreateToggle("Auto [Hit]", function(Value)
_G.Hit = Value
while _G.Hit do
wait(1)  -- Wait for 1 second before checking for enemies
pcall(function()
for i,v in pairs(workspace.Lives:GetDescendants()) do
if v.Name == PlayerTP1 then
if v.Humanoid.Health > 0 then
repeat
    local toolName = "Combat" -- Replace "YourToolNameHere" with the name of your tool
    
    local LocalPlayer = game:GetService("Players").LocalPlayer
for i, v in pairs(LocalPlayer.Backpack:GetChildren()) do
    if v:IsA('Tool') and v.Name == toolName then
        v.Parent = LocalPlayer.Character
        break -- Stop the loop after picking up the tool
    end
end
LocalPlayer.Character:FindFirstChild(toolName):Activate()
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,0,5)
wait()  -- Wait a short time before checking again
until not _G.Hit or v.Humanoid.Health <= 0
end
end
end
end)
local Player = game.Players.LocalPlayer
local function onCharacterAdded(character)
    character.Archivable = false
    character:WaitForChild("HumanoidRootPart").Anchored = false
    if Player.Character then
            onCharacterAdded(Player.Character)
    end
end
    
Player.CharacterAdded:Connect(onCharacterAdded)
end
end)
local Section = Window:NewSection("Stats")
Section:CreateLabel("Check -Stats-")
local Dropdown = Section:CreateDropdown("Select Stat!", {"1", "2", "3", "4"}, 0, function(s)
    PlayerTP2 = s
end)

local Toggle = Section:CreateToggle("Auto Up|Stat", function(Value)
_G.stats = Value
while _G.stats do wait()
    local args = {
        [1] = 1,
        [2] = PlayerTP2
    }
    
    game:GetService("ReplicatedStorage"):WaitForChild("okStats"):FireServer(unpack(args))    
    end
end)
