# Script-master-fishing-no-key
--// BY datbeo100kgkakakaka (FULL SCRIPT)
local Players    = game:GetService("Players")
local CoreGui    = game:GetService("CoreGui")
local Tween      = game:GetService("TweenService")
local UIS        = game:GetService("UserInputService")
local P = Players.LocalPlayer

if CoreGui:FindFirstChild("DatBeoGui") then
    CoreGui.DatBeoGui:Destroy()
end

local S = Instance.new("ScreenGui")
S.Name = "DatBeoGui"
S.ResetOnSpawn = false
S.Parent = CoreGui

--// ===== MÀU SẮC =====
local COLORS = {
    bg       = Color3.fromRGB(15, 15, 20),
    bg2      = Color3.fromRGB(25, 25, 35),
    accent   = Color3.fromRGB(255, 200, 60),
    accent2  = Color3.fromRGB(0, 220, 255),
    green    = Color3.fromRGB(0, 255, 130),
    red      = Color3.fromRGB(255, 60, 80),
    text     = Color3.fromRGB(220, 220, 230),
    textDim  = Color3.fromRGB(130, 130, 145),
}

--// ===== HÀM TIỆN ÍCH =====
local function AddGradient(parent, c1, c2, rot)
    local g = Instance.new("UIGradient", parent)
    g.Color = ColorSequence.new(c1, c2)
    g.Rotation = rot or 0
end

local function AddCorner(parent, r)
    local c = Instance.new("UICorner", parent)
    c.CornerRadius = UDim.new(0, r or 8)
end

local function AddStroke(parent, color, thick, trans)
    local s = Instance.new("UIStroke", parent)
    s.Color = color or COLORS.accent
    s.Thickness = thick or 1.5
    s.Transparency = trans or 0
    return s
end

local function makeDraggable(frame)
    local dragging, dragStart, startPos
    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1
        or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = frame.Position
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)
    frame.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement
        or input.UserInputType == Enum.UserInputType.Touch) then
            local d = input.Position - dragStart
            frame.Position = UDim2.new(
                startPos.X.Scale, startPos.X.Offset + d.X,
                startPos.Y.Scale, startPos.Y.Offset + d.Y
            )
        end
    end)
end

local function CreateButton(parent, size, pos, text, c1, c2)
    local btn = Instance.new("TextButton", parent)
    btn.Size = size
    btn.Position = pos
    btn.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
    btn.TextColor3 = COLORS.text
    btn.TextSize = 12
    btn.Font = Enum.Font.GothamBold
    btn.Text = text
    btn.BorderSizePixel = 0
    btn.AutoButtonColor = false

    AddCorner(btn, 6)
    AddGradient(btn, c1 or COLORS.bg2, c2 or COLORS.bg)

    local orig = btn.BackgroundColor3
    btn.MouseEnter:Connect(function()
        Tween:Create(btn, TweenInfo.new(0.15), {
            BackgroundColor3 = Color3.fromRGB(50, 50, 65)
        }):Play()
    end)
    btn.MouseLeave:Connect(function()
        Tween:Create(btn, TweenInfo.new(0.15), {
            BackgroundColor3 = orig
        }):Play()
    end)

    return btn
end

--// ============================================================
--// KEY SYSTEM
--// ============================================================
local VALID_KEY = "haibigay"

local KeyFrame = Instance.new("Frame", S)
KeyFrame.Size = UDim2.new(0, 280, 0, 170)
KeyFrame.Position = UDim2.new(0.5, -140, 0.4, -85)
KeyFrame.BackgroundColor3 = COLORS.bg
KeyFrame.BorderSizePixel = 0
KeyFrame.Active = true
makeDraggable(KeyFrame)

AddCorner(KeyFrame, 12)
AddStroke(KeyFrame, COLORS.accent, 2)
AddGradient(KeyFrame, COLORS.bg2, COLORS.bg, 90)

local TopBar = Instance.new("Frame", KeyFrame)
TopBar.Size = UDim2.new(1, 0, 0, 45)
TopBar.BackgroundColor3 = COLORS.bg2
TopBar.BorderSizePixel = 0
AddCorner(TopBar, 12)
AddGradient(TopBar, Color3.fromRGB(40, 35, 25), Color3.fromRGB(25, 25, 35))

local KeyTitle = Instance.new("TextLabel", TopBar)
KeyTitle.Size = UDim2.new(1, 0, 1, 0)
KeyTitle.BackgroundTransparency = 1
KeyTitle.TextColor3 = COLORS.accent
KeyTitle.TextSize = 15
KeyTitle.Font = Enum.Font.GothamBold
KeyTitle.Text = "⚡ DATBEO SCRIPT ⚡"

local KeyHint = Instance.new("TextLabel", KeyFrame)
KeyHint.Size = UDim2.new(1, 0, 0, 20)
KeyHint.Position = UDim2.new(0, 0, 0, 52)
KeyHint.BackgroundTransparency = 1
KeyHint.TextColor3 = COLORS.textDim
KeyHint.TextSize = 11
KeyHint.Font = Enum.Font.Gotham
KeyHint.Text = "Nhập key để sử dụng"

local KeyBoxBorder = Instance.new("Frame", KeyFrame)
KeyBoxBorder.Size = UDim2.new(0, 240, 0, 36)
KeyBoxBorder.Position = UDim2.new(0.5, -120, 0, 78)
KeyBoxBorder.BackgroundColor3 = COLORS.bg2
KeyBoxBorder.BorderSizePixel = 0
AddCorner(KeyBoxBorder, 8)
AddStroke(KeyBoxBorder, COLORS.accent2, 1.5, 0.5)

local KeyBox = Instance.new("TextBox", KeyBoxBorder)
KeyBox.Size = UDim2.new(1, -20, 1, 0)
KeyBox.Position = UDim2.new(0, 10, 0, 0)
KeyBox.BackgroundTransparency = 1
KeyBox.TextColor3 = COLORS.accent2
KeyBox.TextSize = 13
KeyBox.Font = Enum.Font.GothamBold
KeyBox.PlaceholderText = "Nhập key..."
KeyBox.PlaceholderColor3 = COLORS.textDim
KeyBox.Text = ""
KeyBox.ClearTextOnFocus = false

local BtnKey = CreateButton(KeyFrame,
    UDim2.new(0, 240, 0, 36),
    UDim2.new(0.5, -120, 0, 122),
    "✓ XÁC NHẬN",
    Color3.fromRGB(40, 60, 50),
    Color3.fromRGB(25, 40, 35)
)
BtnKey.TextColor3 = COLORS.green

--// ===== BẢNG LOADING =====
local LoadFrame = Instance.new("Frame", S)
LoadFrame.Size = UDim2.new(0, 280, 0, 100)
LoadFrame.Position = UDim2.new(0.5, -140, 0.5, -50)
LoadFrame.BackgroundColor3 = COLORS.bg
LoadFrame.BorderSizePixel = 0
LoadFrame.Visible = false
AddCorner(LoadFrame, 12)
AddStroke(LoadFrame, COLORS.green, 2)
AddGradient(LoadFrame, COLORS.bg2, COLORS.bg, 90)

local LoadTitle = Instance.new("TextLabel", LoadFrame)
LoadTitle.Size = UDim2.new(1, 0, 0, 30)
LoadTitle.Position = UDim2.new(0, 0, 0, 12)
LoadTitle.BackgroundTransparency = 1
LoadTitle.TextColor3 = COLORS.accent
LoadTitle.TextSize = 15
LoadTitle.Font = Enum.Font.GothamBold
LoadTitle.Text = "⚡ DATBEO SCRIPT ⚡"

local LoadText = Instance.new("TextLabel", LoadFrame)
LoadText.Size = UDim2.new(1, 0, 0, 22)
LoadText.Position = UDim2.new(0, 0, 0, 42)
LoadText.BackgroundTransparency = 1
LoadText.TextColor3 = COLORS.green
LoadText.TextSize = 12
LoadText.Font = Enum.Font.Gotham
LoadText.Text = "Đang tải script..."

local BarBg = Instance.new("Frame", LoadFrame)
BarBg.Size = UDim2.new(0.85, 0, 0, 8)
BarBg.Position = UDim2.new(0.075, 0, 0, 78)
BarBg.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
BarBg.BorderSizePixel = 0
AddCorner(BarBg, 4)

local BarFill = Instance.new("Frame", BarBg)
BarFill.Size = UDim2.new(0, 0, 1, 0)
BarFill.BackgroundColor3 = COLORS.green
BarFill.BorderSizePixel = 0
AddCorner(BarFill, 4)
AddGradient(BarFill, COLORS.green, COLORS.accent2)

--// ============================================================
--// BẢNG CHÍNH
--// ============================================================
local MainFrame = Instance.new("Frame", S)
MainFrame.Size = UDim2.new(0, 240, 0, 320)
MainFrame.Position = UDim2.new(0.05, 0, 0.3, 0)
MainFrame.BackgroundColor3 = COLORS.bg
MainFrame.Active = true
MainFrame.Visible = false
MainFrame.BorderSizePixel = 0
makeDraggable(MainFrame)

AddCorner(MainFrame, 12)
local MainStroke = AddStroke(MainFrame, COLORS.accent, 1.5, 0.3)
AddGradient(MainFrame, COLORS.bg2, COLORS.bg, 90)

-- Header
local Header = Instance.new("Frame", MainFrame)
Header.Size = UDim2.new(1, 0, 0, 40)
Header.BackgroundColor3 = COLORS.bg2
Header.BorderSizePixel = 0
AddCorner(Header, 12)
AddGradient(Header, Color3.fromRGB(45, 38, 25), Color3.fromRGB(25, 25, 35))

local Title = Instance.new("TextLabel", Header)
Title.Size = UDim2.new(1, 0, 1, 0)
Title.BackgroundTransparency = 1
Title.TextColor3 = COLORS.accent
Title.TextSize = 13
Title.Font = Enum.Font.GothamBold
Title.Text = "⚡ DATBEO SCRIPT ⚡"

-- Divider
local Divider = Instance.new("Frame", MainFrame)
Divider.Size = UDim2.new(0.9, 0, 0, 1)
Divider.Position = UDim2.new(0.05, 0, 0, 42)
Divider.BackgroundColor3 = COLORS.accent
Divider.BorderSizePixel = 0
Divider.BackgroundTransparency = 0.7

-- Nút Auto Câu
local BtnAuto = CreateButton(MainFrame,
    UDim2.new(0, 216, 0, 40),
    UDim2.new(0, 12, 0, 52),
    "🎣 AUTO CÂU 1.3: OFF",
    Color3.fromRGB(35, 45, 40),
    Color3.fromRGB(25, 30, 35)
)
BtnAuto.TextColor3 = COLORS.green
BtnAuto.TextSize = 13

-- Nút Khóa Di Chuyển
local BtnLock = CreateButton(MainFrame,
    UDim2.new(0, 216, 0, 34),
    UDim2.new(0, 12, 0, 98),
    "🔒 KHÓA DI CHUYỂN: OFF",
    Color3.fromRGB(35, 45, 40),
    Color3.fromRGB(25, 30, 35)
)
BtnLock.TextColor3 = COLORS.green

-- Nút Mở Khóa Di Chuyển
local BtnUnlock = CreateButton(MainFrame,
    UDim2.new(0, 216, 0, 34),
    UDim2.new(0, 12, 0, 138),
    "🔓 MỞ KHÓA DI CHUYỂN",
    Color3.fromRGB(50, 40, 30),
    Color3.fromRGB(35, 28, 22)
)
BtnUnlock.TextColor3 = COLORS.accent

-- Nút Sell All
local BtnSell = CreateButton(MainFrame,
    UDim2.new(0, 216, 0, 34),
    UDim2.new(0, 12, 0, 178),
    "💰 SELL ALL",
    Color3.fromRGB(50, 45, 30),
    Color3.fromRGB(35, 30, 22)
)
BtnSell.TextColor3 = COLORS.accent
BtnSell.TextSize = 13

-- Nút Auto Sell
local BtnAutoSell = CreateButton(MainFrame,
    UDim2.new(0, 216, 0, 34),
    UDim2.new(0, 12, 0, 218),
    "💰 AUTO SELL: OFF",
    Color3.fromRGB(45, 40, 30),
    Color3.fromRGB(30, 28, 22)
)
BtnAutoSell.TextColor3 = COLORS.accent

-- Trạng thái
local StatusLbl = Instance.new("TextLabel", MainFrame)
StatusLbl.Size = UDim2.new(1, 0, 0, 20)
StatusLbl.Position = UDim2.new(0, 0, 0, 258)
StatusLbl.BackgroundTransparency = 1
StatusLbl.TextColor3 = COLORS.textDim
StatusLbl.TextSize = 11
StatusLbl.Font = Enum.Font.Gotham
StatusLbl.Text = "● Sẵn sàng"

-- Nút đóng
local BtnClose = Instance.new("TextButton", MainFrame)
BtnClose.Size = UDim2.new(0, 20, 0, 20)
BtnClose.Position = UDim2.new(1, -26, 0, 10)
BtnClose.BackgroundColor3 = Color3.fromRGB(50, 30, 30)
BtnClose.TextColor3 = COLORS.red
BtnClose.TextSize = 12
BtnClose.Font = Enum.Font.GothamBold
BtnClose.Text = "✕"
BtnClose.BorderSizePixel = 0
AddCorner(BtnClose, 4)

--// ===== NÚT MỞ LẠI =====
local isMinimized = false

local ReopenBtn = Instance.new("TextButton", S)
ReopenBtn.Size = UDim2.new(0, 50, 0, 50)
ReopenBtn.Position = UDim2.new(0, 20, 0.5, -25)
ReopenBtn.BackgroundColor3 = COLORS.bg2
ReopenBtn.TextColor3 = COLORS.accent
ReopenBtn.TextSize = 22
ReopenBtn.Font = Enum.Font.GothamBold
ReopenBtn.Text = "⚡"
ReopenBtn.BorderSizePixel = 0
ReopenBtn.Visible = false
ReopenBtn.Active = true

AddCorner(ReopenBtn, 25)
AddStroke(ReopenBtn, COLORS.accent, 2)
AddGradient(ReopenBtn, Color3.fromRGB(45, 38, 25), COLORS.bg2, 90)
makeDraggable(ReopenBtn)

ReopenBtn.MouseEnter:Connect(function()
    Tween:Create(ReopenBtn, TweenInfo.new(0.15), {
        Size = UDim2.new(0, 55, 0, 55),
        Position = UDim2.new(0, 18, 0.5, -27)
    }):Play()
end)
ReopenBtn.MouseLeave:Connect(function()
    Tween:Create(ReopenBtn, TweenInfo.new(0.15), {
        Size = UDim2.new(0, 50, 0, 50),
        Position = UDim2.new(0, 20, 0.5, -25)
    }):Play()
end)

--// ===== BIẾN =====
_G.AutoFish    = false
_G.LockPos     = false
_G.AnchorPos   = nil
_G.ForceUnlock = false
_G.AutoSell    = false

--// ===== INPUT =====
local function K(key)
    pcall(function()
        keypress(key)
        task.wait(0.05)
        keyrelease(key)
    end)
end

local function LeftClick(hold)
    pcall(function()
        mouse1press()
        task.wait(hold and hold > 0 and hold or 0.05)
        mouse1release()
    end)
end

--// ===== CHECK FISH CAUGHT =====
local function CheckFish()
    local function scan(root)
        for _, g in pairs(root:GetDescendants()) do
            if g:IsA("TextLabel") or g:IsA("TextButton") then
                local txt = string.lower(tostring(g.Text or ""))
                if string.find(txt, "fish caught") then
                    return true
                end
            end
        end
        return false
    end

    if P:FindFirstChild("PlayerGui") and scan(P.PlayerGui) then return true end
    if scan(CoreGui) then return true end
    if scan(workspace) then return true end
    return false
end

--// ===== CHECK TÚI ĐẦY =====
local function IsInventoryFull()
    local pg = P:FindFirstChild("PlayerGui")
    if not pg then return false end
    for _, g in pairs(pg:GetDescendants()) do
        if g:IsA("TextLabel") or g:IsA("TextButton") then
            local txt = string.lower(tostring(g.Text or ""))
            if txt:find("full") or txt:find("đầy") 
            or txt:find("inventory is full") then
                return true
            end
        end
    end
    return false
end

--// ===== TÌM NPC BÁN CÁ =====
local function FindSellNPC()
    local char = P.Character
    if not char then return nil end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return nil end
    
    local myPos = hrp.Position
    local npc = nil
    local shortest = math.huge
    
    for _, g in pairs(workspace:GetDescendants()) do
        if g:IsA("Model") or g:IsA("BasePart") then
            local name = g.Name:lower()
            if name:find("fish") or name:find("sell") 
            or name:find("merchant") or name:find("shop")
            or name:find("trader") or name:find("market") then
                local part = g:IsA("BasePart") and g 
                    or g:FindFirstChild("HumanoidRootPart") 
                    or g:FindFirstChildWhichIsA("BasePart")
                if part then
                    local dist = (part.Position - myPos).Magnitude
                    if dist < shortest then
                        shortest = dist
                        npc = part
                    end
                end
            end
        end
    end
    return npc
end

--// ===== CLICK NÚT SELL TRONG GUI =====
local function ClickSellButton()
    local pg = P:FindFirstChild("PlayerGui")
    if not pg then return false end
    
    local clicked = false
    for _, g in pairs(pg:GetDescendants()) do
        if (g:IsA("TextButton") or g:IsA("ImageButton")) and g.Visible then
            local txt = (g.Text or ""):lower()
            local n = g.Name:lower()
            if txt:find("sell") or txt:find("bán") 
            or txt:find("confirm") or txt:find("xác nhận")
            or txt:find("tất cả") or txt:find("all")
            or n:find("sell") or n:find("confirm") then
                g:Activate()
                clicked = true
                task.wait(0.2)
            end
        end
    end
    return clicked
end

--// ===== SELL ALL =====
local function SellAllNow()
    local char = P.Character
    if not char then return false, "Không có nhân vật" end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return false, "Không có HRP" end
    
    local oldCF = hrp.CFrame
    local npc = FindSellNPC()
    if not npc then return false, "Không tìm thấy NPC" end
    
    hrp.CFrame = CFrame.new(npc.Position + Vector3.new(0, 3, 0))
    task.wait(0.5)
    K(Enum.KeyCode.E)
    task.wait(0.8)
    ClickSellButton()
    task.wait(0.4)
    ClickSellButton()
    task.wait(0.4)
    K(Enum.KeyCode.E)
    task.wait(0.3)
    hrp.CFrame = oldCF
    
    return true, "Đã bán tất cả"
end

--// ===== NEO VỊ TRÍ =====
local function SaveAnchor()
    local c = P.Character
    if c and c:FindFirstChild("HumanoidRootPart") then
        _G.AnchorPos = c.HumanoidRootPart.Position
        _G.LockPos = true
    end
end

--// ===== KHÓA DI CHUYỂN =====
task.spawn(function()
    while true do
        task.wait(0.2)
        if not _G.ForceUnlock and _G.LockPos and _G.AnchorPos then
            local c = P.Character
            if c and c:FindFirstChild("HumanoidRootPart") then
                local cur = c.HumanoidRootPart.Position
                if (cur - _G.AnchorPos).Magnitude > 3 then
                    c.HumanoidRootPart.CFrame = CFrame.new(_G.AnchorPos)
                end
            end
        end
    end
end)

--// ===== NÚT AUTO CÂU =====
BtnAuto.MouseButton1Click:Connect(function()
    _G.AutoFish = not _G.AutoFish
    if _G.AutoFish then
        BtnAuto.Text = "🎣 AUTO CÂU 1.3: ON"
        BtnAuto.TextColor3 = COLORS.red
        if not _G.ForceUnlock then
            SaveAnchor()
            BtnLock.Text = "🔒 KHÓA DI CHUYỂN: ON"
            BtnLock.TextColor3 = COLORS.red
        end
        StatusLbl.Text = "● Đang chạy..."
        StatusLbl.TextColor3 = COLORS.green
    else
        BtnAuto.Text = "🎣 AUTO CÂU 1.3: OFF"
        BtnAuto.TextColor3 = COLORS.green
        StatusLbl.Text = "● Đã tắt"
        StatusLbl.TextColor3 = COLORS.textDim
    end
end)

--// ===== NÚT KHÓA DI CHUYỂN =====
BtnLock.MouseButton1Click:Connect(function()
    if _G.LockPos then
        _G.LockPos = false
        _G.AnchorPos = nil
        BtnLock.Text = "🔒 KHÓA DI CHUYỂN: OFF"
        BtnLock.TextColor3 = COLORS.green
        StatusLbl.Text = "● Đã tắt khóa"
    else
        SaveAnchor()
        BtnLock.Text = "🔒 KHÓA DI CHUYỂN: ON"
        BtnLock.TextColor3 = COLORS.red
        StatusLbl.Text = "● Đã khóa vị trí"
    end
end)

--// ===== NÚT MỞ KHÓA =====
BtnUnlock.MouseButton1Click:Connect(function()
    _G.LockPos = false
    _G.AnchorPos = nil
    _G.ForceUnlock = true
    BtnLock.Text = "🔒 KHÓA DI CHUYỂN: OFF"
    BtnLock.TextColor3 = COLORS.green
    StatusLbl.Text = "● ✅ Đã mở khóa!"
    StatusLbl.TextColor3 = COLORS.accent2
    task.wait(0.5)
    _G.ForceUnlock = false
end)

--// ===== NÚT SELL ALL =====
BtnSell.MouseButton1Click:Connect(function()
    StatusLbl.Text = "● Đang bán..."
    StatusLbl.TextColor3 = COLORS.accent
    task.spawn(function()
        local ok, msg = SellAllNow()
        StatusLbl.Text = "● " .. msg
        StatusLbl.TextColor3 = ok and COLORS.green or COLORS.red
    end)
end)

--// ===== NÚT AUTO SELL =====
BtnAutoSell.MouseButton1Click:Connect(function()
    _G.AutoSell = not _G.AutoSell
    if _G.AutoSell then
        BtnAutoSell.Text = "💰 AUTO SELL: ON"
        BtnAutoSell.TextColor3 = COLORS.red
        StatusLbl.Text = "● Chờ túi đầy..."
        StatusLbl.TextColor3 = COLORS.accent2
        
        task.spawn(function()
            while _G.AutoSell do
                if IsInventoryFull() then
                    StatusLbl.Text = "● Túi đầy, đang bán..."
                    StatusLbl.TextColor3 = COLORS.accent
                    local ok, msg = SellAllNow()
                    StatusLbl.Text = "● " .. msg
                    StatusLbl.TextColor3 = ok and COLORS.green or COLORS.red
                    task.wait(2)
                else
                    StatusLbl.Text = "● Chờ túi đầy..."
                    StatusLbl.TextColor3 = COLORS.textDim
                end
                task.wait(1)
            end
        end)
    else
        BtnAutoSell.Text = "💰 AUTO SELL: OFF"
        BtnAutoSell.TextColor3 = COLORS.accent
        StatusLbl.Text = "● Đã tắt auto sell"
        StatusLbl.TextColor3 = COLORS.textDim
    end
end)

--// ===== NÚT ĐÓNG =====
BtnClose.MouseButton1Click:Connect(function()
    isMinimized = true
    ReopenBtn.Visible = true
    Tween:Create(MainFrame, TweenInfo.new(0.2), {BackgroundTransparency = 1}):Play()
    Tween:Create(MainStroke, TweenInfo.new(0.2), {Transparency = 1}):Play()
    for _, v in pairs(MainFrame:GetDescendants()) do
        if v:IsA("TextButton") then
            Tween:Create(v, TweenInfo.new(0.2), {BackgroundTransparency = 1, TextTransparency = 1}):Play()
        elseif v:IsA("TextLabel") then
            Tween:Create(v, TweenInfo.new(0.2), {TextTransparency = 1}):Play()
        elseif v:IsA("Frame") then
            Tween:Create(v, TweenInfo.new(0.2), {BackgroundTransparency = 1}):Play()
        end
    end
    task.wait(0.25)
    if isMinimized then MainFrame.Visible = false end
end)

ReopenBtn.MouseButton1Click:Connect(function()
    isMinimized = false
    MainFrame.Visible = true
    ReopenBtn.Visible = false
    
    MainFrame.BackgroundTransparency = 1
    MainStroke.Transparency = 1
    for _, v in pairs(MainFrame:GetDescendants()) do
        if v:IsA("TextButton") then
            v.BackgroundTransparency = 1
            v.TextTransparency = 1
        elseif v:IsA("TextLabel") then
            v.TextTransparency = 1
        elseif v:IsA("Frame") then
            v.BackgroundTransparency = 1
        end
    end
    
    Tween:Create(MainFrame, TweenInfo.new(0.25), {BackgroundTransparency = 0}):Play()
    Tween:Create(MainStroke, TweenInfo.new(0.25), {Transparency = 0}):Play()
    for _, v in pairs(MainFrame:GetDescendants()) do
        if v:IsA("TextButton") then
            Tween:Create(v, TweenInfo.new(0.25), {BackgroundTransparency = 0, TextTransparency = 0}):Play()
        elseif v:IsA("TextLabel") then
            Tween:Create(v, TweenInfo.new(0.25), {TextTransparency = 0}):Play()
        elseif v:IsA("Frame") then
            Tween:Create(v, TweenInfo.new(0.25), {BackgroundTransparency = 0}):Play()
        end
    end
end)

--// ===== CHU TRÌNH AUTO CÂU =====
task.spawn(function()
    while true do
        if _G.AutoFish then
            StatusLbl.Text = "● P1: Thả cần..."
            LeftClick(1)
            task.wait(4)

            if _G.AutoFish then
                StatusLbl.Text = "● P2: Đang câu..."
                local startTime = tick()
                local caught = false

                task.spawn(function()
                    while _G.AutoFish and not caught do
                        LeftClick(0)
                        task.wait(0.2)
                    end
                end)

                task.spawn(function()
                    local keys = {Enum.KeyCode.Z, Enum.KeyCode.X, Enum.KeyCode.V, Enum.KeyCode.C}
                    while _G.AutoFish and not caught do
                        for _, k in ipairs(keys) do
                            if not _G.AutoFish or caught then break end
                            K(k)
                            task.wait(0.05)
                        end
                    end
                end)

                task.spawn(function()
                    local keys = {Enum.KeyCode.W, Enum.KeyCode.A, Enum.KeyCode.D}
                    while _G.AutoFish and not caught do
                        for _, k in ipairs(keys) do
                            if not _G.AutoFish or caught then break end
                            K(k)
                            task.wait(0.1)
                        end
                    end
                end)

                while _G.AutoFish and (tick() - startTime < 30) do
                    if CheckFish() then
                        caught = true
                        break
                    end
                    task.wait(0.1)
                end

                if caught then
                    StatusLbl.Text = "● ✅ Đã câu được!"
                    StatusLbl.TextColor3 = COLORS.green
                    task.wait(0.3)
                    LeftClick(0)
                    task.wait(1.5)
                else
                    StatusLbl.Text = "● ⏰ Hết thời gian"
                    StatusLbl.TextColor3 = COLORS.red
                    task.wait(0.5)
                end
            end
            task.wait(0.5)
        else
            task.wait(0.2)
        end
    end
end)

--// ===== XỬ LÝ KEY =====
local keyPassed = false

local function OnKeyCorrect()
    if keyPassed then return end
    keyPassed = true

    KeyFrame:Destroy()
    LoadFrame.Visible = true

    task.spawn(function()
        local tween = Tween:Create(BarFill, TweenInfo.new(1.8, Enum.EasingStyle.Quad), {
            Size = UDim2.new(1, 0, 1, 0)
        })
        tween:Play()

        task.wait(0.9)
        LoadText.Text = "Đang khởi tạo..."

        task.wait(0.9)
        LoadText.Text = "✓ Hoàn tất!"
        LoadText.TextColor3 = COLORS.accent

        task.wait(0.4)

        Tween:Create(LoadFrame, TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
        Tween:Create(LoadTitle, TweenInfo.new(0.3), {TextTransparency = 1}):Play()
        Tween:Create(LoadText,  TweenInfo.new(0.3), {TextTransparency = 1}):Play()
        Tween:Create(BarBg,     TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
        Tween:Create(BarFill,   TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
        Tween:Create(LoadStroke,TweenInfo.new(0.3), {Transparency = 1}):Play()
        task.wait(0.35)
        LoadFrame:Destroy()

        MainFrame.Visible = true
        MainFrame.BackgroundTransparency = 1
        MainStroke.Transparency = 1
        for _, v in pairs(MainFrame:GetDescendants()) do
            if v:IsA("TextButton") then
                v.BackgroundTransparency = 1
                v.TextTransparency = 1
            elseif v:IsA("TextLabel") then
                v.TextTransparency = 1
            elseif v:IsA("Frame") then
                v.BackgroundTransparency = 1
            end
        end

        Tween:Create(MainFrame, TweenInfo.new(0.25), {BackgroundTransparency = 0}):Play()
        Tween:Create(MainStroke, TweenInfo.new(0.25), {Transparency = 0}):Play()
        for _, v in pairs(MainFrame:GetDescendants()) do
            if v:IsA("TextButton") then
                Tween:Create(v, TweenInfo.new(0.25), {BackgroundTransparency = 0, TextTransparency = 0}):Play()
            elseif v:IsA("TextLabel") then
                Tween:Create(v, TweenInfo.new(0.25), {TextTransparency = 0}):Play()
            elseif v:IsA("Frame") then
                Tween:Create(v, TweenInfo.new(0.25), {BackgroundTransparency = 0}):Play()
            end
        end
    end)
end

local function OnKey
