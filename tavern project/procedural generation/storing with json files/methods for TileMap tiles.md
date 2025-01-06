
to get our information that we store inside the JSON files, we need to store information to be used with the set_cell() function
set_cell(layer:int, coords:Vector2i, source_id:int, atlas_coords:Vector2i)

methods to extract information from tiles placed inside a scene (from TileMap documentation, not TileSet)
	get_cell_atlas_coords(layer:int, coords:Vector2i): Vector2i
	get_cell_source_id(layer:int, coords:Vector2i): int
	get_layers_count(): int
	get_used_cells(layer:int): Array[Vector2i]
	get_used_cells_by_id(layer:int, source_id:int, atlas_coords:Vector2i): Array[Vector2i]
	
layers_amount = tile_map.get_layers_count()
for i in range(layers_amount): # so we can run this for every layer
	array = tile_map.get_used_cells(i)
	for j in len(array):
		# here is where we get information
		# start by i think storing each cell as a key in a dict
		# then store information in the dict
		# something like key: [layer, coords, source_id, atlas_coords]
		# so the key is the cell, and the value is a list containing info that we append to
		.
		# store first value for the key as the layer
		dict[]
	


Methods for TileMapLayer tiles
(since i actually can't access the layer if I'm using TileMapLayers)
methods to extract info
	get_used_cells_by_id(source_id:int, atlas_coords:Vector2i): Array
		use this because I will likely store multiple atlas' for variants of tiles
	get_cell_source_id(coords:Vector2i): int
		use this to find the source id for the cell
	get_cell_atlas_coords(coords:Vector2i): Vector2i
		use this to find the atlas_coords for the cell
method to set cell
	set_cell(coords:Vector2i, source_id:int, atlas_coords:Vector2i)
methods to get info, but in order
	1) get all the cells in the layer, then for each one find it's coords, source_id, and atlas-coords  
	cells = get_used_cells()
	.
	for i in range(len(cells)):
		coords = cells\[i\]
		source_id = tile_map_layer.get_cell_source_id(cells\[i\])
		atlas_coords = tile_map_layer.get_cell_atlas_coords(cells\[i\])
	2) add the information from the methods into a dictionary
		dictionary

ok here is the plan
it seems like i can store information any way I want in JSON files, using arrays and dictionaries together
so the dictionaries would be for each TileMapLayer
'layers' of information
1) which tile map layer we are on (ex. separate for background and foreground)
2) which cell (how do i organize this? just having an increment for each one?)
3) information for each cell
	1) coords
	2) source_id
	3) atlas_coords
TileMapLayer -> Cell # -> {coords:Vector2i, source_id:int,}

example:
{
	"Background_Layer": \[
		{"coords": "(0,0)", "source_id": "0", "atlas_coords": "(0,0)"},
		{"coords": "(1,0)", "source_id": "0", "atlas_coords": "(1,0)"}
		]
}
this way, each cell is a dictionary
each layer maps to a list of dictionaries

for i in range(len(cells)):
	coords = cells\[i\]
	source_id = tile_map_layer.get_cell_source_id(cells\[i\])
	atlas_coords = tile_map_layer.get_cell_atlas_coords(cells\[i\])
	.

ok so i got it working where information about the tiles in the scene are saved in a dictionary, as in [[Screenshot (31).png]] 
next step is to store into a .json file
after doing that, access the .json file and place tiles again using information from it

how to store information into a .json file?
	var data = ...
	var json_string = JSON.stringify(data)
	


