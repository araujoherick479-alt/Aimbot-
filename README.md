# Aimbot--- Painel ESP/Aimbot/Chams universal, inimigos (não pega em time nem você)
-- Adicionado opção no AIMBOT para "atravessar parede" ou "não atravessar parede" (WallCheck)
-- por: silva/injeção

Jogadores locais = jogo:GetService("Jogadores")
local LocalPlayer = Jogadores.LocalPlayer
Câmera local = workspace.CurrentCamera
local RunService = jogo:GetService("RunService")
espaço de trabalho local = jogo:GetService("Espaço de trabalho")

-- Estados
local espLinha, espCaixa, espChams, espVida = falso,falso,falso,falso
aimbotAtivo local = falso
AimPart local = "Cabeça"
AimFov local = 50
Velocidade local = 16
aimKillAtivo local = falso
aimKillDelay local = 0,01
desenhos locais = {}

local wallCheck = true -- Nova opção: não atravessar parede

ESPColorVisible local = Cor3.deRGB(0,255,0)
ESPColorInvisible local = Cor3.deRGB(255,0,0)
ESPColorWhite local = Cor3.fromRGB(255,255,255)
ESPColorBlue local = Color3.fromRGB(10,40,200)
ESPColorPink local = Color3.fromRGB(255,80,220)
local currentESPColorVisible = ESPColorVisible
local currentESPColorInvisible = ESPColorInvisible
espColorMode local = "visível"

se LocalPlayer.PlayerGui:FindFirstChild("InjectionGUI") então
    LocalPlayer.PlayerGui.InjectionGUI:Destroy()
fim

ScreenGui local = Instância.new("ScreenGui")
ScreenGui.Name = "InjeçãoGUI"
ScreenGui.ResetOnSpawn = falso
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

Quadro local = Instância.new("Quadro")
Frame.Size = UDim2.new(0,250,0,470)
Frame.Posição = UDim2.novo(0,35,0,0,3,0)
Frame.BackgroundColor3 = Cor3.fromRGB(30,30,60)
Frame.Active = verdadeiro
Frame.Draggable = verdadeiro
Frame.Visible = verdadeiro
Frame.Parent = ScreenGui

Título local = Instance.new("TextLabel")
Título.Tamanho = UDim2.novo(1,0,0,30)
Título.BackgroundColor3 = Cor3.fromRGB(50,50,80)
Título.TextColor3 = Color3.fromRGB(0.255.255)
Título.Fonte = Enum.Fonte.SourceSansBold
Título.TamanhoDoTexto = 16
Title.Text = "Painel de Injeção"
Título.Parent = Quadro

btnMin local = Instância.new("TextButton")
btnMin.Size = UDim2.new(0,30,0,25)
btnMin.Posição = UDim2.new(1,-35,0,2)
btnMin.Texto = "_"
btnMin.BackgroundColor3 = Cor3.fromRGB(70,70,100)
btnMin.TextColor3 = Color3.fromRGB(255.255.255)
btnMin.Parent = Quadro

local abrirBtn = nulo
btnMin.MouseButton1Click:Conectar(função()
    Frame.Visible = falso
    se abrirBtn então abrirBtn:Destroy() fim
    abrirBtn = Instance.new("TextButton")
    abrirBtn.Size = UDim2.new(0,100,0,25)
    abrirBtn.Position = UDim2.new(0.35,0,0.3,0)
    abrirBtn.Text = "Abrir Menu"
    abrirBtn.BackgroundColor3 = Color3.fromRGB(70,70,100)
    abrirBtn.TextColor3 = Color3.fromRGB(255.255.255)
    abrirBtn.Active = true
    abrirBtn.Draggable = true
    abrirBtn.Parent = ScreenGui
    abrirBtn.MouseButton1Click:Connect(function()
        abrirBtn:Destroy()
        Frame.Visible = verdadeiro
    fim)
fim)

função local criarBotão(texto,x,y)
    botão local = Instance.new("TextButton")
    btn.Tamanho = UDim2.novo(0,90,0,25)
    btn.Posição = UDim2.novo(0,x,0,y)
    btn.BackgroundColor3 = Cor3.fromRGB(70,70,100)
    btn.TextColor3 = Color3.fromRGB(255.255.255)
    btn.Text = texto
    btn.Parent = Quadro
    botão de retorno
fim

local btnESP = criarBotao("ESP",10,50)
local btnAimbot = criarBotao("Aimbot",10,90)
local btnMisc = criarBotao("Misc",10,130)
local btnInfo = criarBotao("Info",10,170)

espFrame local = Instância.new("Quadro",Quadro)
espFrame.Size = UDim2.new(0,140,0,210)
espFrame.Position = UDim2.new(0,110,0,40)
espFrame.BackgroundTransparency = 1
espFrame.Visible = verdadeiro

aimbotFrame local = Instance.new("Quadro",Quadro)
aimbotFrame.Size = UDim2.new(0,140,0,250)
aimbotFrame.Position = UDim2.new(0,110,0,40)
aimbotFrame.BackgroundTransparency = 1
aimbotFrame.Visible = falso

miscFrame local = Instância.new("Quadro",Quadro)
miscFrame.Size = UDim2.new(0,140,0,320)
miscFrame.Position = UDim2.new(0,110,0,40)
miscFrame.BackgroundTransparency = 1
miscFrame.Visible = falso

infoFrame local = Instance.new("Quadro",Quadro)
infoFrame.Size = UDim2.new(0,250,0,400)
infoFrame.Posição = UDim2.novo(0,0,0,0)
infoFrame.BackgroundTransparency = 1
infoFrame.Visible = falso

btnESP.MouseButton1Click:Conectar(função()
    espFrame.Visible=true
    aimbotFrame.Visible=false
    miscFrame.Visible=false
    infoFrame.Visible=false
fim)
btnAimbot.MouseButton1Click:Conectar(função()
    espFrame.Visible=false
    aimbotFrame.Visible=true
    miscFrame.Visible=false
    infoFrame.Visible=false
fim)
btnMisc.MouseButton1Click:Conectar(função()
    espFrame.Visible=false
    aimbotFrame.Visible=false
    miscFrame.Visible=true
    infoFrame.Visible=false
fim)
btnInfo.MouseButton1Click:Conectar(função()
    espFrame.Visible=false
    aimbotFrame.Visible=false
    miscFrame.Visible=false
    infoFrame.Visible=true
fim)

infoLabel local = Instância.new("TextLabel",infoFrame)
infoLabel.Size = UDim2.new(0,200,0,40)
infoLabel.Position = UDim2.new(0, 170, 0,5, -20)
infoLabel.BackgroundTransparency = 0,3
infoLabel.BackgroundColor3 = Cor3.fromRGB(30,30,80)
infoLabel.TextColor3 = Color3.fromRGB(0.255.255)
infoLabel.Font = Enum.Font.SourceSansBold
infoLabel.TextSize = 20
infoLabel.Text = "por: silva/injeção"
infoLabel.Visible = verdadeiro

função local criarCheckboxESP(txt,y)
    botão local = Instance.new("TextButton",espFrame)
    btn.Tamanho = UDim2.novo(0,140,0,25)
    btn.Posição = UDim2.novo(0,0,0,y)
    btn.Text=txt.." DESLIGADO"
    btn.BackgroundColor3 = Cor3.fromRGB(100,100,150)
    btn.TextColor3 = Color3.fromRGB(255.255.255)
    botão de retorno
fim

local espLinhaBtn = criarCheckboxESP("Linha",0)
local espCaixaBtn = criarCheckboxESP("Caixa",40)
local espChamsBtn = criarCheckboxESP("Chams",80)
local espVidaBtn = criarCheckboxESP("Vida",120)

espLinhaBtn.MouseButton1Click:Conectar(função()
    espLinha = não espLinha
    espLinhaBtn.Text = "Linha "..(espLinha e "ON" ou "OFF")
fim)
espCaixaBtn.MouseButton1Click:Conectar(função()
    espCaixa = não espCaixa
    espCaixaBtn.Text = "Caixa "..(espCaixa e "ON" ou "OFF")
fim)
espChamsBtn.MouseButton1Click:Conectar(função()
    espChams = não espChams
    espChamsBtn.Text = "Chams "..(espChams e "ON" ou "OFF")
fim)
espVidaBtn.MouseButton1Click:Conectar(função()
    espVida = não espVida
    espVidaBtn.Text = "Vida "..(espVida e "ON" ou "OFF")
fim)

aimbotBtn local = Instance.new("TextButton")
aimbotBtn.Size=UDim2.new(0,140,0,25)
aimbotBtn.Position=UDim2.new(0,0,0,0)
aimbotBtn.Text="Aimbot DESLIGADO"
aimbotBtn.BackgroundColor3=Color3.fromRGB(100,100,150)
aimbotBtn.TextColor3=Color3.fromRGB(255.255.255)
aimbotBtn.Parent=aimbotFrame
aimbotBtn.MouseButton1Click:Conectar(função()
    aimbotAtivo = não aimbotAtivo
    aimbotBtn.Text = "Aimbot "..(aimbotAtivo e "ON" ou "OFF")
fim)

local btnHead = Instance.new("TextButton",aimbotFrame)
btnHead.Size=UDim2.new(0,60,0,25)
btnCabeça.Posição=UDim2.novo(0,0,0,35)
btnHead.Text="Cabeça"
btnHead.BackgroundColor3=Cor3.fromRGB(100,100,150)
btnHead.TextColor3=Color3.fromRGB(255.255.255)
btnHead.MouseButton1Click:Conectar(função() AimPart="Cabeça" fim)

local btnTorso = Instance.new("TextButton",aimbotFrame)
btnTorso.Tamanho=UDim2.novo(0,60,0,25)
btnTorso.Posição=UDim2.novo(0,70,0,35)
btnTorso.Text="Torso"
btnTorso.BackgroundColor3=Color3.fromRGB(100,100,150)
btnTorso.TextColor3=Color3.fromRGB(255.255.255)
btnTorso.MouseButton1Click:Conectar(função() AimPart="Torso" fim)

lblFov local = Instância.new("TextLabel",aimbotFrame)
lblFov.Tamanho=UDim2.novo(0,140,0,25)
lblFov.Posição=UDim2.novo(0,0,0,70)
lblFov.TransparênciaDeFundo=1
lblFov.TextColor3=Color3.fromRGB(0,255,0)
lblFov.Text="FOV: "..AimFov

local btnFovMenos = Instance.new("TextButton",aimbotFrame)
btnFovMenos.Tamanho=UDim2.novo(0,60,0,25)
btnFovMenos.Posição=UDim2.novo(0,0,0,95)
btnFovMenos.Text="-"
btnFovMenos.BackgroundColor3=Cor3.fromRGB(100,100,150)
btnFovMenos.TextColor3=Color3.fromRGB(255.255.255)
btnFovMenos.MouseButton1Click:Conectar(função()
    AimFov = math.max(10,AimFov-5)
    lblFov.Text="FOV: "..AimFov
fim)

btnFovMais local = Instance.new("TextButton",aimbotFrame)
btnFovMais.Size=UDim2.new(0,60,0,25)
btnFovMais.Posição=UDim2.novo(0,70,0,95)
btnFovMais.Text="+"
btnFovMais.BackgroundColor3=Color3.fromRGB(100,100,150)
btnFovMais.TextColor3=Color3.fromRGB(255.255.255)
btnFovMais.MouseButton1Click:Conectar(função()
    Campo de Aim = Campo de Aim+5
    lblFov.Text="FOV: "..AimFov
fim)

wallCheckBtn local = Instance.new("TextButton",aimbotFrame)
wallCheckBtn.Size=UDim2.new(0,140,0,25)
wallCheckBtn.Position=UDim2.new(0,0,0,125)
wallCheckBtn.Text="Não atravessar parede"
wallCheckBtn.BackgroundColor3=Cor3.fromRGB(100,100,150)
wallCheckBtn.TextColor3 = Color3.fromRGB (255.255.255)
wallCheckBtn.Parent = aimbotFrame
wallCheckBtn.MouseButton1Click:Conectar(função()
    wallCheck = não wallCheck
    wallCheckBtn.Text = wallCheck e "Não atravessar parede" ou "Atravessar parede"
fim)

lblSpeed local = Instância.new("TextLabel")
lblSpeed.Size=UDim2.new(0,140,0,25)
lblSpeed.Posição=UDim2.novo(0,0,0,0)
lblSpeed.TransparênciaDeFundo=1
lblSpeed.TextColor3=Color3.fromRGB(0.255.255)
lblSpeed.Text="Velocidade: "..Velocidade
lblSpeed.Parent=quadro misc

btnSpeedMenos local = Instance.new("TextButton")
btnSpeedMenos.Size=UDim2.new(0,60,0,25)
btnSpeedMenos.Position=UDim2.new(0,0,0,30)
btnSpeedMenos.Text="-"
btnSpeedMenos.BackgroundColor3=Cor3.fromRGB(100,100,150)
btnSpeedMenos.TextColor3=Color3.fromRGB(255.255.255)
btnSpeedMenos.Parent=miscFrame

btnSpeedMais local = Instance.new("TextButton")
btnSpeedMais.Size=UDim2.new(0,60,0,25)
btnSpeedMais.Position=UDim2.new(0,70,0,30)
btnSpeedMais.Text="+"
btnSpeedMais.BackgroundColor3=Color3.fromRGB(100,100,150)
btnSpeedMais.TextColor3=Color3.fromRGB(255.255.255)
btnSpeedMais.Parent=miscFrame

btnSpeedMenos.MouseButton1Click:Conectar(função()
    Velocidade = math.max(16,Speed-2)
    lblSpeed.Text="Velocidade: "..Velocidade
    se LocalPlayer.Character então LocalPlayer.Character.Humanoid.WalkSpeed = Velocidade final
fim)
btnSpeedMais.MouseButton1Click:Conectar(função()
    Velocidade = Velocidade+2
    lblSpeed.Text="Velocidade: "..Velocidade
    se LocalPlayer.Character então LocalPlayer.Character.Humanoid.WalkSpeed = Velocidade final
fim)

aimKillBtn local = Instance.new("TextButton")
aimKillBtn.Size=UDim2.new(0,140,0,25)
aimKillBtn.Position=UDim2.new(0,0,0,65)
aimKillBtn.Text="AimKill DESLIGADO"
aimKillBtn.BackgroundColor3=Color3.fromRGB(255,50,50)
aimKillBtn.TextColor3=Color3.fromRGB(255.255.255)
aimKillBtn.Parent=miscFrame
aimKillBtn.MouseButton1Click:Conectar(função()
    aimKillAtivo = não aimKillAtivo
    aimKillBtn.Text = "AimKill "..(aimKillAtivo e "ON" ou "OFF")
fim)

lblEspColor local = Instance.new("TextLabel",miscFrame)
lblEspColor.Size = UDim2.new(0,140,0,20)
lblEspColor.Position = UDim2.new(0,0,0,95)
lblEspColor.BackgroundTransparency = 1
lblEspColor.TextColor3 = currentESPColorVisible
lblEspColor.Text = "Cor ESP: Visível (Verde)"

btnEspColorVisible local = Instance.new("TextButton",miscFrame)
btnEspColorVisible.Size = UDim2.new(0,60,0,20)
btnEspColorVisible.Position = UDim2.new(0,0,0,120)
btnEspColorVisible.Text = "Cor ESP Visível"
btnEspColorVisible.BackgroundColor3 = currentESPColorVisible
btnEspColorVisible.TextColor3 = Color3.fromRGB(0,0,0)
btnEspColorVisible.MouseButton1Click:Conectar(função()
    espColorMode = "visível"
    lblEspColor.Text = "Cor ESP: Visível (Verde)"
    lblEspColor.TextColor3 = currentESPColorVisible
    pop-up local = Instância.new("Quadro",miscFrame)
    popup.Tamanho = UDim2.novo(0,135,0,60)
    popup.Posição = UDim2.new(0,0,0,145)
    popup.BackgroundColor3 = Cor3.fromRGB(50,50,100)
    pop-up.BorderSizePixel = 0

    btnWhite local = Instância.new("TextButton",popup)
    btnBranco.Tamanho = UDim2.novo(0,40,0,20)
    btnBranco.Posição = UDim2.novo(0,5,0,5)
    btnWhite.Text = "Branco"
    btnBranco.CorDeFundo3 = ESPColorBranco
    btnWhite.TextColor3 = Color3.fromRGB(0,0,0)
    btnWhite.MouseButton1Click:Conectar(função()
        currentESPColorVisible = ESPColorWhite
        lblEspColor.TextColor3 = ESPColorWhite
        pop-up:Destruir()
    fim)
    btnBlue local = Instância.new("TextButton",popup)
    btnAzul.Tamanho = UDim2.novo(0,40,0,20)
    btnAzul.Posição = UDim2.novo(0,45,0,5)
    btnBlue.Text = "Azul"
    btnAzul.CorDeFundo3 = ESPColorAzul
    btnBlue.TextColor3 = Color3.fromRGB(255.255.255)
    btnBlue.MouseButton1Click:Conectar(função()
        currentESPColorVisible = ESPColorBlue
        lblEspColor.TextColor3 = ESPColorAzul
        pop-up:Destruir()
    fim)
    btnPink local = Instância.new("TextButton",popup)
    btnPink.Size = UDim2.new(0,40,0,20)
    btnPink.Posição = UDim2.novo(0,90,0,5)
    btnPink.Text = "Rosa"
    btnPink.BackgroundColor3 = ESPColorPink
    btnPink.TextColor3 = Color3.fromRGB(255.255.255)
    btnPink.MouseButton1Click:Conectar(função()
        currentESPColorVisible = ESPColorPink
        lblEspColor.TextColor3 = ESPColorPink
        pop-up:Destruir()
    fim)
fim)

btnEspColorInvisible local = Instance.new("TextButton",miscFrame)
btnEspColorInvisible.Size = UDim2.new(0,70,0,20)
btnEspColorInvisible.Position = UDim2.new(0,65,0,120)
btnEspColorInvisible.Text = "Cor ESP Invisível"
btnEspColorInvisible.BackgroundColor3 = currentESPColorInvisible
btnEspColorInvisible.TextColor3 = Color3.fromRGB(0,0,0)
btnEspColorInvisible.MouseButton1Click:Conectar(função()
    espColorMode = "invisível"
    lblEspColor.Text = "Cor ESP: Invisível (Vermelho)"
    lblEspColor.TextColor3 = currentESPColorInvisible
    pop-up local = Instância.new("Quadro",miscFrame)
    popup.Tamanho = UDim2.novo(0,135,0,60)
    popup.Posição = UDim2.new(0,0,0,145)
    popup.BackgroundColor3 = Cor3.fromRGB(50,50,100)
    pop-up.BorderSizePixel = 0

    btnWhite local = Instância.new("TextButton",popup)
    btnBranco.Tamanho = UDim2.novo(0,40,0,20)
    btnBranco.Posição = UDim2.novo(0,5,0,5)
    btnWhite.Text = "Branco"
    btnBranco.CorDeFundo3 = ESPColorBranco
    btnWhite.TextColor3 = Color3.fromRGB(0,0,0)
    btnWhite.MouseButton1Click:Conectar(função()
        currentESPColorInvisible = ESPColorWhite
        lblEspColor.TextColor3 = ESPColorWhite
        pop-up:Destruir()
    fim)
    btnBlue local = Instância.new("TextButton",popup)
    btnAzul.Tamanho = UDim2.novo(0,40,0,20)
    btnAzul.Posição = UDim2.novo(0,45,0,5)
    btnBlue.Text = "Azul"
    btnAzul.CorDeFundo3 = ESPColorAzul
    btnBlue.TextColor3 = Color3.fromRGB(255.255.255)
    btnBlue.MouseButton1Click:Conectar(função()
        currentESPColorInvisible = ESPColorBlue
        lblEspColor.TextColor3 = ESPColorAzul
        pop-up:Destruir()
    fim)
    btnPink local = Instância.new("TextButton",popup)
    btnPink.Size = UDim2.new(0,40,0,20)
    btnPink.Posição = UDim2.novo(0,90,0,5)
    btnPink.Text = "Rosa"
    btnPink.BackgroundColor3 = ESPColorPink
    btnPink.TextColor3 = Color3.fromRGB(255.255.255)
    btnPink.MouseButton1Click:Conectar(função()
        currentESPColorInvisible = ESPColorPink
        lblEspColor.TextColor3 = ESPColorPink
        pop-up:Destruir()
    fim)
fim)

função local isEnemy(char)
    plr local = Jogadores:GetPlayerFromCharacter(char)
    se plr então
        se plr == LocalPlayer então retorna falso fim
        se plr.Team ~= nil e LocalPlayer.Team ~= nil então
            retornar plr.Team ~= LocalPlayer.Team
        fim
        se plr.TeamColor ~= nil e LocalPlayer.TeamColor ~= nil então
            retornar plr.TeamColor ~= LocalPlayer.TeamColor
        fim
        retornar verdadeiro
    fim
    retornar verdadeiro
fim

função local getCharacters()
    caracteres locais = {}
    para _,obj em ipairs(workspace:GetDescendants()) faça
        se obj:IsA("Modelo") e obj:FindFirstChild("Humanoid") e obj:FindFirstChild("HumanoidRootPart") então
            se isEnemy(obj) então
                tabela.inserir(caracteres, obj)
            fim
        fim
    fim
    caracteres de retorno
fim

função local applyChams(char, isVisible)
    para _,parte em ipairs(char:GetChildren()) faça
        se parte:IsA("BasePart") então
            anúncio local = parte:FindFirstChild("ChamAdorno")
            local colorChams = isVisible e currentESPColorVisible ou currentESPColorInvisible
            se espChams então
                se não for um anúncio então
                    ad = Instance.new("AdornoCaixaHandle")
                    ad.Nome = "ChamAdorno"
                    ad.Adornee = parte
                    ad.ZIndex = 10
                    ad.AlwaysOnTop = verdadeiro
                    ad.Size = part.Size + Vector3.new(0.1,0.1,0.1)
                    ad.Color3 = corChams
                    anúncio.Transparência = 0,6
                    ad.Parent = parte
                outro
                    ad.Color3 = corChams
                    anúncio.Transparência = 0,6
                    ad.Size = part.Size + Vector3.new(0.1,0.1,0.1)
                fim
            outro
                se ad então ad:Destroy() fim
            fim
        fim
    fim
fim

função local clearDrawings()
    para _,v em pares(desenhos) faça
        pcall(função() v:Remover() fim)
    fim
    desenhos = {}
fim

função local wallCheckVisible(parte)
    se não for wallCheck então retorne verdadeiro fim
    origem local = Câmera.CFrame.Posição
    local dest = part.Position
    raio local = Ray.new(origem, (origem-destino).Unidade * (origem-destino).Magnitude)
    local ignoreList = {Câmera, LocalPlayer.Character}
    acerto local = espaço de trabalho:FindPartOnRayWithIgnoreList(ray, ignoreList)
    retornar (não atingido) ou (acerto:IsDescendantOf(part.Parent))
fim

função local drawESP()
    clearDrawings()
    caracteres locais = getCharacters()
    para _,char em ipairs(chars) faça
        raiz local = char:FindFirstChild("HumanoidRootPart")
        se raiz então
            pos local, vis = Câmera:WorldToViewportPoint(root.Position)
            centro local = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
            tela localPos = Vector2.new(pos.X, pos.Y)
            dist local = (screenPos - centro).Magnitude
            parte localVisível = wallCheckVisible(raiz)
            local isVisible = vis e dist < AimFov e partVisible
            local colorToUse = isVisible e currentESPColorVisible ou currentESPColorInvisible

            se espLinha e vis então
                ln local = Desenho.new("Linha")
                ln.From = Vetor2.novo(Câmera.TamanhoDaVisualização.X/2,0)
                ln.To = Vetor2.novo(pos.X,pos.Y)
                ln.Color = corParaUsar
                ln.Espessura = 1,2
                ln.Visible = verdadeiro
                tabela.insert(desenhos,ln)
            fim
            se espCaixa e vis então
                tamanho local = Vector2.new(28,38)
                local superiorEsquerdo = Vetor2.novo(pos.X-tamanho.X/2,pos.Y-tamanho.Y/2)
                retângulo local = Desenho.novo("Quadrado")
                rect.Position = superiorEsquerdo
                rect.Size = tamanho
                rect.Color = corParaUsar
                Espessura retangular = 1,5
                rect.Filled = falso
                rect.Visible = verdadeiro
                tabela.inserir(desenhos,retângulo)
            fim
            se espVida e char:FindFirstChild("Humanoid") e vis então
                zumbido local = char.Humanoid
                perc local = hum.Saúde/hum.SaúdeMáxima
                barra local = Desenho.new("Quadrado")
                barra.Posição = Vetor2.novo(pos.X-14,pos.Y-22)
                bar.Size = Vetor2.novo(28*perc,4)
                barra.Cor = Cor3.deRGB(0,255,0)
                bar.Filled = verdadeiro
                bar.Visible = verdadeiro
                tabela.inserir(desenhos,barra)
            fim

            aplicarChams(char, éVisível)
        fim
    fim
fim

função local getAimbotTarget()
    local mais próximoPart = nulo
    localmaispróximoDist = AimFov
    centro local = Vector2.new(Camera.ViewportSize.X/2, Camera.ViewportSize.Y/2)
    caracteres locais = getCharacters()
    para _,
