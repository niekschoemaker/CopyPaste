# Commands
**Copy**

/copy NAME options values - Copy a building
Example: /copy home radius 3 method building
Short example: /copy home r 3 m building

Syntax - Options:

*     `each true/false - default: trueCheck radius from each entity`
*     method building/proximity - default: proximity
Choose the type of mechanics to use to copy a building.
Building will only copy the current building.
Proximity will copy by proximity search, current building or not it will copy everything.
*     radius XX - default: 3
Sets the radius to search for entities around each building parts & deployables
*     share true/false - default: false
Set to copy data CodeLocks, BuildingPrivileges, SleepingBag
*     tree true/false - default: false
Set to copy trees and resources

**Paste**

/paste NAME options values - Paste a building
Example: /paste home auth true stability false
Short example: /paste home a true s false

Syntax - Options:

     auth true/false - default: falseAuthorize player in all cupboards
    blockcollision XX - default: 0Checks in XX radius if there is something that could collide with the new building, if so, blocks the build. 0 is to deactivate the detection.
    deployables true/false - default: trueSet to paste the deployables
    height XX - default: 0Adjust height to paste
    inventories true/false - default: trueSet to paste the inventories
    stability true/false - default: trueSet false to ignore stability system
    vending true/false - default: falseSet to paste sellings, name and broadcasting for Vending Machine

**Pasteback**

/pasteback NAME options values - Paste on old place a building where it was when it was saved
Example: /pasteback home auth true stability false
Short example: /pasteback home a true s false

Syntax - Options:

    auth true/false - default: falseAuthorize player in all cupboards
    deployables true/false - default: trueSet to paste the deployables
    inventories true/false - default: trueSet to paste the inventories
    height XX - default: 0Adjust height to pasteback
    stability true/false - default: trueSet false to ignore stability system
    vending true/false - default: falseSet to paste sellings, name and broadcasting for Vending Machine

**Other**

/undo - Removes what you've last pasted
/list - List of stuctures (from folder oxide/data/copypaste)

# Permissions

    copypaste.copy
    copypaste.list
    copypaste.paste
    copypaste.pasteback
    copypaste.undo

# API

TryCopyFromSteamID(ulong userID, string filename, string[] args)
TryPasteFromSteamID(ulong userID, string filename, string[] args)
TryPasteFromVector3(Vector3 pos, float rotationCorrection, string filename, string[] args)

Return string on failure and true on success

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