local Model = game:GetObjects("rbxassetid://8465179718")[1]

local Mouse = game.Players.LocalPlayer:GetMouse()

local UI = Model
UI.Parent = game.Players.LocalPlayer.PlayerGui




local Data = {}
local WS_Data = {}
local WD_Data = {}
local WeldData = {}
local Names = {}
local WeldCount = 0
local ClassValues = {"CFrame","Anchored","Color","Shape","Size","Material","CanCollide","Health","MaxHealth","Texture","Transparency","SoundId","Part1","Part0","Face","C1","C0","MeshType","ShirtTemplate","PantsTemplate","Brightness","Enabled","Range","Shadows","CastShadow","MeshId"}


local EvenMoreFuckingDataPleaseKillMe = {}

local InstanceBANList = {"Union","MeshPart","Beam","ParticleEmitter","RemoteEvent","LocalScript","Status","Animator","ScreenGui","Frame","SurfaceGui","BillBoardGui","ImageLabel","ImageButton","Button"}






--local UI = game.Players.LocalPlayer.PlayerGui:WaitForChild("ModelGrabber")
UI["GrabberFrame"].T.Text = "Creo's Model Grabber"
local GrabButton = UI["GrabberFrame"].Grab
local SelectedModelText = UI["GrabberFrame"]["Selected Model"]


local GrabTarget = nil
local Outline = UI["GrabberFrame"].Selection
local CLine = Instance.new("Part",nil)

local GrabbingModel = false











local INPUTD = false
spawn(function()
	local UserInputService = game:GetService("UserInputService")

	local gui = UI.GrabberFrame

	local dragging
	local dragInput
	local dragStart
	local startPos

	local function update(input)
		local delta = input.Position - dragStart
		gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end

	gui.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			INPUTD = true
			dragging = true
			dragStart = input.Position
			startPos = gui.Position

			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
					INPUTD = false
				end
			end)
		end
	end)

	gui.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)

	UserInputService.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			update(input)
		end
	end)
end)












Mouse.Button1Down:Connect(function()
	if INPUTD == false then
		local Target = Mouse.Target
		local VENV = Target
		if Target and (Target:IsA("Model") or Target:IsA("Part") or Target:IsA("MeshPart")) then
			while VENV ~= workspace do
				if Target.Parent ~= workspace then
					VENV = Target.Parent
					Target = Target.Parent
				else
					break
				end
			end

			CLine:Destroy()
			GrabTarget = Target
			SelectedModelText.Text = Target.Name
			CLine = Outline:Clone(Target)
			CLine.Parent = workspace
			CLine.Adornee = Target
		else
			Target = nil
			CLine:Destroy()
			SelectedModelText.Text = "NIL"
		end
	end
end)


UI.GrabberFrame.Grab.MouseEnter:Connect(function()
	UI.GrabberFrame.Grab.BackgroundTransparency = 0.9
	if GrabTarget ~= nil then
		UI.GrabberFrame.Grab.TextColor3 = Color3.new(0,999,0)
	else
		UI.GrabberFrame.Grab.TextColor3 = Color3.new(999,0,0)
	end
end)
UI.GrabberFrame.Grab.MouseLeave:Connect(function()
	UI.GrabberFrame.Grab.TextColor3 = Color3.new(1,1,1)
	UI.GrabberFrame.Grab.BackgroundTransparency = 1
end)

UI.GrabberFrame.Grab.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		if GrabTarget ~= nil and GrabbingModel == false then
			GrabbingModel = true
			local tabam = 0
			local GrabFrame = UI.GrabberFrame.Storage.GrabbingFrame:Clone()
			UI.GrabberFrame.Transparency =1
			GrabFrame.Parent = UI
			local DataText = {["Text"] = "Variables = {} \n"}
			local LoadingBar = GrabFrame.GeneratingFrame.PorgressBar.Loaded

			local aol = GrabTarget:Clone()

			local LName = aol.Name
			Names["Instance"..tostring(1)] = LName
			local vn = 1
			aol.Name = math.random(-100000,100000)
			local MDL = Instance.new("Model")
			for i,v in pairs(aol:GetDescendants()) do
				if table.find(InstanceBANList,v.ClassName) then
					v:Destroy()
				else
					vn+=1
					local LName = v.Name			
					v.Name = math.random(-100000,100000)
					Names["Instance"..tostring(vn)] = LName	
				end
			end
			aol.Parent = MDL


			local CT = MDL:GetDescendants()
			for i,v in pairs(CT) do
				game:GetService("RunService").Stepped:wait()

				if table.find(InstanceBANList,v.ClassName) then
				else

					Data["Part"..tostring(tabam)] = {["InstanceType"] = v.ClassName}
					EvenMoreFuckingDataPleaseKillMe[v.Name] = "Instance"..tabam



					Data["Part"..tostring(tabam)]["Name"] = "Instance"..tostring(tabam)
					Data["Part"..tostring(tabam)]["Parent"] = "workspace"
					WS_Data["Instance"..tabam] = v
					WD_Data[v.Name] = "Instance"..tabam





					for l,f in pairs(ClassValues) do
						coroutine.resume(coroutine.create(function()
							if v[f] then
								if f == "CFrame" or f== "C1" or f == "C0" then
									Data["Part"..tostring(tabam)][f] = "CFrame.new("..tostring(v[f])..")"
								elseif f == "Size" then
									Data["Part"..tostring(tabam)][f] = "Vector3.new("..tostring(v[f])..")"
								elseif f == "Color" or f == "Color3" then
									Data["Part"..tostring(tabam)][f] = "Color3.new("..tostring(v[f])..")"
								elseif f == "Texture" or f == "SoundId" or f == "ShirtTemplate" or f == "PantsTemplate" then
									Data["Part"..tostring(tabam)][f] = "'"..v[f].."'"
								elseif f == "MeshId" then
								    Data["Part"..tostring(tabam)][f] = "'"..tostring(v[f]).."'"
								elseif f == "Part1" or f == "Part0" then
									if not WeldData[v.Name] then
										WeldCount += 1
									end
									WeldData["Weld"..WeldCount] = {[tostring(f)] = v[tostring(f)],["Weld"] = v.Name}
								else
									Data["Part"..tostring(tabam)][f] = tostring(v[f])
								end
							end	
						end))
					end














					LoadingBar.Size = UDim2.new((1/#CT)*i,0,1,0)
					tabam+=1	
				end
			end
			local fnv = 0

			GrabFrame.GeneratingFrame.Gen.Text = "Building Code"



			--[[Code Building]]--

			for l=1,tabam do
				game:GetService("RunService").Stepped:wait()
				local MainData = Data["Part"..tostring(fnv)]
				local Classtype = tostring(Data["Part"..tostring(fnv)]["InstanceType"])


				local Name =  tostring(Data["Part"..tostring(fnv)]["Name"])


				Name = Names[WS_Data[tabam]]
				DataText.Text = DataText.Text.."Variables['Instance"..tostring(l).."'] = Instance.new('"..  Classtype  .."');".."Variables['Instance"..tostring(l).."'].Name = '"..tostring(Names["Instance"..tostring(l)]).."'"
				DataText.Text = DataText.Text.."\n"


				for l,f in pairs(ClassValues) do
					coroutine.resume(coroutine.create(function()
						if MainData[f] then
							DataText.Text = DataText.Text.."Variables['Instance"..tostring(fnv+1).."']."..f.." = "..MainData[f]
							DataText.Text = DataText.Text.."\n"	
						end	
					end))
				end

				LoadingBar.Size = UDim2.new((1/tabam)*fnv,0,1,0)	
				DataText.Text = DataText.Text.."\n"


				fnv+=1
			end













			GrabFrame.GeneratingFrame.Gen.Text = "Applying Some More Properties"

			fnv = 1
			for l=1,WeldCount do
				game:GetService("RunService").Stepped:wait()


				LoadingBar.Size = UDim2.new((1/WeldCount)*l,0,1,0)	

				local split = string.split(string.find(WD_Data[WeldData["Weld"..fnv]["Weld"]],"%d+")," ")
				local InstNumber = string.sub(WD_Data[WeldData["Weld"..fnv]["Weld"]],split[1],split[2])

				if WeldData["Weld"..fnv]["Part1"] then
					local data = WD_Data[WeldData["Weld"..fnv]["Part1"].Name]
					local weld = WD_Data[WeldData["Weld"..fnv]["Weld"]]

					local split2 = string.split(string.find(WD_Data[WeldData["Weld"..fnv]["Part1"].Name],"%d+")," ")
					local InstNumber2 = string.sub(WD_Data[WeldData["Weld"..fnv]["Part1"].Name],split2[1],split2[2])


					DataText.Text = DataText.Text.."Variables['"..tostring(string.gsub(weld,"%d+",tostring(tonumber(InstNumber)+1))).."'].Part1 = Variables['".. string.gsub(data,"%d+",InstNumber2+1).."']"


				elseif WeldData["Weld"..fnv]["Part0"] then
					local data = WD_Data[WeldData["Weld"..fnv]["Part0"].Name]
					local weld = WD_Data[WeldData["Weld"..fnv]["Weld"]]


					local split2 = string.split(string.find(WD_Data[WeldData["Weld"..fnv]["Part0"].Name],"%d+")," ")
					local InstNumber2 = string.sub(WD_Data[WeldData["Weld"..fnv]["Part0"].Name],split2[1],split2[2])



					DataText.Text = DataText.Text.."Variables['"..tostring(string.gsub(weld,"%d+",tostring(tonumber(InstNumber)+1))).."'].Part0 = Variables['".. string.gsub(data,"%d+",InstNumber2+1).."']"
				end


				DataText.Text = DataText.Text.."\n"
				fnv+=1

			end









			--[[Parenting]]--


			GrabFrame.GeneratingFrame.Gen.Text = "Parenting Instances"

			fnv = 0
			for l=1,tabam do
				game:GetService("RunService").Stepped:wait()
				local MainData = Data["Part"..tostring(fnv)]
				local Classtype = tostring(Data["Part"..tostring(fnv)]["InstanceType"])
				local Name =  Data["Part"..tostring(fnv)]["Name"]



				local ParentPath = ""
				local StartingPoint = WS_Data[Name]

				if StartingPoint.Parent ~= MDL then
					local split2 = string.split(string.find(WD_Data[StartingPoint.Parent.Name],"%d+")," ")
					local InstNumber2 = string.sub(WD_Data[StartingPoint.Parent.Name],split2[1],split2[2])

					ParentPath = "Variables['"..string.gsub(WD_Data[StartingPoint.Parent.Name],"%d+",InstNumber2+1).."']"
				else
					ParentPath = "workspace"..ParentPath
				end




				DataText.Text = DataText.Text.."Variables['".."Instance"..tostring(l).."'].Parent = "..ParentPath



				LoadingBar.Size = UDim2.new((1/tabam)*fnv,0,1,0)	
				DataText.Text = DataText.Text.."\n"


				fnv+=1

			end

			
			setclipboard(DataText.Text)
			GrabFrame.GeneratingFrame.Gen.Text = "Copied To Clipboard!"
			wait(3)
				UI.GrabberFrame.Transparency =0
				GrabFrame:Destroy()
			GrabbingModel = false
		end
	end
end)
