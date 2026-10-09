--// BAS HUB - CLOVER SEAS UI

if game.PlaceId ~= 117344689755739 then
    return
end

local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local StarterGui = game:GetService("StarterGui")
local StatsService = game:GetService("Stats")
local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

local C = {
    BG = Color3.fromRGB(9, 9, 9),
    Panel = Color3.fromRGB(17, 17, 17),
    Item = Color3.fromRGB(25, 25, 25),
    White = Color3.fromRGB(245, 245, 245),
    Gray = Color3.fromRGB(145, 145, 145),
    Green = Color3.fromRGB(65, 190, 115),
    Red = Color3.fromRGB(190, 65, 65),
    Border = Color3.fromRGB(55, 55, 55),
}

local Language = "en"
local LightMode = false
local CurrentTab = "Main"
local ToggleStates = {}
local ToggleRefresh = {}
local Pages = {}
local TabButtons = {}
local Dropdowns = {}
local ApplyTheme

-- Funções reais ligadas aos interruptores (Features[NomeDoToggle] = function(ligado))
local Features = {}
local Connections = {}
local SavedCFrame

local Settings = {
    Speed = 50, -- velocidade do Speed Boost
    Jump = 100, -- força do Jump Boost
}

-- Coordenadas para o teleporte (preencha com as posições reais do jogo).
-- Exemplo: ["Retro Island"] = Vector3.new(120, 50, -340),
local IslandPositions = {
}

local BossPositions = {
}
-------------------------------------------------------------------

local T = {
    en = {
        subtitle = "Clover Seas",
        Main = "🏠 Main",
        Farm = "⚔ Farm",
        Players = "☺ Players",
        Teleport = "🌀 Teleport",
        Settings = "⚙ Configurations",

        quick = "QUICK FEATURES",
        farming = "FARMING",
        visuals = "PLAYER VISUALS",
        character = "CHARACTER",
        islands = "ISLAND TELEPORT",
        bosses = "BOSS TELEPORT",
        playerTeleport = "PLAYER TELEPORT",
        location = "LOCATION",
        appearance = "APPEARANCE",
        other = "OTHER SETTINGS",

        AutoFarm = "Auto Farm",
        AutoQuest = "Auto Quest",
        AutoCollect = "Auto Collect",
        AutoChest = "Auto Chest",
        AutoBoss = "Auto Boss",
        AutoRollGrimoire = "Auto Roll Grimoire",
        AutoStoreItems = "Auto Store Items",
        AutoEquip = "Auto Equip",
        AutoMana = "Auto Mana",

        FarmMobs = "Farm Mobs",
        FarmLevel = "Farm Level",
        FarmMoney = "Farm Money",
        AutoAcceptQuest = "Auto Accept Quest",
        AutoCompleteQuest = "Auto Complete Quest",

        HighlightPlayer = "Highlight Player",
        ChestHighlight = "Chest Highlight",
        NPCHighlight = "NPC Highlight",
        BossHighlight = "Boss Highlight",
        PlayerESP = "Player ESP",
        ChestESP = "Chest ESP",
        ShowPlayerNames = "Show Player Names",
        ShowDistance = "Show Distance",
        ShowHealth = "Show Health",
        ShowLevel = "Show Player Level",
        SpeedBoost = "Speed Boost",
        JumpBoost = "Jump Boost",
        NoClip = "No Clip",
        InfiniteJump = "Infinite Jump",

        TeleportIsland = "Select Island",
        TeleportBoss = "Select Boss",
        TeleportPlayer = "Select Player",
        SaveLocation = "Save Location",
        ReturnLocation = "Return to Saved Location",

        LightMode = "Light Mode",
        CompactMode = "Compact Mode",
        ShowNotifications = "Notifications",
        HideUI = "Hide UI",
        ShowFPS = "Show FPS",
        ShowPing = "Show Ping",
        Reset = "Reset Visual Toggles",
        Language = "Language",
        Select = "Select",
        Selected = "Selected",
        Saved = "Location saved",
        Returned = "Returned to saved location",
        NoSaved = "No saved location yet",
        NoCoords = "Coordinates not set yet",
        NoTarget = "Player not available",
        TeleportedTo = "Teleported to",
        NoPlayers = "No other players in this server",
        Close = "Close",
    },

    pt = {
        subtitle = "Clover Seas",
        Main = "🏠 Início",
        Farm = "⚔ Farm",
        Players = "☺ Jogadores",
        Teleport = "🌀 Teleporte",
        Settings = "⚙ Configurações",

        quick = "FUNÇÕES PRINCIPAIS",
        farming = "FARM",
        visuals = "VISUAL DOS JOGADORES",
        character = "PERSONAGEM",
        islands = "TELEPORTE DE ILHAS",
        bosses = "TELEPORTE DE BOSS",
        playerTeleport = "TELEPORTE DE JOGADOR",
        location = "LOCALIZAÇÃO",
        appearance = "APARÊNCIA",
        other = "OUTRAS CONFIGURAÇÕES",

        AutoFarm = "Farm Automático",
        AutoQuest = "Missão Automática",
        AutoCollect = "Coleta Automática",
        AutoChest = "Baús Automáticos",
        AutoBoss = "Boss Automático",
        AutoRollGrimoire = "Girar Grimório",
        AutoStoreItems = "Guardar Itens",
        AutoEquip = "Equipar Automaticamente",
        AutoMana = "Mana Automática",

        FarmMobs = "Farmar Inimigos",
        FarmLevel = "Farmar Nível",
        FarmMoney = "Farmar Dinheiro",
        AutoAcceptQuest = "Aceitar Missão",
        AutoCompleteQuest = "Concluir Missão",

        HighlightPlayer = "Destacar Jogadores",
        ChestHighlight = "Destacar Baús",
        NPCHighlight = "Destacar NPCs",
        BossHighlight = "Destacar Bosses",
        PlayerESP = "ESP de Jogadores",
        ChestESP = "ESP de Baús",
        ShowPlayerNames = "Mostrar Nomes",
        ShowDistance = "Mostrar Distância",
        ShowHealth = "Mostrar Vida",
        ShowLevel = "Mostrar Nível",
        SpeedBoost = "Aumentar Velocidade",
        JumpBoost = "Aumentar Pulo",
        NoClip = "Atravessar Objetos",
        InfiniteJump = "Pulo Infinito",

        TeleportIsland = "Selecionar Ilha",
        TeleportBoss = "Selecionar Boss",
        TeleportPlayer = "Selecionar Jogador",
        SaveLocation = "Salvar Localização",
        ReturnLocation = "Voltar à Localização Salva",

        LightMode = "Modo Claro",
        CompactMode = "Modo Compacto",
        ShowNotifications = "Notificações",
        HideUI = "Esconder Interface",
        ShowFPS = "Mostrar FPS",
        ShowPing = "Mostrar Ping",
        Reset = "Resetar Interruptores",
        Language = "Idioma",
        Select = "Selecionar",
        Selected = "Selecionado",
        Saved = "Localização salva",
        Returned = "Voltou à localização salva",
        NoSaved = "Nenhuma localização salva",
        NoCoords = "Coordenadas ainda não definidas",
        NoTarget = "Jogador indisponível",
        TeleportedTo = "Teleportado para",
        NoPlayers = "Nenhum outro jogador neste servidor",
        Close = "Fechar",
    },

    es = {
        subtitle = "Clover Seas",
        Main = "🏠 Inicio",
        Farm = "⚔ Farm",
        Players = "☺ Jugadores",
        Teleport = "🌀 Teletransporte",
        Settings = "⚙ Configuración",

        quick = "FUNCIONES PRINCIPALES",
        farming = "FARM",
        visuals = "VISUAL DE JUGADORES",
        character = "PERSONAJE",
        islands = "TELETRANSPORTE DE ISLAS",
        bosses = "TELETRANSPORTE DE BOSS",
        playerTeleport = "TELETRANSPORTE DE JUGADOR",
        location = "UBICACIÓN",
        appearance = "APARIENCIA",
        other = "OTRAS CONFIGURACIONES",

        AutoFarm = "Farm Automático",
        AutoQuest = "Misiones Automáticas",
        AutoCollect = "Recoger Automáticamente",
        AutoChest = "Cofres Automáticos",
        AutoBoss = "Boss Automático",
        AutoRollGrimoire = "Girar Grimorio",
        AutoStoreItems = "Guardar Objetos",
        AutoEquip = "Equipar Automáticamente",
        AutoMana = "Mana Automática",

        FarmMobs = "Farmear Enemigos",
        FarmLevel = "Farmear Nivel",
        FarmMoney = "Farmear Dinero",
        AutoAcceptQuest = "Aceptar Misión",
        AutoCompleteQuest = "Completar Misión",

        HighlightPlayer = "Resaltar Jugadores",
        ChestHighlight = "Resaltar Cofres",
        NPCHighlight = "Resaltar NPCs",
        BossHighlight = "Resaltar Bosses",
        PlayerESP = "ESP de Jugadores",
        ChestESP = "ESP de Cofres",
        ShowPlayerNames = "Mostrar Nombres",
        ShowDistance = "Mostrar Distancia",
        ShowHealth = "Mostrar Vida",
        ShowLevel = "Mostrar Nivel",
        SpeedBoost = "Aumentar Velocidad",
        JumpBoost = "Aumentar Salto",
        NoClip = "Atravesar Objetos",
        InfiniteJump = "Salto Infinito",

        TeleportIsland = "Seleccionar Isla",
        TeleportBoss = "Seleccionar Boss",
        TeleportPlayer = "Seleccionar Jugador",
        SaveLocation = "Guardar Ubicación",
        ReturnLocation = "Volver a Ubicación Guardada",

        LightMode = "Modo Claro",
        CompactMode = "Modo Compacto",
        ShowNotifications = "Notificaciones",
        HideUI = "Ocultar Interfaz",
        ShowFPS = "Mostrar FPS",
        ShowPing = "Mostrar Ping",
        Reset = "Restablecer Interruptores",
        Language = "Idioma",
        Select = "Seleccionar",
        Selected = "Seleccionado",
        Saved = "Ubicación guardada",
        Returned = "Volviste a la ubicación guardada",
        NoSaved = "Aún no hay ubicación guardada",
        NoCoords = "Coordenadas aún no definidas",
        NoTarget = "Jugador no disponible",
        TeleportedTo = "Teletransportado a",
        NoPlayers = "No hay otros jugadores en este servidor",
        Close = "Cerrar",
    },
}

local function Tr(Key)
    return T[Language][Key] or T.en[Key] or Key
end

local Gui = Instance.new("ScreenGui")
Gui.Name = "BasHub"
Gui.ResetOnSpawn = false
Gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
Gui.Parent = PlayerGui

local function Corner(Object, Radius)
    local U = Instance.new("UICorner")
    U.CornerRadius = UDim.new(0, Radius or 7)
    U.Parent = Object
end

local function Stroke(Object)
    local S = Instance.new("UIStroke")
    S.Color = C.Border
    S.Thickness = 1
    S.Parent = Object
end

local OpenButton = Instance.new("TextButton")
OpenButton.Name = "OpenButton"
OpenButton.Size = UDim2.fromOffset(48, 48)
OpenButton.Position = UDim2.new(0, 18, 0.5, -24)
OpenButton.BackgroundColor3 = C.BG
OpenButton.Text = "BasH"
OpenButton.TextColor3 = C.White
OpenButton.Font = Enum.Font.GothamBold
OpenButton.TextSize = 14
OpenButton.Visible = false
OpenButton.Parent = Gui
Corner(OpenButton, 10)
Stroke(OpenButton)

local Main = Instance.new("Frame")
Main.Name = "Main"
Main.Size = UDim2.fromOffset(680, 440)
Main.Position = UDim2.new(0.5, -340, 0.5, -220)
Main.BackgroundColor3 = C.BG
Main.BorderSizePixel = 0
Main.Parent = Gui
Corner(Main, 10)
Stroke(Main)

local Top = Instance.new("Frame")
Top.Size = UDim2.new(1, 0, 0, 48)
Top.BackgroundColor3 = C.BG
Top.BorderSizePixel = 0
Top.Parent = Main
Corner(Top, 10)

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(0, 150, 1, 0)
Title.Position = UDim2.fromOffset(16, 0)
Title.BackgroundTransparency = 1
Title.Text = "BAS HUB"
Title.TextColor3 = C.White
Title.TextSize = 19
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Top

local Subtitle = Instance.new("TextLabel")
Subtitle.Size = UDim2.new(0, 200, 1, 0)
Subtitle.Position = UDim2.fromOffset(115, 0)
Subtitle.BackgroundTransparency = 1
Subtitle.Text = Tr("subtitle")
Subtitle.TextColor3 = C.Gray
Subtitle.TextSize = 11
Subtitle.Font = Enum.Font.Gotham
Subtitle.TextXAlignment = Enum.TextXAlignment.Left
Subtitle.Parent = Top

local Minimize = Instance.new("TextButton")
Minimize.Size = UDim2.fromOffset(34, 34)
Minimize.Position = UDim2.new(1, -80, 0, 7)
Minimize.BackgroundColor3 = C.Item
Minimize.Text = "—"
Minimize.TextColor3 = C.White
Minimize.TextSize = 18
Minimize.Font = Enum.Font.GothamBold
Minimize.Parent = Top
Corner(Minimize, 6)

local Close = Instance.new("TextButton")
Close.Size = UDim2.fromOffset(34, 34)
Close.Position = UDim2.new(1, -40, 0, 7)
Close.BackgroundColor3 = C.Item
Close.Text = "×"
Close.TextColor3 = C.White
Close.TextSize = 21
Close.Font = Enum.Font.GothamBold
Close.Parent = Top
Corner(Close, 6)

local Sidebar = Instance.new("Frame")
Sidebar.Size = UDim2.new(0, 165, 1, -49)
Sidebar.Position = UDim2.fromOffset(0, 49)
Sidebar.BackgroundColor3 = C.BG
Sidebar.BorderSizePixel = 0
Sidebar.Parent = Main

local SideLayout = Instance.new("UIListLayout")
SideLayout.Padding = UDim.new(0, 7)
SideLayout.SortOrder = Enum.SortOrder.LayoutOrder
SideLayout.Parent = Sidebar

local SidePadding = Instance.new("UIPadding")
SidePadding.PaddingTop = UDim.new(0, 12)
SidePadding.PaddingLeft = UDim.new(0, 10)
SidePadding.PaddingRight = UDim.new(0, 10)
SidePadding.Parent = Sidebar

local SideLine = Instance.new("Frame")
SideLine.Size = UDim2.new(0, 1, 1, -49)
SideLine.Position = UDim2.new(0, 164, 0, 49)
SideLine.BackgroundColor3 = C.Border
SideLine.BorderSizePixel = 0
SideLine.Parent = Main

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -166, 1, -49)
Content.Position = UDim2.new(0, 166, 0, 49)
Content.BackgroundColor3 = C.BG
Content.BorderSizePixel = 0
Content.Parent = Main

local PageTitle = Instance.new("TextLabel")
PageTitle.Size = UDim2.new(1, -30, 0, 35)
PageTitle.Position = UDim2.fromOffset(15, 9)
PageTitle.BackgroundTransparency = 1
PageTitle.Text = Tr("Main")
PageTitle.TextColor3 = C.White
PageTitle.TextSize = 20
PageTitle.Font = Enum.Font.GothamBold
PageTitle.TextXAlignment = Enum.TextXAlignment.Left
PageTitle.Parent = Content

local PageLine = Instance.new("Frame")
PageLine.Size = UDim2.new(1, -30, 0, 1)
PageLine.Position = UDim2.fromOffset(15, 47)
PageLine.BackgroundColor3 = C.Border
PageLine.BorderSizePixel = 0
PageLine.Parent = Content

local function CreatePage(Name)
    local Page = Instance.new("ScrollingFrame")
    Page.Name = Name .. "Page"
    Page.Size = UDim2.new(1, -30, 1, -62)
    Page.Position = UDim2.fromOffset(15, 57)
    Page.BackgroundTransparency = 1
    Page.BorderSizePixel = 0
    Page.ScrollBarThickness = 3
    Page.ScrollBarImageColor3 = C.Gray
    Page.CanvasSize = UDim2.new(0, 0, 0, 0)
    Page.AutomaticCanvasSize = Enum.AutomaticSize.Y
    Page.Visible = false
    Page.Parent = Content

    local Layout = Instance.new("UIListLayout")
    Layout.Padding = UDim.new(0, 8)
    Layout.SortOrder = Enum.SortOrder.LayoutOrder
    Layout.Parent = Page

    Pages[Name] = Page
    return Page
end

local MainPage = CreatePage("Main")
local FarmPage = CreatePage("Farm")
local PlayersPage = CreatePage("Players")
local TeleportPage = CreatePage("Teleport")
local SettingsPage = CreatePage("Settings")

local TabInfo = {
    {Name = "Main"},
    {Name = "Farm"},
    {Name = "Players"},
    {Name = "Teleport"},
    {Name = "Settings"},
}

local function ChangeTab(Name)
    CurrentTab = Name

    for PageName, Page in pairs(Pages) do
        Page.Visible = PageName == Name
    end

    for TabName, Button in pairs(TabButtons) do
        Button.BackgroundColor3 =
            TabName == Name and C.Item or C.BG
        Button.TextColor3 =
            TabName == Name and C.White or C.Gray
    end

    PageTitle.Text = Tr(Name)
end

for Index, Info in ipairs(TabInfo) do
    local Button = Instance.new("TextButton")
    Button.Name = Info.Name .. "Tab"
    Button.Size = UDim2.new(1, 0, 0, 38)
    Button.BackgroundColor3 = C.BG
    Button.BorderSizePixel = 0
    Button.Text = "  " .. Tr(Info.Name)
    Button.TextColor3 = C.Gray
    Button.TextSize = 13
    Button.Font = Enum.Font.GothamMedium
    Button.TextXAlignment = Enum.TextXAlignment.Left
    Button.LayoutOrder = Index
    Button.Parent = Sidebar
    Corner(Button, 6)

    TabButtons[Info.Name] = Button

    Button.MouseButton1Click:Connect(function()
        ChangeTab(Info.Name)
    end)
end

local function CreateSection(Page, Key)
    local Label = Instance.new("TextLabel")
    Label.Name = "Section_" .. Key
    Label.Size = UDim2.new(1, -2, 0, 25)
    Label.BackgroundTransparency = 1
    Label.Text = Tr(Key)
    Label.TextColor3 = C.Gray
    Label.TextSize = 11
    Label.Font = Enum.Font.GothamBold
    Label.TextXAlignment = Enum.TextXAlignment.Left
    Label.Parent = Page
    return Label
end

local function CreateToggle(Page, Key)
    ToggleStates[Key] = false

    local Row = Instance.new("Frame")
    Row.Name = Key
    Row.Size = UDim2.new(1, -3, 0, 43)
    Row.BackgroundColor3 = C.Item
    Row.BorderSizePixel = 0
    Row.Parent = Page
    Corner(Row, 7)
    Stroke(Row)

    local Label = Instance.new("TextLabel")
    Label.Name = "Label"
    Label.Size = UDim2.new(1, -75, 1, 0)
    Label.Position = UDim2.fromOffset(12, 0)
    Label.BackgroundTransparency = 1
    Label.Text = Tr(Key)
    Label.TextColor3 = C.White
    Label.TextSize = 13
    Label.Font = Enum.Font.GothamMedium
    Label.TextXAlignment = Enum.TextXAlignment.Left
    Label.Parent = Row

    local Switch = Instance.new("TextButton")
    Switch.Name = "ToggleButton"
    Switch.Size = UDim2.fromOffset(44, 24)
    Switch.Position = UDim2.new(1, -56, 0.5, -12)
    Switch.BackgroundColor3 = C.Red
    Switch.BorderSizePixel = 0
    Switch.Text = ""
    Switch.AutoButtonColor = false
    Switch.Parent = Row
    Corner(Switch, 12)

    local Knob = Instance.new("Frame")
    Knob.Name = "Knob"
    Knob.Size = UDim2.fromOffset(18, 18)
    Knob.Position = UDim2.fromOffset(3, 3)
    Knob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    Knob.BorderSizePixel = 0
    Knob.Parent = Switch
    Corner(Knob, 10)

    local function Refresh()
        local Enabled = ToggleStates[Key]

        Switch.BackgroundColor3 = Enabled and C.Green or C.Red

        local TargetPosition = Enabled
            and UDim2.new(1, -21, 0, 3)
            or UDim2.fromOffset(3, 3)

        Knob:TweenPosition(
            TargetPosition,
            Enum.EasingDirection.Out,
            Enum.EasingStyle.Quad,
            0.12,
            true
        )
    end

    Switch.MouseButton1Click:Connect(function()
        ToggleStates[Key] = not ToggleStates[Key]
        Refresh()

        if Key == "LightMode" then
            LightMode = ToggleStates[Key]
            ApplyTheme()
        end

        local Feature = Features[Key]
        if Feature then
            task.spawn(Feature, ToggleStates[Key])
        end
    end)

    ToggleRefresh[Key] = Refresh
    return Row
end

local function Notify(Text, Force)
    if not (Force or ToggleStates.ShowNotifications) then
        return
    end

    pcall(function()
        StarterGui:SetCore("SendNotification", {
            Title = "BAS HUB",
            Text = Text,
            Duration = 3,
        })
    end)
end

local function GetHumanoid()
    local Char = Player.Character
    return Char and Char:FindFirstChildOfClass("Humanoid")
end

local function GetRoot()
    local Char = Player.Character
    return Char and Char:FindFirstChild("HumanoidRootPart")
end

local function TeleportTo(Target)
    local Root = GetRoot()
    if Root then
        Root.CFrame = Target
        return true
    end
    return false
end

local DefaultWalk = 16
local DefaultJumpPower = 50
local DefaultUseJumpPower = true

Features.SpeedBoost = function(On)
    local Hum = GetHumanoid()
    if not Hum then return end

    if On then
        DefaultWalk = Hum.WalkSpeed
    else
        Hum.WalkSpeed = DefaultWalk
    end
end

Features.JumpBoost = function(On)
    local Hum = GetHumanoid()
    if not Hum then return end

    if On then
        DefaultJumpPower = Hum.JumpPower
        DefaultUseJumpPower = Hum.UseJumpPower
    else
        Hum.UseJumpPower = DefaultUseJumpPower
        Hum.JumpPower = DefaultJumpPower
    end
end

-- No Clip
Connections.Stepped = RunService.Stepped:Connect(function()
    if not ToggleStates.NoClip then return end

    local Char = Player.Character
    if not Char then return end

    for _, Part in ipairs(Char:GetDescendants()) do
        if Part:IsA("BasePart") and Part.CanCollide then
            Part.CanCollide = false
        end
    end
end)

-- Infinite Jump
Connections.Jump = UIS.JumpRequest:Connect(function()
    if not ToggleStates.InfiniteJump then return end

    local Hum = GetHumanoid()
    if Hum then
        Hum:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

local ESPFolder = Instance.new("Folder")
ESPFolder.Name = "ESP"
ESPFolder.Parent = Gui

local ESPObjects = {}

local function ClearESP(Target)
    local Data = ESPObjects[Target]
    if Data then
        Data.Highlight:Destroy()
        Data.Billboard:Destroy()
        ESPObjects[Target] = nil
    end
end

local function BuildESP(Target, Char)
    local Head = Char:FindFirstChild("Head")
    if not Head then return nil end

    local Highlight = Instance.new("Highlight")
    Highlight.Adornee = Char
    Highlight.FillColor = Color3.fromRGB(255, 70, 70)
    Highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
    Highlight.FillTransparency = 0.6
    Highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
    Highlight.Parent = ESPFolder

    local Billboard = Instance.new("BillboardGui")
    Billboard.Adornee = Head
    Billboard.Size = UDim2.fromOffset(180, 60)
    Billboard.StudsOffset = Vector3.new(0, 3, 0)
    Billboard.AlwaysOnTop = true
    Billboard.Parent = ESPFolder

    local Info = Instance.new("TextLabel")
    Info.Size = UDim2.fromScale(1, 1)
    Info.BackgroundTransparency = 1
    Info.TextColor3 = Color3.fromRGB(255, 255, 255)
    Info.TextStrokeTransparency = 0.3
    Info.TextSize = 13
    Info.Font = Enum.Font.GothamBold
    Info.Parent = Billboard

    local Data = {
        Char = Char,
        Highlight = Highlight,
        Billboard = Billboard,
        Info = Info,
    }
    ESPObjects[Target] = Data
    return Data
end

local function UpdateESP()
    local WantHighlight = ToggleStates.HighlightPlayer
    local ShowName = ToggleStates.ShowPlayerNames or ToggleStates.PlayerESP
    local ShowDist = ToggleStates.ShowDistance or ToggleStates.PlayerESP
    local ShowHp = ToggleStates.ShowHealth or ToggleStates.PlayerESP
    local ShowLvl = ToggleStates.ShowLevel
    local Anything = WantHighlight or ShowName or ShowDist or ShowHp or ShowLvl
    local MyRoot = GetRoot()

    for _, Other in ipairs(Players:GetPlayers()) do
        if Other ~= Player then
            local Char = Other.Character

            if not Char or not Anything then
                ClearESP(Other)
            else
                local Data = ESPObjects[Other]
                if Data and Data.Char ~= Char then
                    ClearESP(Other)
                    Data = nil
                end
                Data = Data or BuildESP(Other, Char)

                if Data then
                    Data.Highlight.Enabled = WantHighlight and true or false

                    local Lines = {}

                    if ShowName then
                        table.insert(Lines, Other.DisplayName)
                    end

                    if ShowLvl then
                        -- Tenta achar o nível em leaderstats (se o jogo tiver)
                        local LeaderStats = Other:FindFirstChild("leaderstats")
                        local Lvl = LeaderStats and (
                            LeaderStats:FindFirstChild("Level")
                            or LeaderStats:FindFirstChild("Lvl")
                        )
                        if Lvl then
                            table.insert(Lines, "Lv. " .. tostring(Lvl.Value))
                        end
                    end

                    if ShowHp then
                        local Hum = Char:FindFirstChildOfClass("Humanoid")
                        if Hum then
                            table.insert(Lines, "HP: "
                                .. math.floor(Hum.Health) .. "/"
                                .. math.floor(Hum.MaxHealth))
                        end
                    end

                    if ShowDist and MyRoot then
                        local Root = Char:FindFirstChild("HumanoidRootPart")
                        if Root then
                            table.insert(Lines, math.floor(
                                (Root.Position - MyRoot.Position).Magnitude
                            ) .. " studs")
                        end
                    end

                    Data.Billboard.Enabled = #Lines > 0
                    Data.Info.Text = table.concat(Lines, "\n")
                end
            end
        end
    end
end

Connections.Removing = Players.PlayerRemoving:Connect(ClearESP)

local StatsLabel = Instance.new("TextLabel")
StatsLabel.Name = "StatsLabel"
StatsLabel.Size = UDim2.fromOffset(220, 20)
StatsLabel.Position = UDim2.new(1, -230, 0, 40)
StatsLabel.BackgroundTransparency = 1
StatsLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
StatsLabel.TextStrokeTransparency = 0.3
StatsLabel.TextXAlignment = Enum.TextXAlignment.Right
StatsLabel.TextSize = 13
StatsLabel.Font = Enum.Font.GothamBold
StatsLabel.Visible = false
StatsLabel.Parent = Gui

local function UpdateStats(FPS)
    local Parts = {}

    if ToggleStates.ShowFPS then
        table.insert(Parts, "FPS: " .. FPS)
    end

    if ToggleStates.ShowPing then
        local Ok, Ping = pcall(function()
            return math.floor(
                StatsService.Network.ServerStatsItem["Data Ping"]:GetValue()
            )
        end)
        table.insert(Parts, "Ping: " .. (Ok and Ping or "?") .. " ms")
    end

    StatsLabel.Visible = #Parts > 0
    StatsLabel.Text = table.concat(Parts, "  |  ")
end

local Accumulator, Frames = 0, 0

Connections.Heartbeat = RunService.Heartbeat:Connect(function(Delta)
    local Hum = GetHumanoid()
    if Hum then
        if ToggleStates.SpeedBoost then
            Hum.WalkSpeed = Settings.Speed
        end
        if ToggleStates.JumpBoost then
            Hum.UseJumpPower = true
            Hum.JumpPower = Settings.Jump
        end
    end

    Accumulator += Delta
    Frames += 1

    if Accumulator >= 0.25 then
        local FPS = math.floor(Frames / Accumulator + 0.5)
        Accumulator = 0
        Frames = 0

        UpdateESP()
        UpdateStats(FPS)
    end
end)

local WindowScale = Instance.new("UIScale")
WindowScale.Scale = 1
WindowScale.Parent = Main

Features.CompactMode = function(On)
    WindowScale.Scale = On and 0.8 or 1
end

Features.HideUI = function(On)
    if On then
        Main.Visible = false
        OpenButton.Visible = true
    end
end

local function Cleanup()
    if ToggleStates.SpeedBoost then
        Features.SpeedBoost(false)
    end
    if ToggleStates.JumpBoost then
        Features.JumpBoost(false)
    end

    for _, Conn in pairs(Connections) do
        Conn:Disconnect()
    end

    for Key in pairs(ToggleStates) do
        ToggleStates[Key] = false
    end
end

CreateSection(MainPage, "quick")
for _, Key in ipairs({
    "AutoFarm", "AutoQuest", "AutoCollect", "AutoChest",
    "AutoBoss", "AutoRollGrimoire", "AutoStoreItems",
    "AutoEquip", "AutoMana",
}) do
    CreateToggle(MainPage, Key)
end

CreateSection(FarmPage, "farming")
for _, Key in ipairs({
    "FarmMobs", "FarmLevel", "FarmMoney",
    "AutoAcceptQuest", "AutoCompleteQuest",
}) do
    CreateToggle(FarmPage, Key)
end

CreateSection(PlayersPage, "visuals")
for _, Key in ipairs({
    "HighlightPlayer", "ChestHighlight", "NPCHighlight",
    "BossHighlight", "PlayerESP", "ChestESP",
    "ShowPlayerNames", "ShowDistance", "ShowHealth", "ShowLevel",
}) do
    CreateToggle(PlayersPage, Key)
end

CreateSection(PlayersPage, "character")
for _, Key in ipairs({
    "SpeedBoost", "JumpBoost", "NoClip", "InfiniteJump",
}) do
    CreateToggle(PlayersPage, Key)
end

local function CreateSelector(Page, Key, Options, DynamicPlayers, OnSelect)
    local Container = Instance.new("Frame")
    Container.Name = Key .. "Container"
    Container.Size = UDim2.new(1, -3, 0, 43)
    Container.AutomaticSize = Enum.AutomaticSize.Y
    Container.BackgroundColor3 = C.Item
    Container.BorderSizePixel = 0
    Container.Parent = Page
    Corner(Container, 7)
    Stroke(Container)

    local Layout = Instance.new("UIListLayout")
    Layout.Padding = UDim.new(0, 5)
    Layout.SortOrder = Enum.SortOrder.LayoutOrder
    Layout.Parent = Container

    local Header = Instance.new("TextButton")
    Header.Name = "Header"
    Header.Size = UDim2.new(1, 0, 0, 43)
    Header.BackgroundTransparency = 1
    Header.Text = "  " .. Tr(Key) .. "     ▼"
    Header.TextColor3 = C.White
    Header.TextSize = 13
    Header.Font = Enum.Font.GothamMedium
    Header.TextXAlignment = Enum.TextXAlignment.Left
    Header.LayoutOrder = 1
    Header.Parent = Container

    local OptionsFrame = Instance.new("Frame")
    OptionsFrame.Name = "Options"
    OptionsFrame.Size = UDim2.new(1, -12, 0, 0)
    OptionsFrame.Position = UDim2.fromOffset(6, 0)
    OptionsFrame.BackgroundTransparency = 1
    OptionsFrame.Visible = false
    OptionsFrame.LayoutOrder = 2
    OptionsFrame.Parent = Container

    local OptionsLayout = Instance.new("UIListLayout")
    OptionsLayout.Padding = UDim.new(0, 5)
    OptionsLayout.Parent = OptionsFrame

    local function RefreshPlayers()
        for _, Child in ipairs(OptionsFrame:GetChildren()) do
            if Child:IsA("TextButton") then
                Child:Destroy()
            end
        end

        local CurrentOptions = Options

        if DynamicPlayers then
            CurrentOptions = {}
            for _, OtherPlayer in ipairs(Players:GetPlayers()) do
                if OtherPlayer ~= Player then
                    table.insert(CurrentOptions, OtherPlayer.Name)
                end
            end

            if #CurrentOptions == 0 then
                CurrentOptions = {Tr("NoPlayers")}
            end
        end

        for Index, Option in ipairs(CurrentOptions) do
            local Choice = Instance.new("TextButton")
            Choice.Name = "Choice" .. Index
            Choice.Size = UDim2.new(1, 0, 0, 32)
            Choice.BackgroundColor3 = C.BG
            Choice.BorderSizePixel = 0
            Choice.Text = "  " .. tostring(Index) .. ". " .. Option
            Choice.TextColor3 = C.White
            Choice.TextSize = 12
            Choice.Font = Enum.Font.Gotham
            Choice.TextXAlignment = Enum.TextXAlignment.Left
            Choice.LayoutOrder = Index
            Choice.Parent = OptionsFrame
            Corner(Choice, 5)

            Choice.MouseButton1Click:Connect(function()
                Header.Text = "  " .. Tr(Key) .. ": " .. Option .. "  ▼"
                OptionsFrame.Visible = false

                if OnSelect then
                    task.spawn(OnSelect, Option)
                end
            end)
        end

        OptionsFrame.Size = UDim2.new(
            1, -12, 0, #CurrentOptions * 37
        )
    end

    Header.MouseButton1Click:Connect(function()
        local Opening = not OptionsFrame.Visible
        if Opening then
            RefreshPlayers()
        end
        OptionsFrame.Visible = Opening
        Header.Text = "  " .. Tr(Key)
            .. (Opening and "     ▲" or "     ▼")
    end)

    if DynamicPlayers then
        Players.PlayerAdded:Connect(function()
            if OptionsFrame.Visible then
                RefreshPlayers()
            end
        end)

        Players.PlayerRemoving:Connect(function()
            if OptionsFrame.Visible then
                RefreshPlayers()
            end
        end)
    end

    Dropdowns[Key] = {
        Header = Header,
        Refresh = RefreshPlayers,
    }

    return Container
end

local function TeleportToPosition(Positions, Name)
    local Position = Positions[Name]
    if Position then
        TeleportTo(CFrame.new(Position))
        Notify(Tr("TeleportedTo") .. " " .. Name)
    else
        Notify(Tr("NoCoords") .. ": " .. Name, true)
    end
end

CreateSection(TeleportPage, "islands")
CreateSelector(TeleportPage, "TeleportIsland", {
    "3", "Retro Island", "Skull Island", "Beginner Island",
}, false, function(Option)
    TeleportToPosition(IslandPositions, Option)
end)

CreateSection(TeleportPage, "bosses")
CreateSelector(TeleportPage, "TeleportBoss", {
    "1", "Midnight Soldier",
}, false, function(Option)
    TeleportToPosition(BossPositions, Option)
end)

CreateSection(TeleportPage, "playerTeleport")
CreateSelector(TeleportPage, "TeleportPlayer", {}, true, function(Option)
    local Target = Players:FindFirstChild(Option)
    local TargetChar = Target and Target.Character
    local TargetRoot = TargetChar and TargetChar:FindFirstChild("HumanoidRootPart")

    if TargetRoot and TeleportTo(TargetRoot.CFrame * CFrame.new(0, 0, 4)) then
        Notify(Tr("TeleportedTo") .. " " .. Option)
    else
        Notify(Tr("NoTarget"), true)
    end
end)

CreateSection(TeleportPage, "location")

local function CreateAction(Page, Key, Callback)
    local Button = Instance.new("TextButton")
    Button.Name = Key .. "Action"
    Button.Size = UDim2.new(1, -3, 0, 43)
    Button.BackgroundColor3 = C.Item
    Button.BorderSizePixel = 0
    Button.Text = "  " .. Tr(Key)
    Button.TextColor3 = C.White
    Button.TextSize = 13
    Button.Font = Enum.Font.GothamMedium
    Button.TextXAlignment = Enum.TextXAlignment.Left
    Button.Parent = Page
    Corner(Button, 7)
    Stroke(Button)

    Button.MouseButton1Click:Connect(function()
        Callback(Button)
    end)

    return Button
end

local function Flash(Button, Key, MessageKey)
    Button.Text = "  " .. Tr(MessageKey)
    task.delay(1.5, function()
        if Button.Parent then
            Button.Text = "  " .. Tr(Key)
        end
    end)
end

CreateAction(TeleportPage, "SaveLocation", function(Button)
    local Root = GetRoot()
    if Root then
        SavedCFrame = Root.CFrame
        Flash(Button, "SaveLocation", "Saved")
    end
end)

CreateAction(TeleportPage, "ReturnLocation", function(Button)
    if SavedCFrame and TeleportTo(SavedCFrame) then
        Flash(Button, "ReturnLocation", "Returned")
    else
        Flash(Button, "ReturnLocation", "NoSaved")
    end
end)

CreateSection(SettingsPage, "appearance")
CreateToggle(SettingsPage, "LightMode")
CreateToggle(SettingsPage, "CompactMode")
CreateToggle(SettingsPage, "ShowNotifications")
CreateToggle(SettingsPage, "HideUI")
CreateToggle(SettingsPage, "ShowFPS")
CreateToggle(SettingsPage, "ShowPing")

CreateSection(SettingsPage, "other")

local LanguageButton = Instance.new("TextButton")
LanguageButton.Name = "LanguageButton"
LanguageButton.Size = UDim2.new(1, -3, 0, 43)
LanguageButton.BackgroundColor3 = C.Item
LanguageButton.BorderSizePixel = 0
LanguageButton.TextColor3 = C.White
LanguageButton.TextSize = 13
LanguageButton.Font = Enum.Font.GothamMedium
LanguageButton.Parent = SettingsPage
Corner(LanguageButton, 7)
Stroke(LanguageButton)

local LanguageOrder = {"en", "es", "pt"}
local LanguageNames = {
    en = "🇺🇸 English",
    es = "🇪🇸 Español",
    pt = "🇧🇷 Português",
}

local function RefreshTexts()
    Subtitle.Text = Tr("subtitle")

    for _, Info in ipairs(TabInfo) do
        local Button = TabButtons[Info.Name]
        if Button then
            Button.Text = "  " .. Tr(Info.Name)
        end
    end

    PageTitle.Text = Tr(CurrentTab)

    for _, Page in pairs(Pages) do
        for _, Object in ipairs(Page:GetDescendants()) do
            if Object:IsA("TextLabel")
                and Object.Name:sub(1, 8) == "Section_" then
                Object.Text = Tr(Object.Name:sub(9))
            end

            if Object:IsA("TextLabel") then
                local Parent = Object.Parent
                if Parent and ToggleStates[Parent.Name] ~= nil
                    and Object.Name == "Label" then
                    Object.Text = Tr(Parent.Name)
                end
            end
        end
    end

    for _, Object in ipairs(TeleportPage:GetDescendants()) do
        if Object:IsA("TextButton") and Object.Name:sub(-6) == "Action" then
            Object.Text = "  " .. Tr(Object.Name:sub(1, -7))
        end
    end

    for _, Object in ipairs(SettingsPage:GetDescendants()) do
        if Object:IsA("TextButton") and Object.Name:sub(-6) == "Action" then
            Object.Text = "  " .. Tr(Object.Name:sub(1, -7))
        end
    end

    LanguageButton.Text = "🌐  " .. Tr("Language")
        .. ": " .. LanguageNames[Language]

    for _, Data in pairs(Dropdowns) do
        local Key = Data.Header.Parent.Name:gsub("Container", "")
        Data.Header.Text = "  " .. Tr(Key) .. "     ▼"
    end
end

function ApplyTheme()
    if LightMode then
        C.BG = Color3.fromRGB(235, 235, 235)
        C.Panel = Color3.fromRGB(245, 245, 245)
        C.Item = Color3.fromRGB(255, 255, 255)
        C.White = Color3.fromRGB(20, 20, 20)
        C.Gray = Color3.fromRGB(95, 95, 95)
        C.Border = Color3.fromRGB(190, 190, 190)
    else
        C.BG = Color3.fromRGB(9, 9, 9)
        C.Panel = Color3.fromRGB(17, 17, 17)
        C.Item = Color3.fromRGB(25, 25, 25)
        C.White = Color3.fromRGB(245, 245, 245)
        C.Gray = Color3.fromRGB(145, 145, 145)
        C.Border = Color3.fromRGB(55, 55, 55)
    end

    Main.BackgroundColor3 = C.BG
    Top.BackgroundColor3 = C.BG
    Sidebar.BackgroundColor3 = C.BG
    Content.BackgroundColor3 = C.BG
    PageTitle.TextColor3 = C.White
    Title.TextColor3 = C.White
    Subtitle.TextColor3 = C.Gray
    SideLine.BackgroundColor3 = C.Border
    PageLine.BackgroundColor3 = C.Border

    for _, Page in pairs(Pages) do
        for _, Object in ipairs(Page:GetDescendants()) do
            if Object:IsA("Frame") and Object.Name ~= "Options" then
                if Object.Name == "TeleportIslandContainer"
                    or Object.Name == "TeleportBossContainer"
                    or Object.Name == "TeleportPlayerContainer" then
                    Object.BackgroundColor3 = C.Item
                elseif ToggleStates[Object.Name] ~= nil then
                    Object.BackgroundColor3 = C.Item
                end
            elseif Object:IsA("TextLabel") then
                Object.TextColor3 = C.White
            elseif Object:IsA("TextButton") then
                if Object.Name == "ToggleButton" then
                    local Key = Object.Parent.Name
                    Object.BackgroundColor3 =
                        ToggleStates[Key] and C.Green or C.Red
                else
                    Object.BackgroundColor3 = C.Item
                    Object.TextColor3 = C.White
                end
            end
        end
    end
    ChangeTab(CurrentTab)
end

LanguageButton.MouseButton1Click:Connect(function()
    local Index = table.find(LanguageOrder, Language) or 1
    Index = (Index % #LanguageOrder) + 1
    Language = LanguageOrder[Index]
    RefreshTexts()
end)

CreateAction(SettingsPage, "Reset", function(Button)
    for Key in pairs(ToggleStates) do
        local WasOn = ToggleStates[Key]
        ToggleStates[Key] = false

        if ToggleRefresh[Key] then
            ToggleRefresh[Key]()
        end

        if WasOn and Features[Key] then
            task.spawn(Features[Key], false)
        end
    end

    if LightMode then
        LightMode = false
        ApplyTheme()
    end
end)

Minimize.MouseButton1Click:Connect(function()
    Main.Visible = false
    OpenButton.Visible = true
end)

OpenButton.MouseButton1Click:Connect(function()
    Main.Visible = true
    OpenButton.Visible = false

    if ToggleStates.HideUI then
        ToggleStates.HideUI = false
        ToggleRefresh.HideUI()
    end
end)

Close.MouseButton1Click:Connect(function()
    Cleanup()
    Gui:Destroy()
end)

local Dragging = false
local DragStart
local StartPosition

Top.InputBegan:Connect(function(Input)
    if Input.UserInputType == Enum.UserInputType.MouseButton1
        or Input.UserInputType == Enum.UserInputType.Touch then

        Dragging = true
        DragStart = Input.Position
        StartPosition = Main.Position

        Input.Changed:Connect(function()
            if Input.UserInputState == Enum.UserInputState.End then
                Dragging = false
            end
        end)
    end
end)

UIS.InputChanged:Connect(function(Input)
    if not Dragging then return end

    if Input.UserInputType == Enum.UserInputType.MouseMovement
        or Input.UserInputType == Enum.UserInputType.Touch then

        local Delta = Input.Position - DragStart
        Main.Position = UDim2.new(
            StartPosition.X.Scale,
            StartPosition.X.Offset + Delta.X,
            StartPosition.Y.Scale,
            StartPosition.Y.Offset + Delta.Y
        )
    end
end)

RefreshTexts()
ChangeTab("Main")
