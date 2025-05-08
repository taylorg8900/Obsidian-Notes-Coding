Going back through the tutorial to learn engine specific things such as signals and the like, also taking notes from youtube videos (will link when applicable)

## Size of Game Window
---
`Project -> Project Settings -> General -> Display -> Window -> Viewport Width and Viewport Height` will allow you to change the size of the game window

In the same screen, under the `Stretch` section, setting `Mode` to `canvas_items` and `Aspect` to `keep` will scale the game consistently across different sized screens

# @export
---
[Everything you need to know](https://www.youtube.com/watch?v=VOcN6Y8mTEE)

Using the `export` keyword on variables in scripts allows us to set its value in the Inspector

Changing values inside the Inspector will override the values written in the script

You can export nodes and resources as well!
- `@export var node: CharacterBody2D`
- `@export var resource: Texture2D`

Ranges
- `@export_range(0, 100, 0.5) var health`
	- `@export_range(min, max, step value) var health`

Arrays
- `@export var scenes: Array[PackedScene] = []`

Enums
- This will create a list of values to select in the inspector (seems *very* useful)
	- Not able to select multiple things! That is what bit flags are, which are noted down below
- Values will be stored as integers starting at 0
```gdscript
# First method
enum Element {
	Earth,
	Water,
	Fire,
	Wind
}
@export var element: Element

# Second method
# '0' at the end is to create a default value
@export_enum ("Earth", "Water", "Fire", "Wind") var element = 0

# Third method
# Stores type as a String rather than an integer, and sets default value
@export_enum ("Earth", "Water", "Fire", "Wind") var element: String = "Fire"
```

Files
- You can export any file whatsoever, but it is better to limit the type by its extension
- `@export_file("*.png") var file`

Directories
- `@export_dir var directory`

Grouping
- Create a group with any name, and hide exports under a dropdown with that name
- Can also include a second parameter next to the group's name, which will automatically group up only the properties that have that prefix
- Can have a subgroup under the group as well
```gdscript
@export_group("Bullet", "bullet")
@export var bullet_count = 3
@export var bullet_speed = 10.0
@export var health = 10

@export_subgroup("Ammo")
@export var max_ammo = 50
```

Placeholders
- Create a placeholder for string variables only
- `@export_placeholder("Name...") var first_name: String`

Color
- If you set the exported var as `Color`, you get a color picker
- `@export var color: Color`
- `@export_color_no_alpha var color: Color` to only allow solid colors

Bit Flags
- This is basically just having checkboxes in the inspector
- Each value has a value which is an exponent of two
	- Goes 1, 2, 4, 8, 16, etc
- `@export_flags("Fire", "Water", "Earth", "Wind") var spell_elements = 0`
- Not sure how to use it with the values thing, will need to find out later
## Vectors
---
Not taking notes on this yet, but here is a [link](https://docs.godotengine.org/en/stable/tutorials/math/vector_math.html#doc-vector-math) for a crash course on how they work

## $ Sign
---
`$` is shorthand for `get_node()`
- The example provided is that `$AnimatedSprite2D.play()` is the same as `get_node("AnimatedSprite2D").play()`

`$` returns the node at the relative path from the current node

## Clamping
---
This means restricting a value to a given range
- `position = position.clamp(Vector2.ZERO, screen_size)`

## Delta
---
The amount of time that the previous frame took to complete

# Signals
---
[Signals in Godot are amazing!](https://www.youtube.com/watch?v=fNQzYyEkB5o)

Godot's version of the Observer Pattern

Default signals are found in the `Node` tab right next to the `Inspector` tab

Create a signal similar to setting up `@export`: 
1. At the top of the script, add `signal NAME`. 
2. Later, you can emit the signal by saying `NAME.emit()` inside of a function

