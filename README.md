--[=[
    Elisium UI Library - Usage Example

    Replace the GitHub URL with your own repository URL.
    The library file itself should contain only the library and end with:
        return Library
]=]

local Library = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY/main/Elisium.lua"
))()

local Window = Library:CreateWindow({
    Title = "My Script",
    Center = true,
    AutoShow = true,
    Resizable = true,
    Draggable = true,
    Size = UDim2.fromOffset(820, 600),
})

local Tabs = {
    Main = Window:AddTab("Main"),
    Visuals = Window:AddTab("Visuals"),
    Settings = Window:AddTab("Settings"),
}

-- Main tab
local General = Tabs.Main:AddLeftGroupbox("General")
local Options = Tabs.Main:AddRightGroupbox("Options")

General:AddLabel("Welcome to Elisium")
General:AddDivider()
General:AddLabel("This is a basic usage example.", true)

General:AddToggle("example_enabled", {
    Text = "Enabled",
    Default = true,
    Callback = function(Value)
        print("Enabled:", Value)
    end,
}):AddKeyPicker("example_enabled_key", {
    Default = "F",
    Mode = "Toggle",
    SyncToggleState = true,
})

General:AddSlider("example_slider", {
    Text = "Amount",
    Default = 50,
    Min = 0,
    Max = 100,
    Rounding = 0,
    Suffix = "%",
    Callback = function(Value)
        print("Amount:", Value)
    end,
})

General:AddDropdown("example_mode", {
    Text = "Mode",
    Values = { "Default", "Balanced", "Advanced" },
    Default = "Balanced",
    Callback = function(Value)
        print("Mode:", Value)
    end,
})

General:AddInput("example_text", {
    Text = "Name",
    Default = "",
    Placeholder = "Type something...",
    Callback = function(Value)
        print("Name:", Value)
    end,
})

Options:AddToggle("example_color_enabled", {
    Text = "Custom color",
    Default = false,
}):AddColorPicker("example_color", {
    Default = Library.AccentColor,
    Title = "Example color",
    Callback = function(Color)
        print("Color:", Color)
    end,
})

Options:AddButton("Test notification", function()
    Library:Notify("Hello from Elisium!", 3)
end)

Options:AddButton("Test success notification", function()
    if Library.NotifySuccess then
        Library:NotifySuccess("Everything worked.", 3, {
            Title = "Success",
        })
    else
        Library:Notify("Everything worked.", 3)
    end
end)

-- Visuals tab
local Visuals = Tabs.Visuals:AddLeftGroupbox("Visuals")

Visuals:AddToggle("visuals_enabled", {
    Text = "Visuals",
    Default = false,
})

Visuals:AddSlider("visuals_range", {
    Text = "Range",
    Default = 250,
    Min = 50,
    Max = 1000,
    Rounding = 0,
    Suffix = " studs",
})

Visuals:AddDropdown("visuals_style", {
    Text = "Style",
    Values = { "Outline", "Solid", "Minimal" },
    Default = "Outline",
})

-- Settings tab
local Settings = Tabs.Settings:AddLeftGroupbox("Interface")

Settings:AddButton("Center window", function()
    if Library.CenterWindow then
        Library:CenterWindow()
    end
end)

Settings:AddButton("Toggle menu", function()
    Library:Toggle()
end)

Settings:AddButton("Test tooltip", function()
    Library:Notify("Hover controls to see their tooltips.", 3)
end)

-- Example of the public control API.
task.delay(1, function()
    local Toggle = Library:GetControl("example_enabled")
    if Toggle and Toggle.GetValue then
        print("Current enabled state:", Toggle:GetValue())
    end
end)
