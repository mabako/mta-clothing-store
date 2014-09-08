mta-clothing-store
==================

Clothing script for MTA:SA

Usage
-----

```lua
setElementModel(player, <gta skin id>)
setElementData(player, 'clothing:id', <custom clothing id>)
```

Modifications
=============

c_shop.lua

* Update to a position of your choice.
* Optionally comment out the click handler.

item-system
-----------

```
	elseif (itemID==16) then -- clothes
		local result = mysql:query_fetch_assoc("SELECT gender,skincolor FROM characters WHERE id='" .. getElementData(source, "dbid") .. "' LIMIT 1")
		local gender = tonumber(result["gender"])
		local race = tonumber(result["skincolor"])
		
		--local skin = tonumber(itemValue)
		local skin, clothingid = unpack(split(tostring(itemValue), ':'))
		skin = tonumber(skin)
		clothingid = tonumber(clothingid) or nil
		if fittingskins[gender] and fittingskins[gender][race] and fittingskins[gender][race][skin] then
			setElementModel(source, skin)
			exports['anticheat-system']:changeProtectedElementDataEx(source, "clothing:id", clothingid, true)
			mysql:query_free( "UPDATE characters SET skin = " .. skin .. ", clothingid = " .. ( clothingid or 'NULL' ) .. " WHERE id = " .. getElementData( source, "dbid" ) )
			triggerEvent('sendAme', source, "changes their clothes.")
		else
			outputChatBox("These clothes do not fit you.", source, 255, 0, 0)
		end
```
shop-system
-----------

Add

```lua
function getFittingSkins()
	return fittingskins
end
```

to `g_shopinfo.lua` and export it.
