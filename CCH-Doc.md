This is just a utility for quirrel scripters to create more robust commands for their modules :man_shrugging: 
I'll add more documentation soon enough. For now, I've got some snippets from my Bomb Vest module, which can be found [here]()


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
		CCH.registerNamespace(nameSpace, "[Bomb Vest v" + GetModuleVersionString("Bomb Vest") + "] -> Press Interact to Explode! Made by ConfusingFool93 :)")

		CCH.registerCommand(
			nameSpace,
			"requireUniform",
			"Require the bomber uniform to be equipped by the player | [optional: true/false]",
			[
				["bool", "action", false]  // Changed from "string" to "bool"
			],
			function(parsed) {
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
