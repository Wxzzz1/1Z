
spawn(function()
	while wait() do wait()
		if _G.AutoFarm or _G.AutoFarmTwilight or _G.AutoFarmSwordMonBlade or _G.AutoFarmAllMonsterSelect or _G.AutoFarmMonNearestSelect or _G.AutoFarmBoss or _G.AutoRaid or _G.AutoHydraSeaKing or _G.AutoKingSamurai or _G.GhostShip then
			pcall(function()
				if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
					local Noclip = Instance.new("BodyVelocity")
					Noclip.Name = "BodyClip"
					Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
					Noclip.MaxForce = Vector3.new(100000, 100000, 100000)
					Noclip.Velocity = Vector3.new(0, 0, 0)
				end
				for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
					if v:IsA("BasePart") then
						v.CanCollide = false
					end
				end
			end)
		else
			if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
				game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
			end
		end
	end
end)
spawn(function()
    pcall(function()
        game:GetService("RunService").Stepped:Connect(function()
            if _G.AutoFarm or _G.AutoFarmTwilight or _G.AutoFarmSwordMonBlade or _G.AutoFarmAllMonsterSelect or _G.AutoFarmMonNearestSelect or _G.AutoFarmBoss or _G.AutoRaid or _G.AutoHydraSeaKing or _G.AutoKingSamurai or _G.GhostShip then
                for _, v in pairs(game:GetService("Players").LocalPlayer.Character:GetDescendants()) do
                    if v:IsA("BasePart") then
                        v.CanCollide = false
                    end
                end
            end
        end)
    end)
end)
spawn(function()
    while task.wait() do
        pcall(function()
            if _G.AutoFarm or _G.AutoFarmTwilight or _G.AutoFarmSwordMonBlade or _G.AutoFarmAllMonsterSelect or _G.AutoFarmMonNearestSelect or _G.AutoFarmBoss or _G.AutoRaid or _G.AutoHydraSeaKing or _G.AutoKingSamurai or _G.GhostShip then
                if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
                    local Noclip = Instance.new("BodyVelocity")
                    Noclip.Name = "BodyClip"
                    Noclip.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
                    Noclip.MaxForce = Vector3.new(100000,100000,100000)
                    Noclip.Velocity = Vector3.new(0,0,0)
                end
            else
                game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
            end
        end)
    end
end)
function Tween(Pos)--game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame
    local Distance = (Pos.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if game.Players.LocalPlayer.Character.Humanoid.Sit then
        game.Players.LocalPlayer.Character.Humanoid.Sit = false
    end
    pcall(function()
        local tween = game:GetService("TweenService"):Create(
            game.Players.LocalPlayer.Character.HumanoidRootPart,
            TweenInfo.new(Distance/380, Enum.EasingStyle.Linear),
            {CFrame = Pos}
        )
        tween:Play()
    end)
end

function EquipWeapon(ToolSe)
    if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
        Tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
        game.Players.LocalPlayer.Character.Humanoid:EquipTool(Tool)
    end
end

randomNumberUI = math.random(1,4)
_G.UIB = "17075379093"

if randomNumberUI == 1 then
    _G.TeamBlack =  true
elseif randomNumberUI == 2 then
    _G.TeamWhite = true
elseif randomNumberUI == 3 then
    _G.TeamGreen = true
elseif randomNumberUI == 4 then
    _G.TeamRed = true
else
    _G.Color = Color3.fromRGB(0,120,120)--Color3.fromRGB(120,35,100)
    _G.FrameTop = Color3.fromRGB(0,100,100)--Color3.fromRGB(100, 35, 35)
    _G.FrameTab =  Color3.fromRGB(0,75,75)--Color3.fromRGB(75, 35, 35)
    _G.PageFrame = Color3.fromRGB(0,85,85)--Color3.fromRGB(85, 35, 35)
    _G.ColorI = Color3.fromRGB(0,100,100)--Color3.fromRGB(100, 45, 45)
end

 --Vars
LocalPlayer = game:GetService("Players").LocalPlayer
Camera = workspace.CurrentCamera
VirtualUser = game:GetService("VirtualUser")
MarketplaceService = game:GetService("MarketplaceService")

--Get Current Vehicle
function GetCurrentVehicle()
    return LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") and LocalPlayer.Character.Humanoid.SeatPart and LocalPlayer.Character.Humanoid.SeatPart.Parent
end

--Regular TP
function TP(cframe)
    GetCurrentVehicle():SetPrimaryPartCFrame(cframe)
end
spawn(function()
	while wait() do
--Velocity TP
        function VelocityTP(cframe)
            pcall(function()
                --TeleportSpeed = math.random(600, 600) ---600,600
                Car = GetCurrentVehicle()
                local BodyGyro = Instance.new("BodyGyro", Car.PrimaryPart)
                BodyGyro.P = 5000
                BodyGyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
                BodyGyro.CFrame = Car.PrimaryPart.CFrame
                local BodyVelocity = Instance.new("BodyVelocity", Car.PrimaryPart)
                BodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
                BodyVelocity.Velocity = CFrame.new(Car.PrimaryPart.Position, cframe.p).LookVector * TeleportSpeed
                wait((Car.PrimaryPart.Position - cframe.p).Magnitude / TeleportSpeed)
                BodyVelocity.Velocity = Vector3.new()
                wait(0.1)
                BodyVelocity:Destroy()
                BodyGyro:Destroy()
            end)
        end
    end
end)


--Auto Farm
StartPosition = CFrame.new(Vector3.new(4940.19775, 66.0195084, -1933.99927, 0.343969434, -0.00796990748, -0.938947022, 0.00281227613, 0.999968231, -0.00745762791, 0.938976645, -7.53822824e-05, 0.343980938), Vector3.new())
EndPosition = CFrame.new(Vector3.new(1827.3407, 66.0150146, -658.946655, -0.366112858, 0.00818905979, 0.930534422, 0.00240773871, 0.999966264, -0.00785277691, -0.930567324, -0.000634518801, -0.366120219), Vector3.new())

AutoFarmFunc = coroutine.create(function()
    while wait() do
        if not AutoFarm then
            AutoFarmRunning = false
            coroutine.yield()
        end
        AutoFarmRunning = true
        pcall(function()
            if not GetCurrentVehicle() and tick() - (LastNotif or 0) > 5 then
                LastNotif = tick()
            else
                TP(StartPosition + (TouchTheRoad and Vector3.new(0,0,0) or Vector3.new(0, 0, 0)))
                VelocityTP(EndPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
                TP(EndPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
                VelocityTP(StartPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
            end
        end)
    end
end)

spawn(function()
	while wait() do
		if AutoFarmByMax then
            pcall(function()
                if not GetCurrentVehicle() and tick() - (LastNotif or 0) > 5 then
                    LastNotif = tick()
                else
                    --if (EndDPosition.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 2300 then
                        --game:GetService("VirtualInputManager"):SendKeyEvent(true,"W",false,game) wait(100)
                        --game:GetService("VirtualInputManager"):SendKeyEvent(false,"W",false,game) wait(.1)
                    --else
                        TP(StartPosition + (TouchTheRoad and Vector3.new(0,0,0) or Vector3.new(0, 0, 0)))
                        VelocityTP(EndPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
                        TP(EndPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
                        --VelocityTP(StartPosition + (TouchTheRoad and Vector3.new() or Vector3.new(0, 0, 0)))
                    --end
                end
            end)
        end
    end
end)
--Anti AFK
AntiAFK = true
LocalPlayer.Idled:Connect(function()
    VirtualUser:CaptureController()
    VirtualUser:ClickButton2(Vector2.new(), Camera.CFrame)
end)

_G.Color = Color3.fromRGB(0,120,120)--Color3.fromRGB(120,35,100)
_G.FrameTop = Color3.fromRGB(0,100,100)--Color3.fromRGB(100, 35, 35)
_G.FrameTab =  Color3.fromRGB(0,75,75)--Color3.fromRGB(75, 35, 35)
_G.PageFrame = Color3.fromRGB(0,85,85)--Color3.fromRGB(85, 35, 35)
_G.ColorI = Color3.fromRGB(0,100,100)--Color3.fromRGB(100, 45, 45)

local Update = loadstring(game:HttpGet("https://pastebin.com/raw/LZBa7hU1"))()


local Library = Update:Window("MrMaxNaJa Community","",Enum.KeyCode.RightControl);
Main = Library:Tab("Main")
Main:Line()

TeleportSpeed = 600

Main:Slider("Teleport Speed",550,750,TeleportSpeed,function(value)
    TeleportSpeed = value
end)

Main:Toggle("Auto Farm By MrMaxNaJa",AutoFarmByMax,function(value)
    AutoFarmByMax = value
    _G.White_Screen = value
end)
Main:Toggle("Auto Farm",AutoFarm,function(value)
    AutoFarm = value
    if value and not AutoFarmRunning then
        coroutine.resume(AutoFarmFunc)
    end
end)
Main:Toggle("TouchTheRoad",TouchTheRoad, function(value)
    TouchTheRoad = value
end)
Main:Toggle("AntiAFK",AntiAFK, function(value)
    AntiAFK = value
end)
Main:Label("Fps Boost")
Main:Toggle("White Screen",_G.White_Screen,function(v)
	_G.White_Screen = v
end)
spawn(function()
	while wait() do
		if _G.White_Screen then
			game:GetService("RunService"):Set3dRenderingEnabled(false)
		else
			game:GetService("RunService"):Set3dRenderingEnabled(true)
		end
	end
end)
Main:Button("BoostFps",function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/MarsQQ/ScriptHubScripts/master/FPS%20Boost"))()
end)
Main:Toggle("Xray",false,function(value)
    NoWorld = value
    if NoWorld == true then
        transparent = true
        x(transparent)
    elseif NoWorld == false then
        transparent = false
        x(transparent)
    end
end)

local transparent = false -- xray
function x(v)
    if v then
        for _,i in pairs(workspace:GetDescendants()) do
            if i:IsA("BasePart") and not i.Parent:FindFirstChild("Humanoid") and not i.Parent.Parent:FindFirstChild("Humanoid") then
                i.LocalTransparencyModifier = 0.7
            end
        end
    else
        for _,i in pairs(workspace:GetDescendants()) do
            if i:IsA("BasePart") and not i.Parent:FindFirstChild("Humanoid") and not i.Parent.Parent:FindFirstChild("Humanoid") then
                i.LocalTransparencyModifier = 0
            end
        end
    end
end
Main:Line()
Main:Button("Max Zoom", function()
    while wait() do
        game.Players.LocalPlayer.CameraMaxZoomDistance = 9223372036854718
    end
end)

Main:Line()
Main:Toggle("NoClip | ทะลุ",_G.NOCLIP,function(value)
    _G.NOCLIP = value
end)

spawn(function()
	pcall(function() --velocity
		game:GetService("RunService").Stepped:Connect(function()
			if _G.NoClip then
                for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                    if v:IsA("BasePart") then
                        v.CanCollide = false    
                    end
                end
            end
		end)
	end)
end)
_G.Rejoin = true
spawn(function()
	while wait() do
		if _G.Rejoin then
			Rejoin = game:GetService("CoreGui").RobloxPromptGui.promptOverlay.ChildAdded:Connect(function(v)
                if v.Name == 'ErrorPrompt' and v:FindFirstChild('MessageArea') and v.MessageArea:FindFirstChild("ErrorFrame") then
                    print("AutoRejoin!")
                    game:GetService("TeleportService"):Teleport(game.PlaceId)
                end
			end)
		end
	end
end)
