local library = loadstring(game:HttpGet(('https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/wall%20v3')))()

local w = library:CreateWindow("discord.gg/altgenerators") -- Creates the window

local b = w:CreateFolder("Script") -- Creates the folder(U will put here your buttons,etc)

b:Label("All Script",{
    TextSize = 25; -- Self Explaining
    TextColor = Color3.fromRGB(255,255,255); -- Self Explaining
    BgColor = Color3.fromRGB(69,69,69); -- Self Explaining
    
}) 

b:Toggle("Fast Waiters & Reach",function(bool)
    shared.toggle = bool
    local npcReach = true

local Client = game.Players.LocalPlayer
local PS = Client.PlayerScripts
local Module = require(PS.ClientMain.Replications.Workers.DummyWalkSequence)
local Worker = require(PS.CookingNew.WorkerComponents.WorkerDefault)
local M1 = require(PS.ClientMain.Replications.Customers.GetNPCFolder)



if npcReach then
   Module.Run = function(data)
       return (data.completeCallback or task.wait)()
   end
end
local npcReach = true
 
if npcReach then
   hookfunction(Module,function()
       return task.wait()
   end)
end
end)

b:Toggle("Collect Bill",function(bool)
    shared.toggle = bool
    warn("Requiring API")do
  loadstring(game:HttpGet("https://pastebin.com/raw/KMc6aBky"))();
end warn("API Loaded")
 
local child = object.child
local descendant = object.descendant
local check = object.check
 
local Tycoon = game.Players.LocalPlayer.Tycoon.Value
descendant.foreach(Tycoon.Items.OftenFiltered.Surface,"Bill",function(Bill)
  local Settings = {
          ["name"] = "CollectBill",
          ["model"] = Bill.Parent
  }
 
  game.ReplicatedStorage.Events.ClientTycoonInput:FireServer(Tycoon,Settings)
end)
 
local Connection,Code = descendant.on_add(Tycoon.Items.OftenFiltered.Surface,function(Bill)
  check.it(Bill.Name == "Bill",function()
      local Settings = {
              ["name"] = "CollectBill",
              ["model"] = Bill.Parent
      }
 
      game.ReplicatedStorage.Events.ClientTycoonInput:FireServer(Tycoon,Settings)
  end)
end)
 
end)

b:Toggle("Npc Instant Cook",function(bool)
    shared.toggle = bool
    local chiefInstantCook = true
local npcReach = true
 
local Client = game.Players.LocalPlayer
local PS = Client.PlayerScripts
local Module = require(PS.ClientMain.Replications.Workers.WalkDummy)
local Worker = require(PS.CookingNew.WorkerComponents.WorkerDefault)
local M1 = require(PS.ClientMain.Replications.Customers.GetNPCFolder)
 
 
 
if npcReach then
   hookfunction(Module,function()
       return task.wait()
   end)
end
 
if chiefInstantCook then
   Worker.event = function(...)
      local args = {...}
      local npc = M1.GetNPCFolder(args[1]).ClientWorkers:FindFirstChild(args[2])
      local M2 = game.ReplicatedStorage.MiscModules.CookingSharedCharacter:FindFirstChild(args[4])
      if M2 then
          require(M2).finishInteract(npc,args[3],args[4])
      end
      return
   end
end
 
end)

b:Toggle("Player InstantCook",function(bool)
    shared.toggle = bool
    local Cooking = game.Players.LocalPlayer.PlayerScripts.CookingNew
local CookProgress = require(Cooking.CookProgress)
local MultiClick = require(Cooking.InputDetectors.MultiClick)
local MouseMovement = require(Cooking.InputDetectors.MouseMovement)
local MouseSpin = require(Cooking.InputDetectors.MouseSpin)
 
local run = CookProgress.run
CookProgress.run = function(...)
  local ARGS = {...}
  ARGS[3] = 0
  return run(unpack(ARGS))
end
 
MultiClick.start = function(...)
  ({...})[3]()
end
 
MouseMovement.start = function(...)
  ({...})[3]()
end
 
MouseSpin.start = function(...)
  ({...})[3]()
end
 
end)

b:Toggle("Instant Happy ( Workers )",function(bool)
    shared.toggle = bool
    local MotiveMin = 95 -- How much motivation is needed to put worker on break
local MotiveMax = 100 -- How much motivation is needed to put worker back to work
local plr = game.Players.LocalPlayer
local Tycoons = workspace.Tycoons:GetChildren()
local WorkerOptions = game:GetService("ReplicatedStorage").Events.WorkerOptions

if not getgenv().Connections then
   getgenv().Connections = {}
   print('Made connections')
else
   for i, v in pairs(getgenv().Connections) do
       v:Disconnect()
       print('Disconnected')
   end
   getgenv().Connections = {}
end

function GetTycoon()
   local t, tt
   for i, v in pairs(workspace.Tycoons:GetChildren()) do
       if v.Player.Value == plr then
           t = v
           tt = true
           break
       else
           t = false
           tt = false
       end
   end
   return { t, tt }
end

local Tycoon
print('Waiting for tycoon')
while not Tycoon do
   local t = GetTycoon()
   if t[2] then
       Tycoon = t[1]
   end
   wait(0.1) -- Wait for a short interval before checking again
end

local Workers = Tycoon.Workers:GetChildren()

for i, worker in pairs(Workers) do
   local MotiveVal = worker.Motivation
   table.insert(getgenv().Connections, MotiveVal.Changed:Connect(function()
       if MotiveVal.Value < MotiveMin then
           WorkerOptions:FireServer("PutOnBreak", worker.Name, true)
       elseif MotiveVal.Value >= MotiveMax then
           WorkerOptions:FireServer("PutOnBreak", worker.Name, false)
       end
   end))
end

b:DestroyGui()
