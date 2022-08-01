_G.Settings = {
  --player_variables
  ["enabled"] = true,
  ["auto_sell"] = true,
  ["auto_purchase_guillitines"] = true,
  ["auto_upgrade_guillitines"] = true,
 
  --NOTE: really fucking annoying if not true
  ["popups_disabled"] = true,
 
  --script_storage (pls no touchie <3)
  ["plot_object"] = nil
 
}

local tweenService = game:GetService("TweenService")
local replicatedStorage = game:GetService("ReplicatedStorage")

local plots = game:GetService("Workspace").Plots
local localPlayer = game.Players.LocalPlayer
local tweenInfo = TweenInfo.new(0.05, Enum.EasingStyle.Linear)

function setPlotObject()
  _G.Settings["plot_object"] = getPlot()
end

function getPlot()
  for _, plot in ipairs(plots:GetChildren()) do
      if plot.OwnerId.Value == localPlayer.UserId then
          return plot
      end
  end
end

function purchaseGuillotine()
  replicatedStorage.PurchaseGuillotine:FireServer()
end

function upgradeGuillotines()
  replicatedStorage.GoldenGuillotine:FireServer()
end

function disablePopups()
  localPlayer.PlayerGui.PopupAlerts.Frame.Visible = false
end

disablePopups()
setPlotObject()

--Thanks MikeyMikey for the suggestion!

_G.Settings["plot_object"].Heads.ChildAdded:Connect(function(instance)
   if _G.Settings["enabled"] and _G.Settings["auto_sell"] then
       replicatedStorage.DepositHeads:FireServer(math.huge)
       
       --prevent client/server lag
       instance:Destroy()
   end
end)

while _G.Settings["enabled"] do
  if _G.Settings["auto_purchase_guillitines"] then
      purchaseGuillotine()
  end
 
  if _G.Settings["auto_upgrade_guillitines"] then
      upgradeGuillotines()
  end
  wait(0.0001)
end
