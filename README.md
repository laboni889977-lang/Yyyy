-- ==========================================
-- 🎮 Custom Game Movement & Velocity Script
-- ==========================================

-- Player Configuration
local player = {
    id = 1,
    name = "Player1",
    position = {x = 0.0, y = 0.0, z = 0.0},
    velocity = {x = 0.0, y = 0.0, z = 0.0},
    moveSpeed = 10.0,
    jumpForce = 15.0,
    backjumpPower = -20.0
}

-- 1. Vector Calculation Helper Function
function Vector3(x, y, z)
    return {x = x, y = y, z = z}
end

-- 2. Apply Impulse/Velocity to Player
function ApplyVelocity(targetPlayer, dirX, dirY, dirZ, force)
    targetPlayer.velocity.x = dirX * force
    targetPlayer.velocity.y = dirY * force
    targetPlayer.velocity.z = dirZ * force
    
    print(targetPlayer.name .. " Applied Velocity -> X: " .. targetPlayer.velocity.x .. " | Y: " .. targetPlayer.velocity.y .. " | Z: " .. targetPlayer.velocity.z)
end

-- 3. Backjump Logic (পছনে লাফ দেওয়ার লজিক)
function TriggerBackjump(targetPlayer)
    -- Backward vector force
    local backDirectionX = 0.0
    local upDirectionY = 1.0  -- Upward impulse
    local backDirectionZ = -1.0 -- Backward impulse
    
    print(">>> Executing Backjump Skill <<<")
    ApplyVelocity(targetPlayer, backDirectionX, upDirectionY, backDirectionZ, targetPlayer.jumpForce)
end

-- 4. Speed Boost Logic (গতি বাড়ানোর লজিক)
function ApplySpeedBoost(targetPlayer, multiplier, durationSeconds)
    local originalSpeed = targetPlayer.moveSpeed
    targetPlayer.moveSpeed = originalSpeed * multiplier
    print(targetPlayer.name .. " Speed Boosted! New Speed: " .. targetPlayer.moveSpeed)
end

-- ==========================================
-- 🚀 Execution Test (লজিক ট্রিগার টেস্ট)
-- ==========================================

-- টেস্ট ১: ব্যাকজাম্প ট্রিগার করা
TriggerBackjump(player)

-- টেস্ট ২: ২ গুণ স্পিড বুস্ট দেওয়া
ApplySpeedBoost(player, 2.0, 5)
