-- Tải thư viện UI Redz V2
local Redz = loadstring(game:HttpGet("https://raw.githubusercontent.com/daucobonhi/Ui-Redz-V2/refs/heads/main/UiREDzV2.lua"))()

-- Cấu hình Cửa sổ chính và Hệ thống Key
local Window = Redz:MakeWindow({
    Hub = {
        Title = "KHOA - ANTI-CHEAT TESTER",
        Animation = "hub"
    },
    Key = {
        KeySystem = true,
        Title = "Xác thực hệ thống",
        Description = "Nhập Key để bắt đầu bài test bảo mật",
        Keys = {"thục đạo sơn"}, -- Key của bạn
        CorrectKey = "Đang khởi chạy...",
        Incorrectkey = "Sai Key rồi!",
        CopyKeyLink = "Đã sao chép liên kết lấy Key"
    }
})

-- Tạo Tab chính để chứa các nút Test
local MainTab = Redz:MakeTab({Name = "Stress Test"})

------- CÁC CHỨC NĂNG TEST BIẾN THÀNH NÚT BẤM -------

-- 1. Test Câu cá ngay lập tức
Redz:AddButton(MainTab, {
    Name = "TEST: Instant Fish (Câu ngay)",
    Callback = function()
        local char = game.Players.LocalPlayer.Character
        local tool = char and char:FindFirstChild("C\225\186\167n C\195\162u")
        if tool then
            local args = {
                tool:WaitForChild("Handle"),
                tool:WaitForChild("Fish"):WaitForChild("DoneFishEvent"),
                tool:WaitForChild("Fish"):WaitForChild("StunBackpackEvent")
            }
            game:GetService("ReplicatedStorage").Event.FishEvent:FireServer(unpack(args))
            print(">>> Đã gửi yêu cầu kết thúc câu cá lập tức.")
        else
            warn("Vui lòng cầm Cần Câu trên tay!")
        end
    end
})

-- 2. Test Spam kỹ năng Thái Cực Cửu Cung
Redz:AddButton(MainTab, {
    Name = "SPAM: Thai Cuc Cuu Cung (30x)",
    Callback = function()
        local char = game.Players.LocalPlayer.Character
        local tool = char and char:FindFirstChild("C\225\186\167n C\195\162u")
        local hook = tool and tool:FindFirstChild("Handle") and tool.Handle:FindFirstChild("Hook")
        
        if hook then
            print(">>> Bắt đầu Spam 30 lần chiêu thức...")
            for i = 1, 30 do
                task.spawn(function()
                    game:GetService("ReplicatedStorage").Event.SkillEvent:FireServer("Thai Cuc Cuu Cung", hook)
                end)
            end
        else
            warn("Không tìm thấy Hook để spam chiêu!")
        end
    end
})

-- 3. Test Bán cá từ xa
Redz:AddButton(MainTab, {
    Name = "TEST: Remote Sell (Bán xa)",
    Callback = function()
        game:GetService("ReplicatedStorage").Event.SellFishEvent:FireServer()
        print(">>> Đã gửi lệnh bán cá từ vị trí hiện tại.")
    end
})

-- Nút thu gọn Menu (Tùy chọn)
Redz:MinimizeButton({
    Image = "rbxassetid://96735549590745",
    Size = {50, 50},
    Color = Color3.fromRGB(255, 0, 0),
    Corner = true
})

