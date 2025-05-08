[An introduction to finite state machines and the state pattern for game development](https://www.youtube.com/watch?v=-ZP2Xm-mY4E)

Comes from the State Pattern

Benefits of State Pattern
- Instead of  having a big ass block of code that is made of a million if else statements, you can organize your code with some modularity 
- Big ass block of code is super hard to read, error prone, hard to fix bugs, etc etc

Attributes of a State Machine
1. Has a fixed number of states
2. Can only be in one state at a time
3. Each state is responsible for doing one thing
4. The active state receives inputs and responds

How to implement them?

Method one: Use enumerators
- This method is still not super ideal since we still have to manage several variables and timers for different states
- Quick and dirty, good for simple objects that only have a couple states
```
# Using enumerators
class Player:
enum States {
	Idle,
	Walking,
	Falling,
	Jumping
}
var has_double_jumped = false
var current_state = States.Idle

func input(event):
	switch current_state:
		States.Idle:
			input_idling(event)
		States.Walking
			input_walking(event)
		etc...

functions for each state down here
```

Method two: The state pattern
1. Create a generic State interface
2. Implement the interface with a class for each state
3. Let the parent entity delegate logic to the class representing the active state
4. Provide a way for states to transiftion to one another

```
# example 1

# Interface
interface State:
	input(event) -> void
	update(delta) -> void
	
class JumpState implements State:
func input(event) -> void:
	if DOUBLE_JUMP_PRESSED:
		transition to double jump state

func update(delta) -> void:
	velocity.y += gravity * delta
	if velocity.y > 0:
		transition to fall state
	if is_on_ground():
		if MOVE_LEFT_)PRESSED or MOVE_RIGHT_PRESSED
			transition to walk state
		else
			transition to idle state

# Letting the parent entity delegate
class Player:
var active_state = new IdleState()

func input(event) -> void:
	active_state.input(event)
func update(delta) -> void:
	active_state.update(delta)
```

But how do we actually transition?
- The method this video will use is to return a new state to the parent class by returning one of the State implementations, and deleting the old one each time we transition

```
# example 2

# Interface
interface State:
	input(event) -> State
	update(delta) -> State

class JumpState implements State:
func input(event) -> void:
	if DOUBLE_JUMP_PRESSED:
		return new DoubleJumpState()

func update(delta) -> void:
	velocity.y += gravity * delta
	if velocity.y > 0:
		return new FallState()
	if is_on_ground():
		if MOVE_LEFT_)PRESSED or MOVE_RIGHT_PRESSED
			return new WalkState()
		else
			return new IdleState()

# Letting the parent entity delegate
class Player:
var active_state = new IdleState()

func input(event) -> void:
	var new_state = active_state.input(event)
	if new_state:
		delete active_state
		active = new_state
		
func update(delta) -> void:
	var new_state = active_state.update(delta)
	if new_state:
		delete active_state
		active = new_state
```

Adding logic for when we enter or exit a state, so we can update animation, etc
```
# Interface

interface State:
	enter() -> void
	exit() -> void
	input(event) -> State
	update(delta) -> State


# Implementation of the interface

class JumpState implements State:

func enter() -> void:
	play_jump_animation()
	play_jump_sound()
	
func exit() -> void:
	pass
	
func input(event) -> void:
	if DOUBLE_JUMP_PRESSED:
		return new DoubleJumpState()

func update(delta) -> void:
	velocity.y += gravity * delta
	if velocity.y > 0:
		return new FallState()
	if is_on_ground():
		if MOVE_LEFT_)PRESSED or MOVE_RIGHT_PRESSED
			return new WalkState()
		else
			return new IdleState()


# Letting the parent entity delegate

class Player:

var active_state = new IdleState()

func change_state(new_state) -> void:
	active_state.exit()
	delete active_state
	active_state = new_state
	active_state.enter()

func input(event) -> void:
	var new_state = active_state.input(event)
	if new_state:
		delete active_state
		active = new_state
		
func update(delta) -> void:
	var new_state = active_state.update(delta)
	if new_state:
		delete active_state
		active = new_state
```