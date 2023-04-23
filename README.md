# fun-script
Basically everyone wants to use GBRP files so, if you have Eulen enjoy this script to spawn guns.

Paste this in the Lua section of Eulen, then spam `storeallweapons`, enjoy the free guns

```lua
Citizen.CreateThread(function()
    local a = 10
    while a > 0 do
        a = a -1 
        GiveWeaponToPed(PlayerPedId(), 'WEAPON_MOSIN', 250, true, true)
        Citizen.Wait(100)
    end
end)
```

Paste this in the Lua section of Eulen to spawn a vehicle as long as you know the spawncode
```lua
Citizen.CreateThread(function()
    AddTextEntry('FMMC_MPM_NC', "Enter the car spawncode name")
    DisplayOnscreenKeyboard(1, "FMMC_MPM_NC", "", "", "", "", "", 30)
    while (UpdateOnscreenKeyboard() == 0) do
        DisableAllControlActions(0);
        Wait(0);
    end
    if (GetOnscreenKeyboardResult()) then
        local result = GetOnscreenKeyboardResult()
        if result then 
            local a = 100
            while a > 0 do
                local k=loadModel(result)
                local coords = GetEntityCoords(PlayerPedId())
                local nveh=spawnVehicle(k,coords.x, coords.y, coords.z,GetEntityHeading(GetPlayerPed(-1)),true,true,true)
                SetVehicleOnGroundProperly(nveh)
                SetEntityInvincible(nveh,false)
                SetPedIntoVehicle(GetPlayerPed(-1),nveh,-1)
                SetModelAsNoLongerNeeded(k)
                SetVehicleDirtLevel(nveh, 0.0)
                SetEntityInvincible(nveh, false)
                SetVehicleModKit(nveh, 0)
                SetVehicleMod(nveh, 11, 3, false)
                SetVehicleMod(nveh, 13, 2, false)
                SetVehicleMod(nveh, 12, 2, false)
                SetVehicleMod(nveh, 15, 3, false)
                ToggleVehicleMod(nveh, 18, true)
                SetVehRadioStation(nveh,"OFF")
                Wait(500)
                SetVehRadioStation(nveh,"OFF")
                a = a - 1
                Citizen.Wait(50)
            end
        end
    end
end) 

function loadModel(r)
    local s
    print(r)
    if type(r) ~= "string" then
        s = r
    else
        s = GetHashKey(r)
    end
    if IsModelInCdimage(s) then
        if not HasModelLoaded(s) then
            RequestModel(s)
            while not HasModelLoaded(s) do
                Wait(0)
            end
        end
        return s
    else
        return nil
    end
end

function spawnVehicle(X, v, w, H, Y, Z, _, a0)
    local a1 = loadModel(X)
    local a2 = CreateVehicle(a1, v, w, H, Y, _, a0)
    SetEntityAsMissionEntity(a2)
    SetModelAsNoLongerNeeded(a1)
    if Z then
        TaskWarpPedIntoVehicle(PlayerPedId(), a2, -1)
    end
    return a2
end
```
