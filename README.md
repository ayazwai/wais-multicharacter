# WAIS-MULTICHARACTER 
- #### Author: Ayazwai#3900
- #### Linkedin: [Ayaz Ekrem](https://www.linkedin.com/in/ayaz-ekrem-770305212/)
- #### Instagram: [Ayaz Ekrem](https://www.instagram.com/ayaz.ekremm/)
- #### Discord Server: [Wais Development](https://discord.com/invite/YanMPNg8Zn)
- ### Sold exclusively at [0resmon](0resmon.tebex.io) tebex or [Wais Development](https://discord.com/invite/YanMPNg8Zn) Discord.

# WARNING FOR QB!
There is one step that our customers using qb-core need to do. This is an important situation.

- Open the `qb-core > server > player.lua` file.
- Find the `QBCore.Player.CheckPlayerData` function.
- Go to the last line of this function. In the last line of this function you will see the following function. `QBCore.Player.CreatePlayer(PlayerData)`
- If this function is redirected with return, go above it, if there is no return, go below it and paste the following code here. `TriggerEvent('wais:sendNewCharacterData', source, PlayerData.cid, PlayerData.citizenid)`

Old QB Like this:

![alt text](https://media.discordapp.net/attachments/1035485961217384488/1109049664029855784/image.png?width=457&height=73)

New QB Like this

![alt text](https://cdn.discordapp.com/attachments/1035485961217384488/1111405469848842402/image.png)

*When you want to delete a player, do not delete it manually from the players list. You can delete all the player's data from the sql tables using this command /closeslot license license:xxxx slotid. Otherwise, if you delete it manually, some bugs and problems may arise.*

# WARNING FOR ESX!
To use Wais-multicharacter you need to follow these steps.

- Open es_extended -> config.lua
- Here you have to replace esx_multicharacter or other script name in the multicharacter section with wais-multicharacter.
- If the identifiers in the users table do not start with char, you should edit them to start with char. Caution Do this if you do not use multikaracters and never have!
For example:

```
an identifier of the form b350xswkrd9324ssfbawd 
You should change it to char1:b350xswkrd9324ssfbawd. 
```
# APPERANCE'S INTEGRATION

- Find the following functions and organize them according to your own apperance name:
```
FOR QB

function Config.SetPlayerCloth(skinData, ped) -- Client side function
    exports['appearance name']:setPedAppearance(ped, skinData)
end

function Config.CharacterSelected(citizenid) -- Client side function (It is triggered when the character is selected and logged into the server.)
    exports['appearance name']:setPlayerAppearance(json.decode(skinVeriables.skin))

    -- If you are invisible when you select your character, paste these codes.
    -- ↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
    SetEntityVisible(PlayerPedId(), true)
    NetworkSetEntityInvisibleToNetwork(PlayerPedId(), false)
end

function Config.CreateNewCharacter(data) -- Client side function ( Data is player register infos )

        local model = data.gender == 0 and `mp_m_freemode_01` or `mp_f_freemode_01`
        SetEntityCoords(PlayerPedId(), Config.DefaultPedSpawn)

        TriggerServerEvent('QBCore:Server:OnPlayerLoaded')
        TriggerEvent('QBCore:Client:OnPlayerLoaded')

        TriggerServerEvent('qb-houses:server:SetInsideMeta', 0, false)
        TriggerServerEvent('qb-apartments:server:SetInsideMeta', 0, 0, false)

        SetEntityVisible(PlayerPedId(), true)
        TriggerEvent('qb-clothes:client:CreateFirstCharacter')

end
```

```
FOR ESX 

function Config.SetPlayerCloth(skinData, ped) -- Client side function
    exports['appearance name']:setPedAppearance(ped, skinData)
end

function Config.CharacterSelected(identifier, charId) -- Client side function (It is triggered when the character is selected and logged into the server.)
    exports['appearance name']:setPlayerAppearance(json.decode(skinVeriables.skin))

    -- If you are invisible when you select your character, paste these codes.
    -- ↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓
    SetEntityVisible(PlayerPedId(), true)
    NetworkSetEntityInvisibleToNetwork(PlayerPedId(), false)
end

function Config.CreateNewCharacter(data) -- Client side function ( Data is player register infos )
    local model = data.sex == 0 and `mp_m_freemode_01` or `mp_f_freemode_01`
    SetEntityCoords(PlayerPedId(), Config.NewChracterDefaultSpawn.x, Config.NewChracterDefaultSpawn.y, Config.NewChracterDefaultSpawn.z)
    SetEntityVisible(PlayerPedId(), true)

    exports['appearance name']:setPlayerModel(model)
    -- if you not using illenium use this lines
    local config = {
        ped = true,
        headBlend = true,
        faceFeatures = true,
        headOverlays = true,
        components = true,
        props = true,
        allowExit = true,
        tattoos = true
    }
    exports['appearance name']:startPlayerCustomization(function(appearance)
        if appearance then
            TriggerServerEvent('apperancename:server:saveAppearance', appearance)
        end
    end, config)
    -- if you using illenium use this line
    TriggerEvent('esx_skin:openSaveableMenu')
end
```
---

# *What is Config.TransferData?*
Transfer data variable is a variable used to transfer the old player data to the new player if you have the script for the first time. When you get this variable for the first time, run the script after making it `true` 1 time. The script will leave you a message when the player data transfer is finished. When you see this message, change the TransferData variable to `false` and restart the server

# *What is Config.PedCoords?*
The position of the character that appears on the screen when the player enters the server. 
When using, use `vector4(x, y, z, w)`

# *What is Config.DefaultPedSpawn?*

This is where the character will spawn when the player creates a new character. Use `vector3(x, y, z)` when using

# *What is Config.DefaultPedHiddenCoords?*

This is the location where the main character will be hidden when the character screen opens. Update this location with a coordinate close to the location you have set. The usage is `vector3(x, y, z)`

# *Know In Camera Settings*

- cam_defaultCoords = What is far away is the variable of the camera. You should use `vector3(x, y, z)` as coordinate.

- cam_animCoords = The position of the camera approaching the character with animation. Here, the position that is a little closer to the character should be entered. `vector3(x, y, z)`

- spotlight_coords = Make the coordinate the same as the coordinate where the pad is located and move it up a little bit with the z-axis.

- spotlight_coords.**rotation** = It is an up and down adjustment of the light.

- spotlight_coords.**distance** = It is the distance of light.

- spotlight_coords.**radius** = It is the width of the circle that appears when the light hits the ground.

- spotlight_coords.**dirZ** = Well, I don't remember that. I forgot 😅😅

- spotlight_coords.**pov** = It's called the pov of light.

# *What is Config.Animations?*

You can change these special animations that players choose for their characters here.
Example Code 
```
    ["table name"] = { --@string
        ["img"] = "img/animations/tell.png",
        ["flag"] = 1, --@number Animation flag check Natives
        ["anim"] = "amb@world_human_hang_out_street@female_arms_crossed@idle_a", --@string Animation name
        ["anim_dic"] = "idle_c", --@string Animation core name
        ["testTime"] = 3500 --@number
    },
``` 

# *What is Config.NUIJobImages?*

It allows you to display the images you specify for the professions you specify.

```
["jobname"] = { --@string
    ["img"] = "img/jobname.png" --@string
},
```

# *How to do set profile pictures?*

###  For QB:
```
Only use trigger for server
TriggerEvent('wais:setCidPicture', source, cid, url)

source: Number, Player source
cid: Number, Player chracter id
url: String, Image url
```

### For ESX:
```
Only use trigger for server
TriggerEvent('wais:setCharPicture', source, charid, url)
source: Number, Player source
charid: Number, Player character id like char"1":xxxx we need char number
url: String, Image url
```

# *Light flash*

As soon as Multichracter is active, you need to turn off the `SYNC` option of your weather script. 
When the character is selected, that is, when NUIClosed, you need to open `SYNC` again in this function.

Example:

```
function Config.NUIActived() -- Client side function
    TriggerEvent('qb-weathersync:client:DisableSync')
end

function Config.NUIClosed() -- Client side function
    TriggerEvent('qb-weathersync:client:EnableSync')
end
```
