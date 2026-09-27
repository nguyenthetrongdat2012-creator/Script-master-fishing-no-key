#scriptmasterfishingnokey
--// DATBEO SCRIPT - FULL
local Players = game:GetService("Players")
local CoreGui = game:GetService("CoreGui")
local Tween   = game:GetService("TweenService")
local VIM     = game:GetService("VirtualInputManager")
local VU      = game:GetService("VirtualUser")
local P       = Players.LocalPlayer

if CoreGui:FindFirstChild("DatBeoGui") then CoreGui.DatBeoGui:Destroy() end

local S = Instance.new("ScreenGui")
S.Name = "DatBeoGui"
S.ResetOnSpawn = false
S.Parent = CoreGui

local C = {
    bg = Color3.fromRGB(15,15,20), bg2 = Color3.fromRGB(25,25,35),
    gold = Color3.fromRGB(255,200,60), cyan = Color3.fromRGB(0,220,255),
    grn = Color3.fromRGB(0,255,130), red = Color3.fromRGB(255,60,80),
    dim = Color3.fromRGB(130,130,145),
}

local function corner(p,r) local c=Instance.new("UICorner",p); c.CornerRadius=UDim.new(0,r or 8) end
local function stroke(p,c,t) local s=Instance.new("UIStroke",p); s.Color=c or C.gold; s.Thickness=t or 1.5; s.Transparency=0.3 end
local function grad(p,c1,c2,r) local g=Instance.new("UIGradient",p); g.Color=ColorSequence.new(c1,c2); g.Rotation=r or 90 end

local function drag(f)
    local d,ds,sp
    f.InputBegan:Connect(function(i)
        if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then
            d=true; ds=i.Position; sp=f.Position
            i.Changed:Connect(function() if i.UserInputState==Enum.UserInputState.End then d=false end end)
        end
    end)
    f.InputChanged:Connect(function(i)
        if d and (i.UserInputType==Enum.UserInputType.MouseMovement or i.UserInputType==Enum.UserInputType.Touch) then
            local x=i.Position-ds
            f.Position=UDim2.new(sp.X.Scale,sp.X.Offset+x.X,sp.Y.Scale,sp.Y.Offset+x.Y)
        end
    end)
end

local function btn(parent,size,pos,text)
    local b=Instance.new("TextButton",parent)
    b.Size=size; b.Position=pos
    b.BackgroundColor3=Color3.fromRGB(30,30,40)
    b.TextColor3=Color3.fromRGB(220,220,230)
    b.TextSize=11; b.Font=Enum.Font.GothamBold; b.Text=text
    b.BorderSizePixel=0; b.AutoButtonColor=false
    corner(b,6)
    b.MouseEnter:Connect(function() Tween:Create(b,TweenInfo.new(0.15),{BackgroundColor3=Color3.fromRGB(50,50,65)}):Play() end)
    b.MouseLeave:Connect(function() Tween:Create(b,TweenInfo.new(0.15),{BackgroundColor3=Color3.fromRGB(30,30,40)}):Play() end)
    return b
end

--// LOADING
local Load = Instance.new("Frame",S)
Load.Size=UDim2.new(0,260,0,90); Load.Position=UDim2.new(0.5,-130,0.5,-45)
Load.BackgroundColor3=C.bg; Load.BorderSizePixel=0
corner(Load,12); stroke(Load,C.grn,2); grad(Load,C.bg2,C.bg)

local LoadTitle=Instance.new("TextLabel",Load)
LoadTitle.Size=UDim2.new(1,0,0,30); LoadTitle.Position=UDim2.new(0,0,0,10)
LoadTitle.BackgroundTransparency=1; LoadTitle.TextColor3=C.gold
LoadTitle.TextSize=14; LoadTitle.Font=Enum.Font.GothamBold; LoadTitle.Text="⚡ DATBEO SCRIPT ⚡"

local LoadText=Instance.new("TextLabel",Load)
LoadText.Size=UDim2.new(1,0,0,20); LoadText.Position=UDim2.new(0,0,0,40)
LoadText.BackgroundTransparency=1; LoadText.TextColor3=C.grn
LoadText.TextSize=11; LoadText.Font=Enum.Font.Gotham; LoadText.Text="Đang tải..."

local BarBg=Instance.new("Frame",Load)
BarBg.Size=UDim2.new(0.85,0,0,6); BarBg.Position=UDim2.new(0.075,0,0,70)
BarBg.BackgroundColor3=Color3.fromRGB(30,30,40); BarBg.BorderSizePixel=0
corner(BarBg,3)

local BarFill=Instance.new("Frame",BarBg)
BarFill.Size=UDim2.new(0,0,1,0); BarFill.BackgroundColor3=C.grn
BarFill.BorderSizePixel=0; corner(BarFill,3); grad(BarFill,C.grn,C.cyan)

--// MAIN
local Main=Instance.new("Frame",S)
Main.Size=UDim2.new(0,230,0,410); Main.Position=UDim2.new(0.05,0,0.15,0)
Main.BackgroundColor3=C.bg; Main.Visible=false; Main.BorderSizePixel=0
corner(Main,12); local MS=stroke(Main,C.gold,1.5); grad(Main,C.bg2,C.bg)
drag(Main)

local Head=Instance.new("Frame",Main)
Head.Size=UDim2.new(1,0,0,36); Head.BackgroundColor3=C.bg2; Head.BorderSizePixel=0
corner(Head,12); grad(Head,Color3.fromRGB(45,38,25),Color3.fromRGB(25,25,35))

local Title=Instance.new("TextLabel",Head)
Title.Size=UDim2.new(1,0,1,0); Title.BackgroundTransparency=1
Title.TextColor3=C.gold; Title.TextSize=12; Title.Font=Enum.Font.GothamBold
Title.Text="⚡ DATBEO SCRIPT ⚡"

--// NÚT
local BtnAuto = btn(Main,UDim2.new(0,206,0,34),UDim2.new(0,12,0,44),"🎣 AUTO CÂU: OFF")
BtnAuto.TextColor3=C.grn

local BtnSkill = btn(Main,UDim2.new(0,206,0,28),UDim2.new(0,12,0,82),"⚔️ AUTO SKILL: OFF")
BtnSkill.TextColor3=C.grn

local BtnMini = btn(Main,UDim2.new(0,206,0,28),UDim2.new(0,12,0,114),"🎮 AUTO MINI: OFF")
BtnMini.TextColor3=C.grn

local BtnClick = btn(Main,UDim2.new(0,206,0,28),UDim2.new(0,12,0,146),"🖱️ AUTO CLICK: OFF")
BtnClick.TextColor3=C.grn

local BtnLock = btn(Main,UDim2.new(0,206,0,28),UDim2.new(0,12,0,178),"🔒 KHÓA: OFF")
BtnLock.TextColor3=C.grn

local BtnUnlock = btn(Main,UDim2.new(0,206,0,28),UDim2.new(0,12,0,210),"🔓 MỞ KHÓA")
BtnUnlock.TextColor3=C.gold

local BtnSell = btn(Main,UDim2.new(0,206,0,28),UDim2.new(0,12,0,242),"💰 SELL ALL")
BtnSell.TextColor3=C.gold

local BtnAutoSell = btn(Main,UDim2.new(0,206,0,28),UDim2.new(0,12,0,274),"💰 AUTO SELL: OFF")
BtnAutoSell.TextColor3=C.gold

--// Ô NHẬP SỐ CÁ
local CountBg = Instance.new("Frame", Main)
CountBg.Size = UDim2.new(0, 206, 0, 28)
CountBg.Position = UDim2.new(0, 12, 0, 306)
CountBg.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
CountBg.BorderSizePixel = 0
corner(CountBg, 6)

local CountLabel = Instance.new("TextLabel", CountBg)
CountLabel.Size = UDim2.new(0, 110, 1, 0)
CountLabel.Position = UDim2.new(0, 8, 0, 0)
CountLabel.BackgroundTransparency = 1
CountLabel.TextColor3 = C.dim
CountLabel.TextSize = 10
CountLabel.Font = Enum.Font.Gotham
CountLabel.Text = "Số cá (1-50):"
CountLabel.TextXAlignment = Enum.TextXAlignment.Left

local CountBox = Instance.new("TextBox", CountBg)
CountBox.Size = UDim2.new(0, 80, 0, 22)
CountBox.Position = UDim2.new(1, -88, 0, 3)
CountBox.BackgroundColor3 = Color3.fromRGB(35, 35, 45)
CountBox.TextColor3 = C.cyan
CountBox.TextSize = 11
CountBox.Font = Enum.Font.GothamBold
CountBox.Text = "10"
CountBox.ClearTextOnFocus = false
CountBox.BorderSizePixel = 0
corner(CountBox, 4)

local BtnSellCount = btn(Main, UDim2.new(0, 206, 0, 28), UDim2.new(0, 12, 0, 338), "🐟 AUTO SELL SỐ: OFF")
BtnSellCount.TextColor3 = C.gold

local Status=Instance.new("TextLabel",Main)
Status.Size=UDim2.new(1,0,0,16); Status.Position=UDim2.new(0,0,0,372)
Status.BackgroundTransparency=1; Status.TextColor3=C.dim
Status.TextSize=10; Status.Font=Enum.Font.Gotham; Status.Text="● Sẵn sàng"

local Close=Instance.new("TextButton",Main)
Close.Size=UDim2.new(0,20,0,20); Close.Position=UDim2.new(1,-26,0,8)
Close.BackgroundColor3=Color3.fromRGB(50,30,30); Close.TextColor3=C.red
Close.TextSize=12; Close.Font=Enum.Font.GothamBold; Close.Text="✕"
Close.BorderSizePixel=0; corner(Close,4)

--// REOPEN
local Reopen=Instance.new("TextButton",S)
Reopen.Size=UDim2.new(0,46,0,46); Reopen.Position=UDim2.new(0,20,0.5,-23)
Reopen.BackgroundColor3=C.bg2; Reopen.TextColor3=C.gold
Reopen.TextSize=20; Reopen.Font=Enum.Font.GothamBold; Reopen.Text="⚡"
Reopen.BorderSizePixel=0; Reopen.Visible=false
corner(Reopen,23); stroke(Reopen,C.gold,2); grad(Reopen,Color3.fromRGB(45,38,25),C.bg2)
drag(Reopen)

--// BIẾN
_G.AutoFish=false; _G.AutoSkill=false; _G.AutoMini=false
_G.AutoClick=false
_G.LockPos=false; _G.AnchorPos=nil
_G.ForceUnlock=false; _G.AutoSell=false
_G.AutoSellCount=false; _G.SellTarget=10; _G.FishCaught=0
local teleCount = 0

--// INPUT
local function K(key, delay)
    delay = delay or 0
    pcall(function() keypress(key) keyrelease(key) end)
    pcall(function()
        VIM:SendKeyEvent(true, key, false, game)
        VIM:SendKeyEvent(false, key, false, game)
    end)
    if delay > 0 then task.wait(delay) end
end

local function Click(hold)
    hold = hold or 0.05
    pcall(function() mouse1press() task.wait(hold) mouse1release() end)
    pcall(function()
        local vp = workspace.CurrentCamera.ViewportSize
        VIM:SendMouseButtonEvent(vp.X/2, vp.Y/2, 0, true, game, 0)
        task.wait(hold)
        VIM:SendMouseButtonEvent(vp.X/2, vp.Y/2, 0, false, game, 0)
    end)
end

--// CHECK FISH CAUGHT
local function CheckFish()
    local function scan(r)
        for _,g in pairs(r:GetDescendants()) do
            if (g:IsA("TextLabel") or g:IsA("TextButton")) then
                if string.find(string.lower(tostring(g.Text or "")),"fish caught") then return true end
            end
        end
        return false
    end
    return (P:FindFirstChild("PlayerGui") and scan(P.PlayerGui)) or scan(CoreGui) or scan(workspace)
end

--// TÌM NPC CÓ CHỮ FISH
local function FindNPC()
    local c = P.Character
    if not c then return nil end
    local h = c:FindFirstChild("HumanoidRootPart")
    if not h then return nil end
    
    local npc, short = nil, math.huge
    
    for _, g in pairs(workspace:GetDescendants()) do
        if g:IsA("Model") or g:IsA("BasePart") then
            local n = g.Name:lower()
            if n:find("fish") then
                local p = g:IsA("BasePart") and g 
                    or g:FindFirstChild("HumanoidRootPart") 
                    or g:FindFirstChildWhichIsA("BasePart")
                if p then
                    local d = (p.Position - h.Position).Magnitude
                    if d < short then short = d; npc = p end
                end
            end
        end
    end
    return npc
end

--// SELL ALL (FLOW: TELE → E → 2 → 1 → 2 → TELE VỀ)
local function SellAll()
    local c=P.Character; if not c then return false,"Không có char" end
    local h=c:FindFirstChild("HumanoidRootPart"); if not h then return false,"Không có HRP" end
    local old=h.CFrame
    local npc=FindNPC(); if not npc then return false,"Không tìm thấy NPC fish" end
    
    -- 1. Tele đến NPC
    h.CFrame=CFrame.new(npc.Position+Vector3.new(0,3,0))
    task.wait(0.8)
    
    -- 2. Bấm E (mở dialogue)
    K(Enum.KeyCode.E, 0.1)
    task.wait(0.8)
    
    -- 3. Bấm 2
    K(Enum.KeyCode.Two, 0.1)
    task.wait(0.5)
    
    -- 4. Bấm 1
    K(Enum.KeyCode.One, 0.1)
    task.wait(0.5)
    
    -- 5. Bấm 2
    K(Enum.KeyCode.Two, 0.1)
    task.wait(0.5)
    
    -- 6. Tele về chỗ cũ
    h.CFrame=old
    task.wait(0.3)
    
    return true,"Đã bán"
end

--// LOCK
local function SaveAnchor()
    local c=P.Character
    if c and c:FindFirstChild("HumanoidRootPart") then
        _G.AnchorPos=c.HumanoidRootPart.Position; _G.LockPos=true
    end
end

task.spawn(function()
    while true do
        task.wait(0.2)
        if not _G.ForceUnlock and _G.LockPos and _G.AnchorPos then
            local c=P.Character
            if c and c:FindFirstChild("HumanoidRootPart") then
                if (c.HumanoidRootPart.Position-_G.AnchorPos).Magnitude>3 then
                    c.HumanoidRootPart.CFrame=CFrame.new(_G.AnchorPos)
                    teleCount = teleCount + 1
                end
            end
        end
    end
end)

--// AUTO SKILL
task.spawn(function()
    while true do
        task.wait(0.05)
        if _G.AutoSkill then
            K(Enum.KeyCode.Z, 0.01)
            K(Enum.KeyCode.X, 0.01)
            K(Enum.KeyCode.C, 0.01)
            K(Enum.KeyCode.V, 0.01)
        end
    end
end)

--// AUTO MINI
task.spawn(function()
    while true do
        task.wait(0.03)
        if _G.AutoMini then
            K(Enum.KeyCode.W, 0.005)
            K(Enum.KeyCode.A, 0.005)
            K(Enum.KeyCode.D, 0.005)
        end
    end
end)

--// AUTO CLICK
task.spawn(function()
    while true do
        task.wait(0.2)
        if _G.AutoClick then Click(0.02) end
    end
end)

--// NHẬP SỐ CÁ
CountBox.FocusLost:Connect(function()
    local n = tonumber(CountBox.Text)
    if n then
        n = math.clamp(math.floor(n), 1, 50)
        CountBox.Text = tostring(n)
        _G.SellTarget = n
    else
        CountBox.Text = "10"
        _G.SellTarget = 10
    end
end)

--// NÚT AUTO CÂU
BtnAuto.MouseButton1Click:Connect(function()
    _G.AutoFish=not _G.AutoFish
    if _G.AutoFish then
        BtnAuto.Text="🎣 AUTO CÂU: ON"; BtnAuto.TextColor3=C.red
        _G.AutoSkill=true; _G.AutoMini=true; _G.AutoClick=true
        BtnSkill.Text="⚔️ AUTO SKILL: ON"; BtnSkill.TextColor3=C.red
        BtnMini.Text="🎮 AUTO MINI: ON"; BtnMini.TextColor3=C.red
        BtnClick.Text="🖱️ AUTO CLICK: ON"; BtnClick.TextColor3=C.red
        if not _G.ForceUnlock then
            SaveAnchor()
            BtnLock.Text="🔒 KHÓA: ON"; BtnLock.TextColor3=C.red
        end
        Status.Text="● Đang chạy..."; Status.TextColor3=C.grn
    else
        BtnAuto.Text="🎣 AUTO CÂU: OFF"; BtnAuto.TextColor3=C.grn
        _G.AutoSkill=false; _G.AutoMini=false; _G.AutoClick=false
        BtnSkill.Text="⚔️ AUTO SKILL: OFF"; BtnSkill.TextColor3=C.grn
        BtnMini.Text="🎮 AUTO MINI: OFF"; BtnMini.TextColor3=C.grn
        BtnClick.Text="🖱️ AUTO CLICK: OFF"; BtnClick.TextColor3=C.grn
        Status.Text="● Đã tắt"; Status.TextColor3=C.dim
    end
end)

BtnSkill.MouseButton1Click:Connect(function()
    _G.AutoSkill = not _G.AutoSkill
    BtnSkill.Text = _G.AutoSkill and "⚔️ AUTO SKILL: ON" or "⚔️ AUTO SKILL: OFF"
    BtnSkill.TextColor3 = _G.AutoSkill and C.red or C.grn
end)

BtnMini.MouseButton1Click:Connect(function()
    _G.AutoMini = not _G.AutoMini
    BtnMini.Text = _G.AutoMini and "🎮 AUTO MINI: ON" or "🎮 AUTO MINI: OFF"
    BtnMini.TextColor3 = _G.AutoMini and C.red or C.grn
end)

BtnClick.MouseButton1Click:Connect(function()
    _G.AutoClick = not _G.AutoClick
    BtnClick.Text = _G.AutoClick and "🖱️ AUTO CLICK: ON" or "🖱️ AUTO CLICK: OFF"
    BtnClick.TextColor3 = _G.AutoClick and C.red or C.grn
end)

BtnLock.MouseButton1Click:Connect(function()
    if _G.LockPos then
        _G.LockPos=false; _G.AnchorPos=nil
        BtnLock.Text="🔒 KHÓA: OFF"; BtnLock.TextColor3=C.grn
    else
        SaveAnchor()
        BtnLock.Text="🔒 KHÓA: ON"; BtnLock.TextColor3=C.red
    end
end)

BtnUnlock.MouseButton1Click:Connect(function()
    _G.LockPos=false; _G.AnchorPos=nil; _G.ForceUnlock=true
    BtnLock.Text="🔒 KHÓA: OFF"; BtnLock.TextColor3=C.grn
    Status.Text="● ✅ Đã mở khóa!"; Status.TextColor3=C.cyan
    task.wait(0.5); _G.ForceUnlock=false
end)

BtnSell.MouseButton1Click:Connect(function()
    Status.Text="● Đang bán..."; Status.TextColor3=C.gold
    task.spawn(function()
        local ok,msg=SellAll()
        Status.Text="● "..msg
        Status.TextColor3=ok and C.grn or C.red
    end)
end)

BtnAutoSell.MouseButton1Click:Connect(function()
    _G.AutoSell=not _G.AutoSell
    BtnAutoSell.Text = _G.AutoSell and "💰 AUTO SELL: ON" or "💰 AUTO SELL: OFF"
    BtnAutoSell.TextColor3 = _G.AutoSell and C.red or C.gold
end)

BtnSellCount.MouseButton1Click:Connect(function()
    _G.AutoSellCount = not _G.AutoSellCount
    if _G.AutoSellCount then
        BtnSellCount.Text="🐟 AUTO SELL SỐ: ON"; BtnSellCount.TextColor3=C.red
        _G.FishCaught = 0
        Status.Text="● Đếm: 0/".._G.SellTarget; Status.TextColor3=C.cyan
    else
        BtnSellCount.Text="🐟 AUTO SELL SỐ: OFF"; BtnSellCount.TextColor3=C.gold
        Status.Text="● Đã tắt"; Status.TextColor3=C.dim
    end
end)

Close.MouseButton1Click:Connect(function()
    Main.Visible=false; Reopen.Visible=true
end)

Reopen.MouseButton1Click:Connect(function()
    Main.Visible=true; Reopen.Visible=false
end)

--// VÒNG LẶP CHÍNH
task.spawn(function()
    while true do
        task.wait(0.1)
        if _G.AutoFish then
            teleCount = 0
            
            -- Bấm ô 1 (trang bị cần)
            Status.Text = "● Trang bị cần..."
            Status.TextColor3 = C.cyan
            K(Enum.KeyCode.One, 0.1)
            task.wait(0.3)
            
            -- Thả cần
            Status.Text = "● Thả cần..."
            Status.TextColor3 = C.gold
            Click(0.5)
            task.wait(0.3)
            
            -- Đang câu
            Status.Text = "● Đang câu..."
            Status.TextColor3 = C.grn
            
            local startT = tick()
            local caught = false
            
            while _G.AutoFish and (tick() - startT < 25) do
                if teleCount >= 3 then
                    Status.Text = "● ⚠️ Tele 3 lần!"
                    Status.TextColor3 = C.red
                    break
                end
                if CheckFish() then caught = true break end
                task.wait(0.1)
            end
            
            if caught then
                _G.FishCaught = _G.FishCaught + 1
                Status.Text = "● ✅ Câu! (".._G.FishCaught.."/".._G.SellTarget..")"
                Status.TextColor3 = C.grn
                
                -- Đủ số → bán
                if _G.AutoSellCount and _G.FishCaught >= _G.SellTarget then
                    Status.Text = "● Đủ ".._G.SellTarget.." cá! Bán..."
                    Status.TextColor3 = C.gold
                    
                    local wasLocked = _G.LockPos
                    _G.LockPos = false
                    _G.ForceUnlock = true
                    task.wait(0.3)
                    
                    SellAll()
                    task.wait(1)
                    
                    _G.FishCaught = 0
                    _G.ForceUnlock = false
                    if wasLocked then SaveAnchor() end
                    
                    Status.Text = "● Đã bán! Đếm lại từ 0"
                    Status.TextColor3 = C.grn
                end
                
                task.wait(0.5)
                Click(0)
                task.wait(1.5)
            elseif teleCount >= 3 then
                Status.Text = "● 🔄 Tele 3 lần"
                Status.TextColor3 = C.gold
                task.wait(0.5)
            else
                Status.Text = "● ⏰ Hết thời gian"
                Status.TextColor3 = C.red
                task.wait(0.5)
            end
        end
    end
end)

--// LOADING
task.spawn(function()
    Tween:Create(BarFill,TweenInfo.new(1.5),{Size=UDim2.new(1,0,1,0)}):Play()
    task.wait(0.8); LoadText.Text="Đang khởi tạo..."
    task.wait(0.7); LoadText.Text="✓ Hoàn tất!"; LoadText.TextColor3=C.gold
    task.wait(0.3)
    Tween:Create(Load,TweenInfo.new(0.3),{BackgroundTransparency=1}):Play()
    for _,v in pairs(Load:GetDescendants()) do
        if v:IsA("TextLabel") then Tween:Create(v,TweenInfo.new(0.3),{TextTransparency=1}):Play()
        elseif v:IsA("Frame") then Tween:Create(v,TweenInfo.new(0.3),{BackgroundTransparency=1}):Play()
        elseif v:IsA("UIStroke") then Tween:Create(v,TweenInfo.new(0.3),{Transparency=1}):Play() end
    end
    task.wait(0.35); Load:Destroy()
    Main.Visible=true
    Main.BackgroundTransparency=1; MS.Transparency=1
    for _,v in pairs(Main:GetDescendants()) do
        if v:IsA("TextButton") then v.BackgroundTransparency=1; v.TextTransparency=1
        elseif v:IsA("TextLabel") then v.TextTransparency=1
        elseif v:IsA("Frame") then v.BackgroundTransparency=1 end
    end
    Tween:Create(Main,TweenInfo.new(0.25),{BackgroundTransparency=0}):Play()
    Tween:Create(MS,TweenInfo.new(0.25),{Transparency=0.3}):Play()
    for _,v in pairs(Main:GetDescendants()) do
        if v:IsA("TextButton") then Tween:Create(v,TweenInfo.new(0.25),{BackgroundTransparency=0,TextTransparency=0}):Play()
        elseif v:IsA("TextLabel") then Tween:Create(v,TweenInfo.new(0.25),{TextTransparency=0}):Play()
        elseif v:IsA("Frame") then Tween:Create(v,TweenInfo.new(0.25),{BackgroundTransparency=0}):Play() end
    end
end)
