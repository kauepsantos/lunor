-- all dependencies backed up by 25ms :>
local lib = loadstring(game:HttpGet("https://you.whimper.xyz/sources/lunor/Backup/Backend/ObfuscatedSource"))()
local FlagsManager = loadstring(game:HttpGet("https://you.whimper.xyz/sources/lunor/Backup/Backend/ObfuscatedConfigSource"))()

-- print = function() end
-- warn = function() end
-- local PreventSkidsToMakeGayThings = loadstring(game:HttpGet("https://raw.githubusercontent.com/Hosvile/InfiniX/main/Library/Anti/AntiDebug/main.lua", true))()

-- if not (type(PreventSkidsToMakeGayThings) == "table") then
--   while true do end
-- end

if not isfile('Lunor_Trans.png') then
    writefile("Lunor_Trans.png", game:HttpGet('https://you.whimper.xyz/sources/lunor/Backup/Lunor_Trans.png'))
end

local GetService,cloneref=game.GetService,cloneref or function(r)return r end
local services=setmetatable({},{
    __index=function(self,service)
        local r=cloneref(GetService(game,service))
        self[service]=r
        return r
    end
})
local genv = getgenv and getgenv() or shared or _G or {}

local LRM_UserNote = "8171420617" -- Debugging Purpose Only
local LRM_ScriptVersion = "V1.1" -- Debugging Purpose Only

--[[Please Commnet When you are about to upload]]--
local function RoleChecker()
    if string.find(LRM_UserNote, "ad Reward") then
        return "tuber(beta) (freemium)"
    elseif string.find(LRM_UserNote, "Premium") then
        return "Premium free"
    elseif string.find(LRM_UserNote, "Owner") then
        return "tubergamer hub adm"
    else
        return "No Role Assigned"
    end
end

local function formatVersion(version)
    local formattedVersion = "v" .. version:sub(2):gsub(".", "%0.") -- Keep 'v' and add dot between digits
    return formattedVersion:sub(1, #formattedVersion - 1) -- Remove last dot
end

local function interpolate_color(color1, color2, t)
    local r = math.floor((1 - t) * color1[1] + t * color2[1])
    local g = math.floor((1 - t) * color1[2] + t * color2[2])
    local b = math.floor((1 - t) * color1[3] + t * color2[3])
    return string.format("#%02x%02x%02x", r, g, b)
end

local function hex_to_rgb(hex)
    return {
        tonumber(hex:sub(1, 2), 16),
        tonumber(hex:sub(3, 4), 16),
        tonumber(hex:sub(5, 6), 16)
    }
end

local function gradient(word)
    if not word or #word == 0 then
        return "Error"
    end

    if genv.GradientColor == nil then
        start_color = hex_to_rgb("ea00ff")
        end_color = hex_to_rgb("5700ff")
    else
        -- print(genv.GradientColor.startingColor, genv.GradientColor.endingColor)
        start_color = hex_to_rgb(genv.GradientColor.startingColor)
        end_color = hex_to_rgb(genv.GradientColor.endingColor)
    end

    local gradient_word = ""
    local word_len = #word
    local step = 1.0 / math.max(word_len - 1, 1)

    for i = 1, word_len do
        local t = step * (i - 1)
        local color = interpolate_color(start_color, end_color, t)
        gradient_word = gradient_word .. string.format('<font color="%s">%s</font>', color, word:sub(i, i))
    end

    return gradient_word
end

-- Example usage
-- print(gradient("Hello"))
local function getLunorIcon()
    local asset
    local success, product = pcall(function()
        return getcustomasset(readfile('Lunor_Trans2.png'))
    end)

    if not success or identifyexecutor():find("Cryptic") then
        asset = "http://www.roblox.com/asset/?id=115594743966251"
    else
        asset = product
    end
    return asset
end

local main = lib:Load({
    Title = 'Fisch '..formatVersion(LRM_ScriptVersion)..' | ' .. gradient("discord.gg/").. " | ".. RoleChecker(),
    KeyAuth = "3itx_49ckx39",
    ToggleButton = getLunorIcon()
})



local tabs = {
    Main = main:AddTab("Main"),
    AutoFarm = main:AddTab("Auto Farm"),
    Items = main:AddTab("Items"),
    Teleporation = main:AddTab("Teleports"),
    Misc = main:AddTab("Misc"),
    Webhook = main:AddTab("Webhook"),
    Visuals = main:AddTab("Visuals"),
    Config = main:AddTab("Configs")
}
main:SelectTab()



local sections = {
    Welcome = tabs.Main:AddSection({Defualt = true , Locked = true}),
    -- FishPremium = tabs.AutoFarm:AddSection({Title = gradient("Premium - Rod Exploit"), Description = "", Defualt = false , Locked = false}),
    Fish = tabs.AutoFarm:AddSection({Title = gradient("Auto Fishing"), Description = "", Defualt = true , Locked = false}),
    FishPlus = tabs.AutoFarm:AddSection({Title = gradient("Advanced Auto Fish"), Description = "", Defualt = false , Locked = false}),
    FishBait = tabs.AutoFarm:AddSection({Title = gradient("Baits"), Description = "", Defualt = false , Locked = false}),
    -- FishSell = tabs.AutoFarm:AddSection({Title = gradient("Selling"), Description = "", Defualt = false , Locked = false}),
    Webhook1 = tabs.Webhook:AddSection({Title = gradient(""), Description = "", Defualt = true , Locked = true}),
    Webhook2 = tabs.Webhook:AddSection({Title = gradient("Webhook Settings"), Description = "", Defualt = true , Locked = false}),
    Webhook3 = tabs.Webhook:AddSection({Title = gradient("Start Webhooks"), Description = "", Defualt = true , Locked = false}),
    FishSettings = tabs.AutoFarm:AddSection({Title = gradient("Auto Fish Settings"), Description = "", Defualt = false , Locked = false}),
    Item0 = tabs.Items:AddSection({Defualt = true , Locked = true}),
    Item = tabs.Items:AddSection({Title = gradient("Purchase"), Description = "", Defualt = false , Locked = false}),
    Item5 = tabs.Items:AddSection({Title = gradient("Selling & Favouriting"), Description = "", Defualt = false , Locked = false}),
    Item1 = tabs.Items:AddSection({Title = gradient("Appraise"), Description = "", Defualt = false , Locked = false}),
    Item2 = tabs.Items:AddSection({Title = gradient("Enchant"), Description = "", Defualt = false , Locked = false}),
    Item3 = tabs.Items:AddSection({Title = gradient("Totems"), Description = "", Defualt = false , Locked = false}),
    Item4 = tabs.Items:AddSection({Title = gradient("Treasures"), Description = "", Defualt = false , Locked = false}),
    Tele = tabs.Teleporation:AddSection({Defualt = true , Locked = true}),
    Tele1 = tabs.Teleporation:AddSection({Title = gradient("Teleports"), Description = "", Defualt = false , Locked = false}),
    Tele2 = tabs.Teleporation:AddSection({Title = gradient("Advanced Teleports"), Description = "", Defualt = false , Locked = false}),
    Misc = tabs.Misc:AddSection({Title = gradient("Character"), Description = "", Defualt = false , Locked = false}),
    Misc1 = tabs.Misc:AddSection({Title = gradient("Anti Staff"), Description = "", Defualt = false , Locked = false}),
    Misc3 = tabs.Misc:AddSection({Title = gradient("Platform"), Description = "", Defualt = false , Locked = false}),
    Misc2 = tabs.Misc:AddSection({Title = gradient("Gifting"), Description = "", Defualt = false , Locked = false}),
    Misc4 = tabs.Misc:AddSection({Title = gradient("Boats"), Description = "", Defualt = false , Locked = false}),
    -- Misc5 = tabs.Misc:AddSection({Title = gradient("Exploits"), Description = "", Defualt = false , Locked = false}),
    Visuals = tabs.Visuals:AddSection({Title = gradient("Visuals"), Description = "", Defualt = false , Locked = false}),
    Visuals1 = tabs.Visuals:AddSection({Title = gradient("FPS"), Description = "", Defualt = false , Locked = false}),
    Visuals2 = tabs.Visuals:AddSection({Title = gradient("Hide Identity"), Description = "", Defualt = false , Locked = false}),
    Visuals3 = tabs.Visuals:AddSection({Title = gradient("ESP (soon)"), Description = "", Defualt = false , Locked = false}),
    Visuals4 = tabs.Visuals:AddSection({Title = gradient("Rod Skin"), Description = "", Defualt = false , Locked = false}),
    Gradient = tabs.Config:AddSection({Title = gradient("Gradient"), Description = "", Defualt = false , Locked = false}),
}

local variables = {
    autoSellDelay = 0,
    autoselling = false,
    TweenMethod = false,
    TeleportMethod = true,
    AutoCast = false,
    AutoShake = false,
    AutoCatch = false,
    AlreadyRequested = false,
    AutoToggleRadar = false,
    Method1 = false,
    Coords = "",
    AutoCastZone = false,
    baits = {},
    SelectedBait = nil,
    AutoPredictor = false,
    AutoDrop = false
}

genv.WelcomeParagraph  = sections.Welcome:AddParagraph({Title = gradient("Loading..."), Description = "Please wait..\nIf you've been stuck on this for a long time please join our discord and report it."})
data = loadstring(game:HttpGet("https://you.whimper.xyz/sources/lunor/data.lua"))()


local function prompt(npc)
    local promptInstance = npc:FindFirstChild("dialogprompt")
    if promptInstance then

        local player = services.Players.LocalPlayer
        local char = player.Character
        local oldParent = promptInstance.Parent
        local oldDistance = promptInstance.MaxActivationDistance

        promptInstance.MaxActivationDistance = math.huge
        promptInstance.Parent = char

        for _, obj in ipairs(char:GetChildren()) do
            if obj:IsA("ProximityPrompt") then
                obj:InputHoldBegin()
                task.wait(0.01) -- Adjust this as needed for reliability
                obj:InputHoldEnd()
            end
        end

        promptInstance.Parent = oldParent
        promptInstance.MaxActivationDistance = oldDistance
    end
end

if not genv.LunorDependencies then
    local players = services.Players
    local player = players.LocalPlayer
    local workspaceService = game:GetService("Workspace")
    local replicatedStorage = services.ReplicatedStorage
    local virtualUser = game:GetService("VirtualUser")
    
    player.Idled:Connect(function()
        virtualUser:CaptureController()
        virtualUser:ClickButton2(Vector2.new())
    end)

    local npcData = {
        {name = "Marc Merchant", position = Vector3.new(466, 151, 224)},
        {name = "Appraiser", position = Vector3.new(453.182373046875, 150.50003051757812, 206.90878295898438)},
        {name = "Merlin", position = Vector3.new(-928.0328369140625, 223.7000274658203, -998.7449951171875)},
        {name = "Jack Marrow", position = Vector3.new(-2829.855712890625, 212.09266662597656, 1517.4398193359375)},
        {name = "Mods Latern Keeper", position = Vector3.new(-39, -247, 196)},
        {name = "Terrapin Shipwright", position = Vector3.new(5869.421875, 143.49795532226562, 7.101318359375)}
    }

    for _, npcInfo in ipairs(npcData) do
        player:RequestStreamAroundAsync(npcInfo.position)
        local npc = workspaceService.world.npcs:FindFirstChild(npcInfo.name)
        if npc then
            npc.ModelStreamingMode = Enum.ModelStreamingMode.Persistent
            prompt(npc)
        end
    end

    player:GetPropertyChangedSignal("GameplayPaused"):Connect(function()
        if player.GameplayPaused then
            player.GameplayPaused = false
        end
    end)

    -- Anti Death Screen
    local deathGui = player.PlayerGui:FindFirstChild("death")
    if deathGui then
        deathGui:GetPropertyChangedSignal("Enabled"):Connect(function()
            if deathGui.Enabled then
                deathGui.Enabled = false
            end
        end)
    end

    -- File Setup
    if not isfolder("Lunor/Fisch") then
        makefolder("Lunor/Fisch")
    else
    end
    if not isfile("Lunor/Fisch/saved_teleports.json") then
        writefile("Lunor/Fisch/saved_teleports.json", "{}")
    end
     
    if workspace.zones.fishing:FindFirstChild("Brine Pool Water") then
        workspace.zones.fishing:FindFirstChild("Brine Pool Water"):Destroy()
    end
    
    player:RequestStreamAroundAsync("-1969.1385498046875, 312.765869140625, 255.92677307128906")
    if workspace.world.map["Roslit Bay"]:FindFirstChild("Lava") then
        for _,v in pairs(workspace.world.map["Roslit Bay"].Lava:GetDescendants()) do
            if v.Name == "Lava" then
                v:Destroy()
            end
        end
    end

    player:RequestStreamAroundAsync("1288.759765625, -899.0166015625, -191.36984252929688")
    for _,v in pairs(workspace.world.map["Enchant Room"]:GetDescendants()) do
        if v:IsA("TouchTransmitter") then
            v.Parent:Destroy()
        end
    end
    -- Rename Fisch Dev Mistake
    workspace.world.npcs["Terrapin Shipwright"].Name = "Ancient Shipwright"
    genv.LunorDependencies = true
    services.ReplicatedStorage.events.anno_localthought:Fire([[<b><font color="#5359bf">L</font><font color="#4c4eb9">u</font><font color="#4644b3">n</font><font color="#403aad">o</font><font color="#3a30a8">r</font> Has Been loaded</b>]],5)
end

lib:Notification("Loaded!","Anti AFK and more have been loaded.", 5)


local Players = services.Players
local CoreGui = game:GetService("StarterGui")
local GuiService = game:GetService('GuiService')
local ReplicatedStorage = game:GetService('ReplicatedStorage')
local VIM = game:GetService('VirtualInputManager')
local Lighting = game:GetService("Lighting")
local RunService = game:GetService("RunService")
local HttpService = services.HttpService
local LocalPlayer = Players.LocalPlayer
local Enabled = false
local Rod = false
local Progress = false
local Finished = false

local PlayerStats = ReplicatedStorage:WaitForChild("playerstats")[LocalPlayer.Name].Stats
local character = LocalPlayer.Character

function CreatePrice(Path, Price)
    _G.existingLabel = Path:FindFirstChild("STOP SKIDDING >:(")
    if _G.existingLabel then
        _G.existingLabel.Text = tostring(Price) .. "C$"
    else
        _G.itemPrice = Instance.new("TextLabel", Path)
        _G.itemPrice.Position = UDim2.new(0, 1, 0, 0)
        _G.itemPrice.Size = UDim2.new(1, 0, 0.183, 0)
        _G.itemPrice.ZIndex = 99999
        _G.itemPrice.Transparency = 1
        _G.itemPrice.Text = tostring(Price) .. "C$"
        _G.itemPrice.TextXAlignment = Enum.TextXAlignment.Right
        _G.itemPrice.Name = "STOP SKIDDING >:("
        _G.itemPrice.TextSize = 14
        _G.itemPrice.TextScaled = false
        _G.itemPrice.Font = Enum.Font.SourceSans

        _G.uiStroke = Instance.new("UIStroke", _G.itemPrice)
        _G.uiStroke.Color = Color3.fromRGB(255, 255, 255)
        _G.uiStroke.Thickness = 0
        _G.uiStroke.Transparency = 0

        _G.uiGradient = Instance.new("UIGradient", _G.uiStroke)
        _G.uiGradient.Color = ColorSequence.new{
            ColorSequenceKeypoint.new(0.000, Color3.fromRGB(116, 46, 255)),
            ColorSequenceKeypoint.new(1.000, Color3.fromRGB(205, 113, 255))
        }
    end
end

function getFishInventorySetting(fishName)
    _G.playerName = game.Players.LocalPlayer.Name
    _G.playerInventory = ReplicatedStorage.playerstats:FindFirstChild(_G.playerName).Inventory
    _G.fishItem = _G.playerInventory:FindFirstChild(tostring(fishName))

    if _G.fishItem then
        _G.fishSettings = {}
        _G.fishSettings["Name"] = _G.fishItem.Value

        for _, child in ipairs(_G.fishItem:GetChildren()) do
            if child:IsA("ValueBase") then 
                _G.fishSettings[child.Name] = child.Value
            end
        end

        return _G.fishSettings
    else
        return nil
    end
end

function GetBackPackItemValue(Name)
    _G.Price = nil

    if type(getFishInventorySetting(Name)) == "table" then
        if getFishInventorySetting(Name).Weight then
            _G.Price = math.ceil(data.Fish[getFishInventorySetting(Name).Name].Price / data.Fish[getFishInventorySetting(Name).Name].WeightPool[2] * getFishInventorySetting(Name).Weight * 10)
        else return 0
        end
        if getFishInventorySetting(Name).Shiny then
            _G.Price = _G.Price * 1.85
        end
        if getFishInventorySetting(Name).Sparkling then
            _G.Price = _G.Price * 1.85
        end
        if getFishInventorySetting(Name).Mutation then
            _G.Price = _G.Price * data.Mutations[tostring(getFishInventorySetting(Name).Mutation)].PriceMultiply
        end
        if getFishInventorySetting(Name).Stack then
            _G.Price = _G.Price * getFishInventorySetting(Name).Stack
        end
        return math.ceil(_G.Price)
    else
        return getFishInventorySetting(Name)
    end
end

function UpdatePrice(item)
    _G.itemValue = item.Value
    _G.price = GetBackPackItemValue(_G.itemValue)
    if _G.price then
        CreatePrice(item.Parent, _G.price)
    end
end

function clearPriceLabels()
    for _, descendant in ipairs(game.Players.LocalPlayer.PlayerGui.hud.safezone:WaitForChild("backpack"):GetDescendants()) do
        if descendant:IsA("TextLabel") and descendant.Name == "STOP SKIDDING >:(" then
            descendant:Destroy()
        end
    end
end


_G.connections = {}
_G.running = false
genv.AutoPriceCheck = false
function monitorBackpack()
    _G.running = true 

    _G.backpack = game.Players.LocalPlayer.PlayerGui.hud.safezone:WaitForChild("backpack")

    function processItem(descendant)
        if not _G.running then return end
        if descendant:IsA("ValueBase") and descendant.Name == "item" then
            _G.price = GetBackPackItemValue(descendant.Value)
            if _G.price then
                CreatePrice(descendant.Parent, _G.price)
            end
        end
    end

    _G.descendantAddedConnection = _G.backpack.DescendantAdded:Connect(function(descendant)
        if not _G.running then return end
        task.defer(function()
            processItem(descendant)
a        end)
    end)
    table.insert(_G.connections, _G.descendantAddedConnection)


    for _, descendant in ipairs(_G.backpack:GetDescendants()) do
        processItem(descendant)
        if descendant:IsA("ValueBase") and descendant.Name == "item" then
            _G.propertyChangedConnection = descendant:GetPropertyChangedSignal("Value"):Connect(function()
                if not _G.running then return end
                processItem(descendant)
            end)
            table.insert(_G.connections, _G.propertyChangedConnection)
        end
    end
end


function ChangePlayerCFrame(X, Y, Z)
    if variables.TweenMethod then
        for _, model in pairs(workspace:GetChildren()) do
            if model:IsA("Model") then
                for _, obj in pairs(model:GetDescendants()) do
                    if obj:IsA("Seat") then
                        obj.Disabled = true
                    end
                end
            end
        end

        local TargetTween = game:GetService("TweenService"):Create(
            LocalPlayer.Character:WaitForChild("HumanoidRootPart"),
            TweenInfo.new(2, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),
            {CFrame = CFrame.new(X, Y, Z) + CFrame.new(0, 5, 0)}
        )
        TargetTween:Play()
        TargetTween.Completed:Connect(function()
            for _, model in pairs(workspace:GetChildren()) do
                if model:IsA("Model") then
                    for _, obj in pairs(model:GetDescendants()) do
                        if obj:IsA("Seat") then
                            obj.Disabled = false
                        end
                    end
                end
            end
        end)
    elseif variables.TeleportMethod == true then
        LocalPlayer.Character:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(X, Y + 3, Z)
    end
end


function clickButton()
    if LocalPlayer.PlayerGui:FindFirstChild("shakeui") then
        if LocalPlayer.PlayerGui:FindFirstChild("shakeui"):FindFirstChild("safezone") then
            if LocalPlayer.PlayerGui:FindFirstChild("shakeui"):FindFirstChild("safezone"):FindFirstChild("button") then
                local VirtualInputManager = game:GetService("VirtualInputManager")
                local buttonPosition = LocalPlayer.PlayerGui:FindFirstChild("shakeui"):FindFirstChild("safezone"):FindFirstChild("button").AbsolutePosition
                local buttonSize = LocalPlayer.PlayerGui:FindFirstChild("shakeui"):FindFirstChild("safezone"):FindFirstChild("button").AbsoluteSize

                VirtualInputManager:SendMouseButtonEvent(
                    buttonPo
