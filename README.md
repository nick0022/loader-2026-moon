--// Game Scripts Database (GameId -> Script Info)
        local GameScripts = {
            ["2023680558"] = { name = "Animal Simulator", url = "https://api.jnkie.com/api/v1/luascripts/public/6e89ed0fc5cabc676513be69c347c6f2b3566c1a6547d30202eb7a2bbf9007e7/download", icon = "🐾" },
            ["5909935640"] = { name = "Mush Yo", url = "https://api.jnkie.com/api/v1/luascripts/public/dcded354e622870c151e87f40c873c1d9387a702ec0c41fc9916c40ff51a237e/download", icon = "🍄" },
            ["5421899973"] = { name = "Combat Arena", url = "https://api.jnkie.com/api/v1/luascripts/public/c8ae7551adf5c8beeb810ac38549f5d8a95e08f813988e02f8ab8e461ef1f29f/download", icon = "⚔️" },
            ["6701277882"] = { name = "Fish it", url = "https://api.jnkie.com/api/v1/luascripts/public/1d7cf9433a4c043fca6f23f0a573742428b7e970a6f5dd4000493892252bf557/download", icon = "🐟" },
            ["7585079192"] = { name = "Anime Story", url = "https://api.jnkie.com/api/v1/luascripts/public/0982e25bc5a662039985cc258a0401e9fca50425083acd0f90861c2671d261f9/download", icon = "🔮" },
            ["9266873836"] = { name = "Anime Fighting Simulator: Endless", url = "https://api.jnkie.com/api/v1/luascripts/public/a18c8cd6892a87814a7464804312acebf86e19b900528a7d8ae1a832c65a1237/download", icon = "🥷🏻" },
        }

local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local UserInputService = game:GetService("UserInputService")
local MarketplaceService = game:GetService("MarketplaceService")

local player = Players.LocalPlayer

local currentGameId = tostring(game.GameId) 
local detectedGame = GameScripts[currentGameId]

print("═══════════════════════════════════════════")
print("🌙 MoonHUB Auto Loader v3")
print("═══════════════════════════════════════════")
print("📍 Current Game ID (Universe):", currentGameId)

task.wait(3)

if detectedGame then
    print("✅ Game Detected:", detectedGame.icon, detectedGame.name)
    print("🚀 Auto-loading script in 2 seconds...")
    
    task.wait(2)
    
    print("📥 Loading script...")
    
    local success, err = pcall(function()
        loadstring(game:HttpGet(detectedGame.url))()
    end)
    
    if success then
        print("✅ Script loaded successfully!")
    else
        warn("❌ Failed to load script:", err)
        print("🔄 Retrying in 3 seconds...")
        
        task.wait(3)
        
        local success2, err2 = pcall(function()
            loadstring(game:HttpGet(detectedGame.url))()
        end)
        
        if success2 then
            print("✅ Script loaded on retry!")
        else
            warn("❌ Script failed to load after retry:", err2)
        end
    end
else
    print("⚠️ Game not supported!")
    print("📋 Supported games (By Game ID):")
    for id, gameInfo in pairs(GameScripts) do
        print("   •", gameInfo.icon, gameInfo.name, "(ID:", id .. ")")
    end
    print("═══════════════════════════════════════════")
end
