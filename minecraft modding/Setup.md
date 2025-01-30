https://moddingtutorials.org/1.19.2/environment-setup
^ this actually not very useful as it turns out, decided to do the most up to date tutorial i could find instead

# [Getting Started #1](https://www.youtube.com/watch?v=eFofdJ1BYYs&list=PLKGarocXCE1GspJBXQEGuhazihZCSSLmK)
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

# [Custom Items #2](https://www.youtube.com/watch?v=G1ZGToiB9_U&list=PLKGarocXCE1GspJBXQEGuhazihZCSSLmK&index =2)
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

# [Custom Blocks #3](https://www.youtube.com/watch?v=Y2w0PgvABVU&list=PLKGarocXCE1GspJBXQEGuhazihZCSSLmK&index=3)
significantly more confusing/difficult than adding Custom Items

### registering our blocks
---
create new 'block' package, just like the 'item' package
create new 'ModBlocks' class in the 'block' package
	things to hit autocomplete/tab on:
	- DeferredRegister
	- Block ( #important make sure to choose the net.minecraft.world.level.block.Block import statement)
	- ForgeRegistries
	- FirstMod

	public class ModBlocks {
		// a way to register our blocks by using a deferred register
		public static final DeferredRegister<Block> BLOCKS = 
			DeferredRegister.create(ForgeRegistries.BLOCKS, FirstMod.MOD_ID);
		}
		
also need a register method
	autocomplete:
	- IEventBus

	public static void register(IEventBus eventBus) {
		BLOCKS.register(eventBus);
	}

call ModBlocks.register(modEventBus); in our FirstMod class

we also need to register a block item which is associated with that block (what is displayed in inventory)
helper methods
[[Lambda Expressions]]
	autocomplete:
	- RegistryObject
	- BlockItem
	- Supplier

	// will register our block item, which is associated with our block
	// is called in the method directly under this one
	//
	private static <T extends Block> void registerBlockItem(String name, RegistryObject<T> block) {
		ModItems.ITEMS.register(name, () -> new BlockItem(block.get(), new Item.Properties)}

	// used with the variable declaration below to let us use the block and assign properties to it
	// 'Supplier<T> block' parameter is a special type of functional interface from java.util.function
	// it returns an instance of T when called
	// here is an example of using this in a regular java class
	// Supplier<String> stringSupplier = () -> "hello world";
	// System.out.println(stringSupplier.get()); // outputs: hello world
	//
	private static <T extends Block> RegistryObject<T> registerBlock(String name, Supplier<T> block) {
		RegistryObject<T> toReturn = BLOCKS.register(name, block);
		registerBlockItem(name, toReturn);
		return toReturn;
	}

register our block
	
	// this is *variable declaration* and not a method, hence no curly braces after ALEXANDRITE_BLOCK
	// 'static' = belongs to the class, not instances
	// 'public static final' is never a method, always for variable declarations and constants
	//
	public static final RegistryObject<Block> ALEXANDRITE_BLOCK = registerBlock("alexandrite_block",
		() -> new Block(BlockBehaviour.Properties.of()
			.strength(4f).requiresCorrectToolForDrops().sound(SoundType.AMETHYST)));

add our block to the creative mode tab, in FirstMod class, underneath where we have our INGREDIANTS tab logic

	if(event.getTabKey() == CreativeModeTabs.BUILDING_BLOCKS) {
		event.accept(ModBlocks.ALEXANDRITE_BLOCK)
	}

### adding assets
folders we need to add
- add 'blockstates' folder to resources/assets/sockarockeemod folder
- add 'block' folder to resources/assets/sockarockeemod/models folder
- add 'block' folder to resources/assets/sockarockeemod/textures folder

1) in resources/assets/sockarockeemod/blockstates
- add 'alexandrite_block.json'
	- has to match the name that we have for the block in our 'registerBlock' statement in ModBlocks class
- for setting a block down inside the world
- points us to which model to display, when the block gets placed down
```
{
	"variants": {
		"": {
			"model": "sockarockeemod:block/alexandrite_block"
		}
	}
}
```

2) in resources/assets/sockarockeemod/models/block
- add 'alexandrite_block.json'
- looks very similar to the item json file
- this is how minecraft knows what to display when the block exists in the world
```
{
	"parent": "minecraft:block/cube_all",
	"textures": {
		"all": "sockarockeemod:block/alexandrite_block"
	}
}
```
3) in resources/assets/sockarockeemod/textures/block, add the png files for our blocks provided by KaupenJoe

block currently would not have a texture inside of the inventory, or a name, so we also need an item model json file

4) in resources/assets/sockarockeemod/models/item
- add 'alexandrite_block.json'
- basically refers back to the block model json file from step 2
```
{
	"parent": "sockarockeemod:block/alexandrite_block"
}
```

still need a translation

5) in resources/sockarockeemod/lang, add this line under the other ones: `"block.sockarockeemod.alexandrite_block": "Block of Alexandrite"`

# [Custom Creative Mode Tab #4](https://www.youtube.com/watch?v=WoX__Wulx3o&list=PLKGarocXCE1GspJBXQEGuhazihZCSSLmK&index=4)

KaupenJoe likes to create all of the following inside of the 'item' package,  because it has to do with items in the first place and so you 'don't need a separate class'  
Inside src/main/java/net/sockarockee/firstmod/item, create java class `ModCreativeModeTabs`  

ModCreativeModeTabs class
1) need a deferred register 'public static final'
	autocomplete the following:
	- DeferredRegister -> import net.minecraftforge.registries.DeferredRegister;
	- CreativeModeTab -> import net.minecraft.world.item.CreativeModeTab;
	- Registries.CREATIVE_MODE_TAB -> import net.minecraft.core.registries.Registries;
	- FirstMod.MOD_ID -> import net.sockarockee.firstmod.FirstMod;
```
public static final DeferredRegister<CreativeModeTab> CREATIVE_MODE_TABS = 
	DeferredRegister.create(Registries.CREATIVE_MODE_TAB, FirstMod.MOD_ID);
```
2) need a register method to use this with
	autocomplete the following:
	- IEventBus -> import net.minecraftforge.eventbus.api.IEventBus;
```
public static void register(IEventBus eventBus) {
	CREATIVE_MODE_TABS.register(eventBus);
}
```
3) now we call this in our FirstMod class, just like with the items and blocks
```
ModCreativeModeTabs.register(modEventBus);
```
4) now we actually get to adding the creative mode tab
	- can pretty easily modify this to make new creative mode tabs, that have different icons and items inside
	- autocomplete the following:
		- RegistryObject ->                import net.minecraftforge.registries.RegistryObject;
		- CreativeModTab ->              ~~already got imported~~
		- CreativeModeTab.builder() ->  ~~already imported~~
		- ItemStack ->                        import net.minecraft.world.item.ItemStack;
		- Component.translatable -> import net.minecraft.network.chat.Component;
		- 
```
public static final RegistryObject<CreativeModTab> ALEXANDRITE_ITEMS_TAB = 
	CREATIVE_MODE_TABS.register("alexandrite_items_tab",
	() -> CreativeModeTab.builder()
		.icon(() -> new ItemStack(ModItems.ALEXANDRITE.get()))
		.title(Component.translatable("creativetab.sockarockeemod.alexandrite_items")) 
		.displayItems(itemDisplayParamters, output) -> {
			output.accept(ModItems.ALEXANDRITE.get());
			output.accept(ModItems.RAW_ALEXANDRITE.get())
		})
		.build());
```
5) if we make more creative mode tabs, we need to order them properly
	- do this by adding in `withTabsBefore()` method into our code block:
```
public static final RegistryObject<CreativeModTab> ALEXANDRITE_BLOCKS_TAB = 
	CREATIVE_MODE_TABS.register("alexandrite_blocks_tab",
	() -> CreativeModeTab.builder()
		.icon(() -> new ItemStack(ModItems.ALEXANDRITE.get()))
		.withTabsBefore(ALEXANDRITE_ITEMS_TAB.getID())
		.title(Component.translatable("creativetab.sockarockeemod.alexandrite_blocks")) 
		.displayItems(itemDisplayParamters, output) -> {
			output.accept(ModBlocks.ALEXANDRITE_BLOCK.get());
			output.accept(ModBlocks.RAW_ALEXANDRITE_BLOCK.get())
		})
		.build());
```
6) we need a name in the lang folder, and the key needs to match what is in the .title() method above
```
"creativetab.sockarockeemod.alexandrite_blocks": "Alexandrite Blocks"
```

any additional tabs that dont fit, will be added to additional pages at the top of the creative mode inventory like usual