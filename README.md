-- =====================================================================
-- BLOX FRUIT CHECKER v4.0 — DIRECT WEBHOOK (KHÔNG CẦN SERVER)
-- Chức năng: Xác thực tài khoản, check kho mỗi 60s, báo cáo khi nhấn P
-- =====================================================================

-- ╔═══════════════════════════════════════════════════════════════════╗
-- ║  ⚠️  DÁN URL WEBHOOK CỦA BẠN VÀO ĐÂY (Giữ nguyên dấu ngoặc kép) ║
-- ╚═══════════════════════════════════════════════════════════════════╝
local WEBHOOK_URL = "https://discord.com/api/webhooks/YOUR_ID/YOUR_TOKEN"

-- Tùy chọn cấu hình
local CHECK_INTERVAL = 60      -- 60 giây check 1 lần
local MATERIAL_COST  = 5       -- Trừ 5 nguyên liệu mỗi khi có item mới (chỉ hiển thị log)
local SHUTDOWN_KEY   = Enum.KeyCode.P -- Nhấn P để kết thúc và gửi báo cáo

-- =====================================================================
-- SERVICES & BIẾN TOÀN CỤC
-- =====================================================================
local HttpService = game:GetService("HttpService")
local Players     = game:GetService("Players")
local UIS         = game:GetService("UserInputService")
local RS          = game:GetService("ReplicatedStorage")
local player      = Players.LocalPlayer

local SESSION_START = os.time()
local SESSION_ID    = tostring(math.random(100000, 999999))
local SHUTDOWN_FLAG = false
local SHARED_INV    = {}
local baselineSet   = false

-- =====================================================================
-- 1. GAME GUARD (Chỉ chạy nếu là Blox Fruit)
-- =====================================================================
local BLOX_PLACES = {[2753915549]="Sea 1",[4442272183]="Sea 2",[7449423635]="Sea 3"}
local remotes = RS:FindFirstChild("Remotes")
local commF = remotes and remotes:FindFirstChild("CommF_")

if not (BLOX_PLACES[game.PlaceId] or game.CreatorId == 3318366760 or commF) then
    warn("[GUARD ❌] Đây không phải Blox Fruit. Dừng script.")
    return
end
print("[GUARD ✅] Đã xác nhận Blox Fruit: " .. (BLOX_PLACES[game.PlaceId] or "CommF_"))

-- =====================================================================
-- 2. HÀM GỬI DISCORD (Hỗ trợ mọi Executor)
-- =====================================================================
local webhookMethod = "none"
local function sendEmbed(embeds)
    if WEBHOOK_URL:find("YOUR_") then
        warn("[WEBHOOK ❌] Bạn chưa thay URL Webhook thật vào dòng 12!")
        return false
    end
    
    local payload = HttpService:JSONEncode({username = "Blox Fruit Checker", embeds = embeds})
    
    -- Thử các hàm request của executor
    local try = {
        {name="request", fn=request},
        {name="syn.request", fn=syn and syn.request},
        {name="http.request", fn=http and http.request},
    }
    for _, t in ipairs(try) do
        if type(t.fn) == "function" then
            local ok, res = pcall(function()
                return t.fn({Url=WEBHOOK_URL, Method="POST", Headers={["Content-Type"]="application/json"}, Body=payload})
            end)
            if ok and res and (res.StatusCode==200 or res.StatusCode==204 or res.Success) then
                webhookMethod = t.name
                print("[WEBHOOK ✅] Gửi thành công qua " .. webhookMethod)
                return true
            end
        end
    end
    
    -- Fallback cho Roblox Studio
    local okH, errH = pcall(function()
        HttpService:PostAsync(WEBHOOK_URL, payload, Enum.HttpContentType.ApplicationJson)
    end)
    if okH then
        webhookMethod = "HttpService"
        print("[WEBHOOK ✅] Gửi thành công qua HttpService")
        return true
    end
    
    warn("[WEBHOOK ❌] Gửi thất bại. Hãy chắc chắn Executor của bạn hỗ trợ request.")
    return false
end

-- =====================================================================
-- 3. PHÂN LOẠI VẬT PHẨM
-- =====================================================================
local FRUITS = {["Rocket"]=1,["Spin"]=1,["Chop"]=1,["Spring"]=1,["Bomb"]=1,["Smoke"]=1,["Spike"]=1,["Flame"]=1,["Falcon"]=1,["Ice"]=1,["Sand"]=1,["Dark"]=1,["Diamond"]=1,["Light"]=1,["Rubber"]=1,["Barrier"]=1,["Ghost"]=1,["Magma"]=1,["Door"]=1,["Quake"]=1,["Human"]=1,["Buddha"]=1,["Love"]=1,["Spider"]=1,["Sound"]=1,["Phoenix"]=1,["Portal"]=1,["Rumble"]=1,["Pain"]=1,["Blizzard"]=1,["Gravity"]=1,["Mammoth"]=1,["T-Rex"]=1,["Dough"]=1,["Shadow"]=1,["Venom"]=1,["Control"]=1,["Spirit"]=1,["Dragon"]=1,["Leopard"]=1,["Kitsune"]=1,["Yeti"]=1,["Gas"]=1}
local SWORDS = {["Cutlass"]=1,["Katana"]=1,["Iron Mace"]=1,["Dual Katana"]=1,["Triple Katana"]=1,["Wando"]=1,["Saddi"]=1,["Longsword"]=1,["Shisui"]=1,["Rengoku"]=1,["Dark Blade"]=1,["Buddy Sword"]=1,["Hallow Scythe"]=1,["Hollow Scythe"]=1,["True Triple Katana"]=1,["Cursed Dual Katana"]=1,["Yama"]=1,["Tushita"]=1,["Koko"]=1,["Pole (1st Form)"]=1,["Pole (2nd Form)"]=1,["Trident"]=1,["Shark Saw"]=1,["Midnight Blade"]=1,["Dragonheart"]=1,["Soul Cane"]=1,["Fox Lamp"]=1,["Twin Hooks"]=1,["Serpent Bow"]=1}
local STYLES = {["Combat"]=1,["Dark Step"]=1,["Electric Claw"]=1,["Fishman Karate"]=1,["Dragon Talon"]=1,["Superhuman"]=1,["Death Step"]=1,["Sharkman Karate"]=1,["Godhuman"]=1,["Sanguine Art"]=1}
local GUNS = {["Flintlock"]=1,["Slingshot"]=1,["Cannon"]=1,["Musket"]=1,["Cursed Dual Pistols"]=1,["Kabucha"]=1,["Bizarre Rifle"]=1,["Dragonstorm"]=1}
local ICONS = {Fruit="🍎",Sword="⚔️",FightingStyle="🥋",Gun="🔫",Other="📦"}

local function classify(name)
    local n = name:lower()
    if FRUITS[name] or n:find("fruit") then return "Fruit" end
    if SWORDS[name] or n:find("sword") or n:find("katana") or n:find("blade") or n:find("scythe") then return "Sword" end
    if STYLES[name] then return "FightingStyle" end
    if GUNS[name] or n:find("gun") or n:find("rifle") then return "Gun" end
    return "Other"
end

-- =====================================================================
-- 4. LẤY KHO ĐỒ
-- =====================================================================
local function getInventory()
    local inv = {}
    if commF then
        local ok, data = pcall(function() return commF:InvokeServer("getInventory") end)
        if ok and type(data) == "table" then
            for _, item in pairs(data) do
                if type(item) == "table" and item.Name then
                    inv[item.Name] = (inv[item.Name] or 0) + (item.Count or 1)
                end
            end
        end
    end
    return inv
end

-- =====================================================================
-- 5. GỬI THÔNG BÁO ĐĂNG NHẬP
-- =====================================================================
local function notifyLogin()
    sendEmbed({{
        title = "🟢 TÀI KHOẢN ĐANG HOẠT ĐỘNG",
        description = "**Tài khoản:** `"..player.Name.."`\n**User ID:** `"..player.UserId.."`\n**Session ID:** `"..SESSION_ID.."`",
        color = 0x00FF00,
        fields = {
            {name="📡 Server", value="`"..game.JobId.."`", inline=false},
            {name="🗺️ Sea", value=BLOX_PLACES[game.PlaceId] or "Unknown", inline=true},
            {name="⏱️ Check mỗi", value="**"..CHECK_INTERVAL.."s**", inline=true},
        },
        footer = {text="Bắt đầu: "..os.date("%Y-%m-%d %H:%M:%S")}
    }})
end

-- =====================================================================
-- 6. GỬI BÁO CÁO KẾT THÚC
-- =====================================================================
local function notifySessionEnd(reason)
    local duration = os.time() - SESSION_START
    local counts = {Fruit=0, Sword=0, FightingStyle=0, Gun=0, Other=0}
    local total = 0
    
    for name, info in pairs(SHARED_INV) do
        if info.count > 0 then
            counts[classify(name)] = counts[classify(name)] + info.count
            total = total + info.count
        end
    end

    sendEmbed({{
        title = "🔴 TÀI KHOẢN KẾT THÚC HOẠT ĐỘNG — "..player.Name,
        description = "**Lý do:** "..reason.."\n**Thời lượng:** **"..math.floor(duration/60).." phút**",
        color = 0xE74C3C,
        fields = {
            {name="🍎 Trái", value=tostring(counts.Fruit), inline=true},
            {name="⚔️ Kiếm", value=tostring(counts.Sword), inline=true},
            {name="🥋 Võ thuật", value=tostring(counts.FightingStyle), inline=true},
            {name="🔫 Súng", value=tostring(counts.Gun), inline=true},
            {name="📦 Khác", value=tostring(counts.Other), inline=true},
            {name="📊 Tổng", value="**"..total.."**", inline=true},
        }
    }})
    
    task.wait(1)
    
    -- Gửi chi tiết kho đồ
    local groups = {Fruit={}, Sword={}, FightingStyle={}, Gun={}, Other={}}
    for name, info in pairs(SHARED_INV) do
        if info.count > 0 then table.insert(groups[classify(name)], {name=name, count=info.count}) end
    end
    
    local fields, chunk = {}, {}
    for cat, items in pairs(groups) do
        if #items > 0 then
            table.sort(items, function(a,b) return a.count > b.count end)
            local lines = {}
            for i=1, math.min(#items, 30) do table.insert(lines, "• **"..items[i].name.."** ×"..items[i].count) end
            table.insert(chunk, {name=ICONS[cat].." "..cat:upper().." ("..#items..")", value=table.concat(lines, "\n"), inline=false})
            
            if #chunk >= 8 then
                sendEmbed({{title="📋 Chi tiết kho đồ", color=0x9B59B6, fields=chunk}})
                chunk = {}; task.wait(1)
            end
        end
    end
    if #chunk > 0 then sendEmbed({{title="📋 Chi tiết kho đồ", color=0x9B59B6, fields=chunk}}) end
end

-- =====================================================================
-- 7. VÒNG LẶP KIỂM TRA (60s/lần)
-- =====================================================================
local function checkCycle()
    local current = getInventory()
    local newItems = {}
    
    for name, count in pairs(current) do
        local old = SHARED_INV[name] and SHARED_INV[name].count or 0
        if count > old then newItems[name] = count - old end
        SHARED_INV[name] = {count=count, type=classify(name)}
    end
    
    if baselineSet and next(newItems) ~= nil then
        local totalNew = 0
        for _, diff in pairs(newItems) do totalNew = totalNew + diff end
        print("[CHECK] +"..totalNew.." item mới. Trừ "..(totalNew*MATERIAL_COST).." nguyên liệu.")
        
        local fields = {}
        for name, diff in pairs(newItems) do
            table.insert(fields, {name="✨ "..name, value="+"..diff.." (tổng: "..SHARED_INV[name].count..")", inline=false})
        end
        sendEmbed({{title="📦 Vật phẩm mới — "..player.Name, color=0x3498DB, fields=fields}})
    else
        print("[CHECK] Không có item mới. ("..os.date("%H:%M:%S")..")")
    end
end

-- =====================================================================
-- 8. SHUTDOWN HANDLER
-- =====================================================================
local function shutdown(reason)
    if SHUTDOWN_FLAG then return end
    SHUTDOWN_FLAG = true
    print("[SHUTDOWN] Đang gửi báo cáo: "..reason)
    pcall(notifySessionEnd, reason)
end

UIS.InputBegan:Connect(function(input, gp)
    if gp then return end
    if input.KeyCode == SHUTDOWN_KEY then shutdown("Nhấn phím P") end
end)
pcall(function() player.OnTeleport:Connect(function() shutdown("Teleport") end) end)
pcall(function() Players.PlayerRemoving:Connect(function(p) if p == player then shutdown("Disconnect") end end) end)

-- =====================================================================
-- 9. KHỞI CHẠY
-- =====================================================================
print("==============================================")
print(" BLOX FRUIT CHECKER v4.0")
print(" Account: "..player.Name)
print(" Nhấn ["..SHUTDOWN_KEY.Name.."] để kết thúc & báo cáo.")
print("==============================================")

notifyLogin()
task.wait(2)

-- Lưu kho đồ ban đầu
local snap = getInventory()
for name, count in pairs(snap) do SHARED_INV[name] = {count=count, type=classify(name)} end
baselineSet = true

-- Bắt đầu vòng lặp
task.spawn(function()
    while not SHUTDOWN_FLAG do
        task.wait(CHECK_INTERVAL)
        if SHUTDOWN_FLAG then break end
        pcall(checkCycle)
    end
end)
