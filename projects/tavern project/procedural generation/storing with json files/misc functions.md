
[How to save and load data in Godot 4](https://www.youtube.com/watch?v=ybjt_EWyL5U)
documentation sections things that are used in the video:
FileAccess: provides methods for file reading and writing operations
	.store_string
	FileAccess.open 
	FileAccess.file_exists
	.get_as_text
JSON: Helper class for creating and parsing JSON data
	whenever you load an integer, it's actually loaded as a float in Godot so cast it to an int
	.parse
	OK <- this is predefined, something about if parse is successful, it returns OK and result can be retrieved using data
	.get_error_message
	.get_error_line
	.get_data
	
	
people at [this link](https://forum.godotengine.org/t/how-to-store-and-load-json-data/12836/3) are saying that custom resources are very helpful. maybe watching [this video by Pefeper](https://www.youtube.com/watch?v=vzRZjM9MTGw) or [this video by DevWorm](https://youtu.be/zbAKzM-Odb4?si=vT_QwWX7GzWZgVkM) will be good for learning how to use custom resources
im looking at [documentation](https://docs.godotengine.org/en/stable/tutorials/scripting/resources.html#creating-your-own-resources) for custom resources, and maybe using them is better? not sure

var_to_str(variable) converts it into a string, for storing in a JSON file
in GDScript, saying dict = {} and then dict.text will make a key named "text", same as dict\[text\]

const SAVE_FILE_PATH = "user://game_save.save" <- .save is the file extension, can be anything
var save_file = FileAccess.open(SAVE_FILE_PATH, FileAccess.WRITE)
	opens a file at the SAVE_FILE_PATH, in write mode
if save_file == null:
	print("error message")
	return
var json_string = JSON.stringify(save_data)
save_file.store_string(json_string)

if !FileAccess.file_exists(SAVE_FILE_PATH):
	return # if file doesnt exist where the path takes it, return
var save_file = FileAccess.open(SAVE_FILE_PATH, FileAccess.READ)
var json_string = save_file.get_as_text()
var json = JSON.new()

> [!parse_result]
> var parse_result = json.parse(json_string)

if parse_result != OK:
	print("JSON parse error ", json.get_error_message(), "on line", json.get_error_line()))
	return
var save_data = json.get_data()

random notes after watching and copy/pasting the code into godot and messing with it
how does it store and retrieve, and also use the information stored in the JSON file?
	(specifically this video, not how I would do it for the tilemaplayer stuff)
	-it is calling a function for either the saving or loading depending on if player clicks the buttons (this means they aren't ran inside of \_ready)
	-its assigning the .text attribute for the TextEdit node to what is stored in the JSON file
	- its calling the update_color() custom function to update the .modulate attribute for the texturerect
	- its assigning the .position attribute for the texturerect to what is stored
	.
	so basically in here the nodes already all exist, they are just having their attributes such as color and position be updated by what is stored by the keys in the dictionary
other interesting things I didn't know existed:
	in godot, adding a key to a dict can look like dict.key and also dict\["key"\]
	Color.WHITE exists, sort of like saying "white" in pygame
	.size() on an array is like len(array) in python
	.connect(custom_function) to call functions
	the return value (parse_result) is an error code defined in Godot, so sort of like a boolean but not exactly. it's used to check for errors
	json.result is automatically set by the parse() method, is a property, and is filled with the parsed data if the parsing is successful
	use json.get_data() to retrieve json.result, as it is a getter function defined in Godot
	
TLDR: updating attributes for nodes, using what is stored in the JSON file. it doesn't create any new nodes, or save/load information in the \_ready function but instead calls a save() and load() custom function using a .connect method, to call them and save or load information.