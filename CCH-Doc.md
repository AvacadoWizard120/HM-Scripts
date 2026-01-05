This is just a utility for quirrel scripters to create more robust commands for their modules :man_shrugging: 
I'll add more documentation soon enough. For now, I've got some snippets from my Bomb Vest module, which can be found [here](https://discord.com/channels/1321476389815324733/1457687169283133523)


You can initialize it as a soft dependency or a required dependency. Here is an example of how to initialize custom commands helper as a soft dependency:

```bash
local CCH

if ("cch" in getconsttable()) {
	print("Custom Command Helper found!")
	CCH = getconsttable()["cch"]
} else {
	print("Custom Command Helper NOT FOUND! Commands will be disabled.")
	CCH = null
}
```

Here's an example of how you can require a specific version of cch in your module:
```lua
	if (GetModuleVersionString("Custom Command Helper") == "1.3" && IsModuleLoaded("Custom Command Helper")) {
		// If the installed version of cch meets the required version
	} else {
		print("This module requires Custom Command Helper version " + cchVersion + ", yours is " + GetModuleVersionString("Custom Command Helper") + "  | Commands disabled...")
	}
```


Here's an example of how you can register a command that takes an optional boolean argument:
```lua
function registerCommands() {
	if (CCH != null) {
	    -- you must register the namespace for your module using the registerNamespace function, it takes 2 string arguments; the namespace itself, and a description of your module.
		CCH.registerNamespace(nameSpace, "[Bomb Vest v" + GetModuleVersionString("Bomb Vest") + "] -> Press Interact to Explode! Made by ConfusingFool93 :)")

		CCH.registerCommand(
			nameSpace, -- The namespace of your module (string)
			"requireUniform", -- the command you want to register (string)
			"Require the bomber uniform to be equipped by the player | [optional: true/false]", -- a brief description of the command (string)
			[
				["bool", "action", false] -- a table of arguments the command takes, each argument is registered as an array [type (string), "action", required (bool)]
			],
			function(parsed) { -- a function to run when the command is entered
				if ("action" in parsed) {
					requireUniform = parsed.action
					if (requireUniform) {
						print("[Bomb Vest] Require bomber uniform Enabled!")
					} else {
						print("[Bomb Vest] Require bomber uniform Disabled!")
					}
				} else {
					print("[Bomb Vest] Require bomber uniform = " + requireUniform)
				}
			}
		)
	}
}
```

- Each command will be registered to the Heated Metal console as namespace.command
  If I register my module's namespace as "bv" (Bomb Vest module), and I have a command called "requireUniform", then I would have to input it into the console like "bv.requireUniform" and then follow that up with any arguments your command takes. "bv.requireUniform true"
