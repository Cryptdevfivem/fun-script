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
