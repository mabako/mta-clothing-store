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

shop-system
-----------

Add

```lua
function getFittingSkins()
	return fittingskins
end
```

and export it.
