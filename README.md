# climb-and-jump-trophy-1q
trophy 1q 
local function createBlock(position, size, color)
	local part = Instance.new("Part")
	part.Anchored = true
	part.Position = position
	part.Size = size
	part.Color = color
	part.Parent = workspace
	return part
end

-- Lantai dasar
createBlock(Vector3.new(0, 0.5, 0), Vector3.new(100, 1, 100), Color3.fromRGB(100, 255, 100))

-- Tangga naik
for i = 1, 10 do
	createBlock(Vector3.new(0, i * 5, 0), Vector3.new(10, 1, 10), Color3.fromRGB(255, 255 - i * 20, 0))
end

-- Puncak
local top = createBlock(Vector3.new(0, 60, 0), Vector3.new(20, 1, 20), Color3.fromRGB(0, 0, 255))

-- Trophy
local trophy = Instance.new("Part")
trophy.Name = "Trophy"
trophy.Shape = Enum.PartType.Ball
trophy.Color = Color3.fromRGB(255, 215, 0)
trophy.Size = Vector3.new(4, 4, 4)
trophy.Position = Vector3.new(0, 63, 0)
trophy.Anchored = true
trophy.Parent = workspace

local scriptObj = Instance.new("Script")
scriptObj.Name = "TrophyScript"
scriptObj.Source = [[
local TROPHY_VALUE = 1000000000000000
local part = script.Parent
local debounce = false

local function onTouched(hit)
	if debounce then return end
	local player = game.Players:GetPlayerFromCharacter(hit.Parent)
	if not player then return end
	debounce = true

	local stats = player:FindFirstChild("leaderstats")
	if stats then
		local money = stats:FindFirstChild("Money")
		if money then
			money.Value += TROPHY_VALUE
			print(player.Name .. " mendapatkan trophy 1Q!")
		end
	end

	part.Transparency = 1
	wait(1)
	part:Destroy()
end

part.Touched:Connect(onTouched)
]]
scriptObj.Parent = trophy
