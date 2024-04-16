---
title: Gestión de protecciones
tag: faq
category: faq
---

## 1. ¿Cómo hago que los jugadores puedan proteger gratis?**

Cambia `requires-claim-blocks` a `false` en  [`global.conf`](/wiki/advanced/Global-Config.html) en la sección `creation-settings`.  

## 2. ¿Cómo transfiero una protección de forma gratuita?**

Crea una protección, usa `/claiminfo` -> `Admin Settings` y cambia `Requires Claim Blocks` a false.  
Después usa `/claimtransfer <playername>` para transferir la protección al jugador.  

## 3. ¿Cómo creo una protección usando WorldEdit?**  

Primero asegúrate que la "wand" está en modo "cuboid", ya que GD solo soporta ese modo. Usa la "wand" para seleccionar dos puntos opuestos.  
Si quieres crear una protección en 2D desde la capa de bedrock hasta el cielo, usa `/claimwe`.  

Si quieres crear una protección en 3D que respeta las alturas seleccionadas con WE, entonces usa `/cuboid`, y después `/claimwe`.  
Usando `/cuboid` te activará el modo 3D para las siguientes selecciones, donde la altura se respeta.  

## 4. ¿Cómo uso el mod WECUI visuals con las protecciones de GD?**

Asegúrate de que estás usando la herramienta de investigación (minecraft:stick por defecto) o estás en `/claimmode` y haces clic derecho a un área.

Además, si este click con el palo o con `/claimmode` lo haces mientras pulsas Shift, verás todas las protecciones cercanas.
  
## 5. ¿Cómo permito a todos acceder a mi Spawn?** 

Otorga permiso de acceso a todos usando `/at public` donde "public" representa a todos los jugadores.  
Lee [Sistema de Permiso](/wiki/basic/Trust-System.html).  

Si necesitas una protección más detallada, usa el sistema de Flags.  
Lee [Flag Definitions GUI](/wiki/basic/Flag-Definitions-GUI.html)

## 6. ¿Cómo selecciono una protección específica para hacer cambios? (cambiar configuraciones, etc..)**

La mayoría de los comandos de GD usarán la protección sobre la que te encuentras en ese momento. Simplemente entre en la protección sobre la que quieras hacer un cambio.  
Si la protección está lejos, usa `/claimlist` y teletranspórtate clicando "TP".  

## 7. ¿Cómo puedo hacer pruebas en una protección como un jugador sin permisos?**

Usa `/cfdebug` para entrar en un modo de depuración de Flags y después realiza tu acción.  
Se te tratará como a alguien sin permisos internamente para todas las protecciones. Cuando acabes, simplemente usa `/cfdebug` otra vez.  

## 8. Is there a way to allow a permission within all claims but deny it in the wild?**

  - ### To deny a specific player permission in wilderness

1. Assign permission to all players in LuckPerms.
2. Stand in wilderness claim.
3. Execute command `/cpp <playername> <permission> false`

  - ### To deny a specific group permission in wilderness

1. Assign permission to all players in LuckPerms.
2. Stand in wilderness claim.
3. Execute command `/cpg <group> <permission> false`

Note: The same steps can be applied to any claim.

## 9. How do I stop a player from executing a command in a claim like `/sethome` ?**  

  - ### Deny the permission on a group in claim.  

1. Stand in claim where you want to deny the permission.  
2. Execute command `/cpg <group> <permission> false`  
ex. To deny the permission `essentials.sethome` for group `default`  
`/cpg default essentials.sethome false`  

  - ### Deny the permission on a single player in claim.  

1. Stand in claim where you want to deny the permission.  
2. Execute command `/cpp <playername> <permission> false`  
ex. To deny the permission `essentials.sethome` for player `Mike`  
`/cpp Mike essentials.sethome false`  

  - ### Deny the command-execute flag on a group in claim.  

1. Stand in claim where you want to deny the `command-execute` flag.  
2. Execute command `/cfg <group> command-execute <pluginid:command[arg]> false`  
ex. To deny the essentials command `/sethome` for group `default`  
`/cfg default command-execute essentials:sethome false`  

  - ### Deny the command-execute flag on a single player in claim.

1. Stand in claim where you want to deny the `command-execute` flag.  
2. Execute command `/cfp <playername> command-execute <pluginid:command[arg]> false`  
ex. To deny the essentials command `/sethome` for player `Mike`  
`/cfp Mike command-execute essentials:sethome false`  

Note: Use `/gddebug record claim` to get the proper info for command.  
See [Debugging](/wiki/advanced/Debugging.html) for more info.

## 10. How do I allow my admins to bypass protection ?**  

Grant them access to use the `/ignoreclaims` command in order to toggle GriefDefender god-mode. 

## 11. How do I allow essentials `/sethome` in only claims users are trusted in?**

Run the command `/cf command-execute essentials:sethome false default=user`

## 12. How do I allow players to fly in their own claims?**

1. Deny flight globally in all claims by running command `/claimoption player-deny-flight true default=global`
2. Give players permission to use the `fly` command.
3. Assign the permission `griefdefender.admin.option.perk.fly.owner` to player or group.

## 13. How do I give claim owners the ability to allow other players to fly in their claims?**

1. Admins need to assign all players the following perk permissions
```
griefdefender.admin.option.perk.fly.resident
griefdefender.admin.option.perk.fly.accessor
griefdefender.admin.option.perk.fly.builder
griefdefender.admin.option.perk.fly.container
griefdefender.admin.option.perk.fly.manager
```
Note: Don't forget to run `/gdreload` after changing permissions

These permissions allow the trusted player to fly in claims they are trusted to.

2. Have the claim owners trust players they wish to fly in their claims.

## 14. Is it possible to copy flags from and admin claim to other admin claim?**

1. From the `/gd` menu navigate to `CLAIM` then `CLAIMGROUP`.
2. Click `ADMIN` tab.
3. Click `+` button.
4. Enter claimgroup name.
5. Go to an admin claim that you want joined to group and navigate back to `CLAIMGROUP` in gd menu.
6. Click `ADMIN` tab.
7. Click `JOIN`

Repeat steps 5-7 for each claim you wanted joined to claimgroup.

Once this is complete, setup your flags in any claim joined to claimgroup. All claims in claimgroup will share flags.

Note: Unjoining a claim from a claimgroup will revert the claim back to its local flags.

## 15. How do Geyser players confirm commands?  

They can use the command `/gdconfirm`  


## 16. How do I prevent players from earning blocks while AFK?  

1. Open [`global.conf`](/wiki/advanced/Global-Config.html).  
2. Search for the following section  
```
# The minimum threshold of movement (in blocks) required to receive accrued claim blocks. (Default: 0)
# Note: The claim block task runs every 5 minutes which is the time each player will get to move the required amount of blocks.
claim-block-task-move-threshold=0
```
3. Set `claim-block-task-move-threshold` to the amount of blocks you want to require players to move every 5 minutes to not be considered AFK.  
