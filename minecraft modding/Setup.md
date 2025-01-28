https://moddingtutorials.org/1.19.2/environment-setup
^ this actually not very useful as it turns out, decided to do the most up to date tutorial i could find instead

[Getting Started #1](https://www.youtube.com/watch?v=eFofdJ1BYYs&list=PLKGarocXCE1GspJBXQEGuhazihZCSSLmK)
 - download intellij, JDK, blah blah blah
 - download mdk from forge, did 1.21 version
 - change packet structure name from com.example.examplemod to "net.sockarockee.firstmod"
 - emptied out a lot of methods in the ExampleMod class
 - changed MODID to MOD_ID
 - changed name of class from ExampleMod to FirstMod (this also changed name of class on the left side)
 - MOD_ID = "sockarockeemod", changed from MOD_ID = "examplemod"
	 - can only have lowercase, no dashes, underscores and numbers might be ok
 - gradle.properties file
	 - change mod_id="sockarockeemod"
	 - change mod_version=0.0.1
	 - change mod_group_id=net.sockarockee.firstmod (structure of our packages)
	 - change mod_authors=sockarockee
	 - change mod_description to something
	 - mappings
		 - use parchment mappings, because parameters look like p_035716 without it which is scary
		 - change mapping_channel=parchment
		 - change mapping_version=2024.11.17-1.21.1 (can find for specific version [here](https://parchmentmc.org/docs/getting-started))
		 - copy ParchmentMC maven repository
			 - settings.gradle file
			 - paste the line of code in step 1 from the link above right under the other maven line, to add it
		 - apply the librarian plugin
			 - bulid.gradle file
			 - paste the line of code in step 2 below the ForgeGradle plugin
 - reload gradle by using the elephant icon -> "reload all gradle projects"
	 - this downloads all of the parchment stuff for us
 - download sources in the elephant icon, because i think it won't compile correctly currently? idk
	 - after doing this the classes change, adds a lot of descriptive comments explaining things
	 - can ctrl + left click to explore classes and functions and all that
 - elephant icon -> tasks -> forgegradle runs -> runClient 
	 - will start minecraft up
 - setup github repository

[Custom Items #2](https://www.youtube.com/watch?v=G1ZGToiB9_U&list=PLKGarocXCE1GspJBXQEGuhazihZCSSLmK&index=2)
item package
	right click on our firstmod package, and add another package named "item"
	
add java class to "item" package, name it "ModItems"
	for this next part, here are the things you want to hit tab on to automatically import things with: 
	- DeferredRegister
	- Item
	- ForgeRegistries
	- FirstMod
	other notes
		need the angle brackets to tell it what kind of a register this is (in this case ITEMS)
		these lines of code are saying 'here are our items, make sure they are registered', this works via a deferred register
		deferred registers can work with a lot of things, like creative tabs, items, blocks
		deferred registers are basically lists that are given to minecraft when it is needed (maybe like events?)
		essentially what this does is give minecraft a list of items, which are registered under our MOD_ID
		
	public class ModItems {
		public static final DeferredRegister<Item> ITEMS = 
			DeferredRegister.create(ForgeRegistries.ITEMS, FirstMod.MOD_ID);
	}

next step after creating out ModItems class
	here are the things you want to hit tab on to automatically import things
	- IEventBus
	
	public static void register(IEventBus eventBus) {
		ITEMS.register(eventBus);
	}

now we need to call the register method in our FirstMod class
	under the MinecraftForge.EVENT_BUS.register(this); line in our FirstMod class, add this:

	ModItems.register(modEventBus);

now we can register our item, back in the ModItems class
	tab to autocomplete these things: 
	- RegistryObject
	- Item.Properties
	"public static final" is apparently a convention
	the "()" in "ITEM.register" is a 'supplier', which idk what that is

	public static final RegistryObject<Item> ALEXANDRITE = ITEMS.register("alexandrite",
		() -> new Item(new Item.Properties()));

now we can add our item to the creative mode tab
go back to FirstMod class
go to addCreative method
	this adds our ALEXANDRITE item to the ingrediants tab

	if(event.getTabKey() == CreativeModeTabs.INGREDIANTS) {
		event.accept(ModItems.ALEXANDRITE);
	}

now we can add our name and texture for our item
- go to resources directory, next to our java directory that we have been doing everything in
- add 'assets' directory to 'resources directory'
- add 'sockarockeemod' (MUST match our MOD_ID) folder to 'assets' folder
- add 'lang' folder to 'sockarockeemod' folder
- add 'models' folder to 'sockarockeemod' folder
- add 'textures' folder to 'sockarockeemod' folder
- add 'item' folder to 'models' folder
- add 'item' folder to 'textures' folder
- add 'en_us.json' file to 'lang' folder
	 add this to the en_us.json file
	 gives our item a name that will be displayed to the player

		{
			"item.sockarockeemod.alexandrite": "Alexandrite"
		}
- add 'alexandrite.json' to 'item' folder in 'models' folder
	 add this to the alexandrite.json file
	 the parent part is so that the item in your hand gets extruded a little to make a 3d model
	 the textures part and the item/alexandrite is telling it where to look for the png, so textures -> item -> alexandrite
	 can duplicate this file by doing ctrl + left click + drag, into the parent folder

		{
			"parent": "minecraft:item/generated",
			"textures": {
				"layer0: "sockarockeemod:item/alexandrite"
			}
		}
- add pngs to 'item' folder, in 'textures' folder

summary
	register item 
	add to the creative mode tab
	add a translation
	add the json file which points to our texture

[Custom Blocks #3](https://www.youtube.com/watch?v=Y2w0PgvABVU&list=PLKGarocXCE1GspJBXQEGuhazihZCSSLmK&index=3)

	