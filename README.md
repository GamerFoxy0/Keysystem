# SentinelUI Key System v1.00

---

| Field | Type | Description |
|-------|------|-------------|
| **GUIAnimations** | boolean | Toggles UI tween animations. |
| **SecureMode** | boolean | Prevents bypassing loggers anti-spy (work in progress). |
| **DebugMode** | boolean | Toggles debug mode prints everything in console. |
| **MainTitle** | string | title of key system. |
| **MainDesc** | string | description of key system. |
| **KeyLink** | string | URL copied when the user clicks "Get Key". |
| **DiscordLink** | string | URL copied when the user clicks "discord" (only works if premium is enabled). |
| **Directory** | string (path) | directory controlls custom names for keys that save. |
| **Keyless** | boolean | If true, bypasses key verification. (cant use with premium mode) |
| **Premium** | boolean | If true, uses discord link instead of get key button. (cant use with keyless mode) |
| **MainLoader** | function or nil | Function executed after successful login. |

---

## Colors (Color3)

Dim = Color3.fromRGB(5, 5, 5)
LoaderBg = Color3.fromRGB(15, 15, 20)
ContentBg = Color3.fromRGB(0, 0, 0)
GetKeyBg = Color3.fromRGB(20, 20, 20)

StrokeDark = Color3.fromRGB(23, 20, 33)
StrokeLight = Color3.fromRGB(29, 29, 29)
StrokeAccent = Color3.fromRGB(113, 56, 255)
StrokeSettings = Color3.fromRGB(33, 33, 43)
StrokeSettingsEnabled = Color3.fromRGB(49, 45, 67)
UpdateLine = Color3.fromRGB(52, 52, 52)

TextWhite = Color3.fromRGB(255, 255, 255)
TextDim = Color3.fromRGB(220, 220, 220)
TextPlaceholder = Color3.fromRGB(68, 63, 79)

ButtonStatic = Color3.fromRGB(47, 47, 47)
InputBg = Color3.fromRGB(15, 15, 15)
InputBgVerify = Color3.fromRGB(94, 94, 94)

Primary = Color3.fromRGB(61, 55, 125)
AccentGradient1 = Color3.fromRGB(89, 67, 231)
AccentGradient2 = Color3.fromRGB(145, 99, 240)

IconNormal = Color3.fromRGB(203, 187, 255)
IconActive = Color3.fromRGB(241, 231, 255)
IconDim = Color3.fromRGB(169, 161, 255)

Success = Color3.fromRGB(83, 156, 70)
SuccessBg = Color3.fromRGB(10, 20, 8)
Fail = Color3.fromRGB(156, 63, 99)
FailBg = Color3.fromRGB(20, 9, 9)

SettingsToggleDisabled = Color3.fromRGB(54, 52, 60)
SettingsToggleEnabled = Color3.fromRGB(124, 58, 237)

NotificationBg = Color3.fromRGB(23, 23, 31)
NotificationText = Color3.fromRGB(180, 190, 255)
InitializeGradient = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(89, 67, 231)), ColorSequenceKeypoint.new(0.12, Color3.fromRGB(89, 67, 231)), ColorSequenceKeypoint.new(0.14, Color3.fromRGB(145, 99, 240)), ColorSequenceKeypoint.new(0.52, Color3.fromRGB(145, 99, 240)), ColorSequenceKeypoint.new(0.89, Color3.fromRGB(145, 99, 240)), ColorSequenceKeypoint.new(0.89, Color3.fromRGB(89, 67, 231)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(89, 67, 231))}
TopbarGradient =  ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(15, 15, 20)), ColorSequenceKeypoint.new(0.50, Color3.fromRGB(20, 20, 27)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(15, 15, 20))}

---

## Fonts

Main = Font.new("rbxasset://fonts/families/Arimo.json", Enum.FontWeight.Bold, Enum.FontStyle.Normal)
Main2 = Enum.Font.Arimo
Header = Enum.Font.GothamBold
SubHeader = Enum.Font.GothamMedium
Simple = Enum.Font.SourceSans


---

## Assets

--Images

Logo = {ID='rbxassetid://86119635566201',Size=UDim2.new(0, 95, 0, 95)}
other images cant be changed.

---

## Settings

CornerRadius = UDim.new(0, 8)
PillRadius = UDim.new(1, 0)
BackgroundAnim = true
AnimSpeed = 0.8
AnimationColor = Color3.fromRGB(61, 55, 125)
AnimationTransparency = 0.7
AnimStyle = Enum.EasingStyle.Exponential

Custom = {
Remember = true // default values on first launch
BackgroundTransparent = true // default values on first launch
}

---

## Updates

Updates = {
[1] = {
Version = "v0.4.0"
Date = "04.12.2024"
Updates = {
"tuff fire latest update",
"latest updates get more highlight",
}
}
}

---

## Notify

SentinelUI.Notify(--creates a notification (string)
Title = "Notification" (string) 
Description = "content" (string) 
Duration = 5 // Seconds
Type = "info" // "success" | "warn" | "alert"

---

# EXAMPLE SCRIPT

```lua
local SentinelUI = loadstring(game:HttpGet("https://sentinel1.vercel.app/get/Keysystem.lua"))()
local AuthorizeToken = crypt.hash(tick()..tostring(math.random()), "sha256")-- This generates a unique key to prevent key bypassing. Do not modify.

-- Customize the look and feel of your key system here.
SentinelUI.Keys.MainTitle    = "Junke" -- The title
SentinelUI.Keys.MainDesc     = "Please enter your key to continue" -- The subtitle
SentinelUI.Keys.Directory    = "KeyHub" -- file name where the key saves (Change this!!!!!!!111)
SentinelUI.Keys.Assets.Logo  = {ID='rbxassetid://0',Size=UDim2.new(0, 150, 0, 150)} -- Your logo Image ID and Image Size

-- Everything inside this function runs ONLY after the user enters the valid key.
local function OnKeyVerified()
    print("Key authorized! Loading main script")
    
    -- Put your actual script here
end

-- This shows your users what is new in the latest version.
table.insert(SentinelUI.Keys.Updates, 1, {
    Version = "v0.5.0",
    Date    = "09.12.2025",
    Updates = { 
        "tuff", 
        "tuff2", 
        "tuff3" 
    }
})

SentinelUI.Initialize({
    KeyLink = "https://linkvertise.com/link", -- Where users click get the key
    Token   = AuthorizeToken, -- Security token
    MainLoader = OnKeyVerified, -- Function to run on success
    --Keyless true, --keyless mode
    --Premium true, --remvoes get key button and puts discord link
    Function = function(userInput) 
        -- This is where you check the key. 
        if userInput == "example_verify" then
            SentinelUI.Authorize(AuthorizeToken) -- Success
        else
            SentinelUI.Fail() -- Wrong Key
        end
    end
})

-- You can add custom settings
SentinelUI.AddSettings({
    Title = "Auto-Load Script",
    Desc  = "Automatically skip the key screen if a valid key is saved.",
    Default = true,
    Function = function(state)
        print("Auto-Load is now:", state)
    end
})

if queue_on_teleport then
    queue_on_teleport([[
        if getgenv().SentinelKeySystem == true then return end

        --key system loadstring here in order to auto execute when joining places
    ]])
end
