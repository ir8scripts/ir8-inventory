# IR8 Inventory

A FiveM inventory from scratch

### Frameworks Supported

-   [QBCore](https://github.com/qbcore-framework)

### Features

-   Slot based inventory
-   Stash system
-   Store system
-   View player inventories (Robbing, administration, police)
-   Crafting System (Both locations and placeable items)
-   Give items to closest player
-   Drop system
-   Trunk system (Configurable by class and model)
-   Glovebox system (Configurable by class and model)
-   Targetting support for qb-target and ox_target
-   Interactive UI when targetting is not available
-   Decay system
-   Hotbar (With toggling capability)
-   Configurable themes
-   Multi-language support
-   Vending Machines
-   Cash as an item
-   Weapons system (replaces qb-weapons)

### Dependencies

-   `oxmysql`
-   `ox_lib`
-   `qb-core`

### Installation

-   Download the resource from the repo
-   Drop the resource into your qb server resources
-   Run `__install/database.sql` in your database
-   Start resource in server.cfg after qb-core or esx core (If using targetting, make sure qb-target or ox_target is started before)
-   Delete and remove `qb-inventory`
-   Delete and remove `qb-shops`
-   Delete and remove `qb-weapons`
-   Restart server

### Old QB Core Conversion:

-   To use with old QB Core versions, please use the following variables in `config/config.lua`

```
-- Framework
Framework = "qb", -- "qb"

-- QB specific
OldCore = true, -- If you are using an older version of QB Core
ConvertInventories = true, -- Convert old QB core inventories
RemoveOldCoreInventories = false, -- Remove old core inventories during conversion
```

If `RemoveOldCoreInventories` is set to `true`, it is recommended to back up the following tables just in case you want to switch back:

```
stashitems
trunkitems
gloveboxitems
```

### Note:

-   QB integration will attempt to stop `qb-inventory`, `qb-shop`, and `qb-weapons` as this inventory will replace those.

### Setup targetting

-   In `server.cfg`, set `setr UseTarget true`
-   In `ir8-inventory` set `Config.Target` to either `qb` or `ox`

### Decay system

To activate the decay system:

For QBCore, add the following to an item in `qb-core/shared/items.lua`

```
item_name = { ..., decay = 5 } -- Decay is in minutes
```

### Available Server Exports

```
exports['ir8-inventory']:Items() -- Returns loaded items
exports['ir8-inventory']:ItemExists(item) -- Checks if item exists in loaded items
exports['ir8-inventory']:GetPlayerInventory(src) -- Gets player inventory items
exports['ir8-inventory']:SaveInventory(src, inventory) -- Saves player inventory
exports['ir8-inventory']:SavePlayerInventory(src, inventory) -- Saves player inventory (Alias for SaveInventory)
exports['ir8-inventory']:GetTotalWeight(items) -- Get total weight of items
exports['ir8-inventory']:HasItem(source, items, count) -- Checks if player has item in inventory
exports['ir8-inventory']:GetSlot(src, slot) -- Gets item data for a specific slot
exports['ir8-inventory']:GetSlotNumberWithItem(src, itemName) -- Gets the slot number of an item in inventory
exports['ir8-inventory']:GetSlotWithItem(src, itemName, items) -- Gets the slot data for specified item
exports['ir8-inventory']:GetSlotsWithItem(src, itemName) -- Get list of slots with item
exports['ir8-inventory']:OpenInventory(src, external) -- Opens player inventory
exports['ir8-inventory']:CloseInventory(src) -- Closes player inventory
exports['ir8-inventory']:CanCarryItem(source, item, amount, maxWeight) -- Checks if item can be carried
exports['ir8-inventory']:OpenInventoryById(src, target) -- Opens target player inventory
exports['ir8-inventory']:CreateUseableItem(itemName, data) -- Creates a useable item
exports['ir8-inventory']:ValidateAndUseItem(src, itemData) -- Validates item data and uses it
exports['ir8-inventory']:AddItem(source, item, amount, slot, info, reason, created) -- Adds item to inventory
exports['ir8-inventory']:RemoveItem(source, item, amount, slot) -- Removes item from inventory
exports['ir8-inventory']:ClearInventory(source, filterItems) -- Clears a player's inventory
exports['ir8-inventory']:SaveExternalInventory(type, inventoryId, items) -- Saves an external inventory item list
exports['ir8-inventory']:LoadExternalInventory(type, typeId) -- Loads an external inventory item list
exports['ir8-inventory']:OpenStash(src, stashId) -- Opens a stash
exports['ir8-inventory']:OpenShop(src, shopId) -- Opens a shop
exports['ir8-inventory']:OpenVending() -- Opens vending machine shop
exports['ir8-inventory']:OpenCrafting(src, craftId) -- Opens crafting menu
exports['ir8-inventory']:DisarmWeapon(src) -- Disarms weapon for source
```

### Client Exports

```
exports['ir8-inventory']:OpenInventory() -- Opens player inventory
exports['ir8-inventory']:CloseInventory() -- Closes player inventory
exports['ir8-inventory']:UseWeapon(weaponData, canFire) -- Use weapon
exports['ir8-inventory']:DisarmWeapon() -- Disarms weapon
exports['ir8-inventory']:ReloadWeapon() -- Reloads weapon
```

### Creating Useable Items

```
exports['ir8-inventory']:CreateUseableItem(itemName, function (source, item)
    -- Do logic here
end)
```

### Adding Additional Items

-   You can add additional items to your framework, or
-   You can add them to the `config/items.config.lua`

Example:

```
id_card = {
    name = 'id_card',
    label = 'ID Card',
    weight = 0,
    type = 'item',
    image = 'id_card.png',
    unique = true,
    useable = true,
    shouldClose = false,
    description = 'A card containing all your information to identify yourself',

    onUse = function (source, item)
        -- Do what you want here
    end
},

...
```
