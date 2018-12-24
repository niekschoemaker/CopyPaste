# Commands
**Copy**

```
/copy NAME options values - Copy a building
Example: /copy home radius 3 method building
Short example: /copy home r 3 m building
```

<u>Syntax - Options:</u>

* **each true/false** - *default: true* - Check radius from each entity

* **method building/proximity** - *default: proximity* - Choose the type of mechanics to use to copy a building.</br>
     **Building**: Only copy the current building.</br>
     **Proximity**: Copy all blocks close to the building. (Some deployables can be missing with Building also use proximity in these cases)

* **radius XX** - *default: 3* - Sets the radius to search for entities around each building parts & deployables

* **share true/false** - *default: false* - Set to copy data CodeLocks, BuildingPrivileges, SleepingBag

* ** tree true/false** - *default: false* - Set to copy trees and resources


**Paste**

```
/paste NAME options values - Paste a building
Example: /paste home auth true stability false
Short example: /paste home a true s false
```

<u>Syntax - Options:</u>

* **auth true/false** - *default: false* - Authorize player in all cupboards
* **blockcollision XX** - *default: 0* - Checks in XX radius if there is something that could collide with the new building, if so, blocks the build. 0 is to deactivate the detection.
* **deployables true/false** - *default: true* - Set to paste the deployables
* **height XX **- *default: 0 *- Adjust height to paste
* **inventories true/false** - *default: true* - Set to paste the inventories
* **stability true/false** - *default: true* - Set false to ignore stability system
* **vending true/false** - *default: false* - Set to paste sellings, name and broadcasting for Vending Machine

**Pasteback**

/pasteback NAME options values - Paste on old place a building where it was when it was saved
Example: /pasteback home auth true stability false
Short example: /pasteback home a true s false

<u>Syntax - Options:</u>

* **auth true/false** - *default: false* - Authorize player in all cupboards
* **deployables true/false** - *default: true* - Set to paste the deployables
* **inventories true/false **- *default: true* - Set to paste the inventories
* **height XX** - *default: 0* - Adjust height to pasteback
* **stability true/false** - *default: true* - Set false to ignore stability system
* **vending true/false** - *default: false* - Set to paste sellings, name and broadcasting for Vending Machine

**Other**

/undo - Removes what you've last pasted
/list - List of stuctures (from folder oxide/data/copypaste)

# Permissions

* copypaste.copy
* copypaste.list
* copypaste.paste
* copypaste.pasteback
* copypaste.undo

# API
```
object TryCopyFromSteamID(ulong userID, string filename, string[] args)
object TryPasteFromSteamID(ulong userID, string filename, string[] args)
object TryPasteFromVector3(Vector3 pos, float rotationCorrection, string filename, string[] args)
```

Returns string on failure and true on success

Example:
```
bool BuyBuilding(BasePlayer player, string buildingName)
{
    var options = new List<string>{ "blockcollision", "true" };

    var success = CopyPaste.Call("TryPasteFromSteamID", player.userID, buildingName, options.ToArray());

    if(success is string)
    {
        SendReply(player, "Can't place the building here");

        return false;
    }

    SendReply(player, "You've successfully bought this building");

    return true;
}
```