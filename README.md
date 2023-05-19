# WAIS-MULTICHARACTER 
- #### Author: Ayazwai#3900
- #### Linkedin: [Ayaz Ekrem](https://www.linkedin.com/in/ayaz-ekrem-770305212/)
- #### Instagram: [Ayaz Ekrem](https://www.instagram.com/ayaz.ekremm/)
- #### Discord Server: [Wais Development](https://discord.com/invite/YanMPNg8Zn)
- ### Sold exclusively at [0resmon](0resmon.tebex.io) tebex or Wais Development Discord.

# *What is Config.TransferData?*
Transfer data variable is a variable to transfer the old player data to the new player if you bought the script for the first time. When you get this variable for the first time, run the script after making it `true` for 1 time. The script will leave you a message when the transfer of player data is finished.

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
TriggerEvent('wais:setCidPicture', source, charid, url)
source: Number, Player source
charid: Number, Player character id like char"1":xxxx we need char number
url: String, Image url
```

# WARNING FOR QB!
There is one step that our customers using qb-core need to do. This is an important situation.

- Open the `qb-core > server > player.lua` file.
- Find the `QBCore.Player.CheckPlayerData` function.
- Go to the last line of this function. In the last line of this function you will see the following function. `QBCore.Player.CreatePlayer(PlayerData)`
- If this function is redirected with return, go above it, if there is no return, go below it and paste the following code here. `TriggerEvent('wais:sendNewCharacterData', source, PlayerData.cid, PlayerData.citizenid)`

Like this:

![alt text](https://media.discordapp.net/attachments/1035485961217384488/1109049664029855784/image.png?width=457&height=73)

*When you want to delete a player, do not delete it manually from the players list. You can delete all the player's data from the sql tables using this command /closeslot license license:xxxx slotid. Otherwise, if you delete it manually, some bugs and problems may arise.*
