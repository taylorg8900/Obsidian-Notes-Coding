 
Here is the entire PlayerMovement state manager from the last video
- A lot of this stuff we want to use for NPC's so we want to make it more modular
- There is a lot of state management happening here (this is supposed to be a PlayerMovement script brah) , and it should be in it's own script named 'StateMachine'

```C#
public class PlayerMovement : MonoBehaviour {
	
	public AirState airState;
	public IdleState idleState;
	public RunState runState;
	public State kneelState
	
	State state;
	
	public Animator animator;
	public Rigidbody2D body;
	public BoxCollider2D groundCheck;
	public LayerMask groundMask;
	
	public float acceleration;
	[Range(0f, 1f)]
	public float groundDecay;
	public float maxXSpeed;
	
	public bool grounded { get; private set; }
	public float xInput { get; private set; }
	public float yInput { get; private set; }
	
	void Start() {
		idleState.Setup(body, animator, this);
		runState.Setup(body, animator, this);
		airState.Setup(body, animator, this);
		kneelState.Setup(body, animator, this);
		
		state = idleState;
	}
	
	void Update() {
		CheckInput();
		HandleJumpInput();
		SelectState();
		state.Do();
	}
	
	void SelectState() {
		State oldState = state;
		if (grounded) {
			if (yInput < 0) {
				state = kneelState;
			} else if (xInput == 0) {
				state = idleState;
			} else {
				state = runState;
			}
		} else {
			state = airState;
		}
		
		if (oldState != state || oldState.isComplete) {
			oldState.Exit();
			state.Initialise();
			state.Enter();
		}
	}
	
	void CheckInput() {
		xInput = Input.GetAxis("Horizontal");
		yInput = Input.GetAxis("Vertical");
	}
	
	void HandleXMovement() {
		if (Mathf.Abs(xInput) > 0) {
			float increment = xInput * acceleration;
			float newSpeed = Mathf.Clamp(body.velocity.x + increment, -maxXSpeed, maxXSpeed);
			body.velocity = new Vector2(newSpeed, body.velocity.y);
			
			FaceInput();
		}
	}
	
	void FaceInput() {
		float direction = Mathf.Sign(xInput);
		transform.localScale = new Vector3(direction, 1, 1);
	}
	
	void HandleJumpInput() {
		if (Input.GetButtonDown("Jump") && grounded) {
			body.velocity = new Vector2(body.velocity.x, airState.jumpSpeed);
		}
	}
	
	void CheckGround() {
		grounded = Physics2D.OverlapAreaAll(groundCheck.bounds.min, groundCheck.bounds.max, groundMask).Length >0;
	}
	
	void ApplyFriction() {
		if (grounded && xInput == 0 && body.velocity.y <= 0) {
			body.velocity *= groundDecay;
		}
	}
}
```

Here is the original version of the State which states inherit from as well

```C#
public abstract class State : MonoBehaviour {
	public bool isComplete { get; protected set; }
	protected float startTime;
	public float time => Time.time - startTime;
	
	protected Rigidbody2D body;
	protected Animator animator;
	protected PlayerMovement input;
	
	public virtual void Enter() {}
	public virtual void Do() {}
	public virtual void FixedDo() {}
	public virtual void Exit() {}
	
	public void Setup(Rigidbody2D _body, Animator _animator, PlayerMovement _playerMovement) {
		body = _body;
		animator = _animator;
		input = _playerMovement;
	}
	
	public void Initialise() {
		isComplete = false;
		startTime = Time.time;
	}
}
```
# Creating the StateMachine script, changing PlayerMovement and State, and creating blackboard 'Core'

```C#
public class StateMachine {
	public State state;
	public void Set(State newState, bool forceReset = false) {
		if (state != newState || forceReset) {
			State? Exit();
			state 
		}
	}
}
```

```C#
public class PlayerMovement : Core {
	
	public AirState airState;
	public IdleState idleState;
	public RunState runState;
	public State kneelState
	
	public BoxCollider2D groundCheck;
	public LayerMask groundMask;
	
	public float acceleration;
	[Range(0f, 1f)]
	public float groundDecay;
	public float maxXSpeed;
	
	public bool grounded { get; private set; }
	public float xInput { get; private set; }
	public float yInput { get; private set; }
	
	void Start() {
		
		// Inherited from Core
		SetupInstances();
		machine.Set(idleState);
	}
	
	void Update() {
		CheckInput();
		HandleJumpInput();
		SelectState();
		machine.state.Do();
	}
	
	void SelectState() {

		if (grounded) {
			if (yInput < 0) {
				machine.Set(kneelState);
			} else if (xInput == 0) {
				machine.Set(idleState);
			} else {
				machine.Set(runState);
			}
		} else {
			machine.Set(airState);
		}
	}
	
	void CheckInput() {
		xInput = Input.GetAxis("Horizontal");
		yInput = Input.GetAxis("Vertical");
	}
	
	void HandleXMovement() {
		if (Mathf.Abs(xInput) > 0) {
			float increment = xInput * acceleration;
			float newSpeed = Mathf.Clamp(body.velocity.x + increment, -maxXSpeed, maxXSpeed);
			body.velocity = new Vector2(newSpeed, body.velocity.y);
			
			FaceInput();
		}
	}
	
	void FaceInput() {
		float direction = Mathf.Sign(xInput);
		transform.localScale = new Vector3(direction, 1, 1);
	}
	
	void HandleJumpInput() {
		if (Input.GetButtonDown("Jump") && grounded) {
			body.velocity = new Vector2(body.velocity.x, airState.jumpSpeed);
		}
	}
	
	void CheckGround() {
		grounded = Physics2D.OverlapAreaAll(groundCheck.bounds.min, groundCheck.bounds.max, groundMask).Length >0;
	}
	
	void ApplyFriction() {
		if (grounded && xInput == 0 && body.velocity.y <= 0) {
			body.velocity *= groundDecay;
		}
	}
}
```

```C#
public abstract class State : MonoBehaviour {
	public bool isComplete { get; protected set; }
	protected float startTime;
	public float time => Time.time - startTime;
	
	public virtual void Enter() {}
	public virtual void Do() {}
	public virtual void FixedDo() {}
	public virtual void Exit() {}
	
	public void SetCore(Core _core) {
		core = _core;
	}
	
	public void Initialise() {
		isComplete = false;
		startTime = Time.time;
	}
}
```

Why do we want a Core?
- There are things that we expect every entity to have (Player, NPC, enemy) such as:
	- Rigidbody2D
	- Animator

```C#
public abstract class Core : MonoBehaviour {
	public Rigidbody2D body;
	public Animator animator;
	public PlayerMovement input;
	
	public StateMachine machine;
	
	// Searches through an objects hierarchy, and for each State that it finds will set its core to this
	// Has a constraint that any game object that has states needs to have those states live inside of 
	// it's game object hierarchy but that's pretty reasonable so 
	public void SetupInstances() {
		machine = new StateMachine();
		State[] allChildStates = GetComponentsInChildren<State>();
		foreach (State state in allChildStates) {
			state.SetCore(this);
		}
	}
}
```

I am going to leave these here, since I want to understand the differences between how it works right now with just the player, and after we modify them for the NPC to use

# Creating the NPC



```C#
public class GroundSensor : MonoBehaviour {
	
	public BoxCollider2D groundCheck;
	public LayerMask groundMask;
	public bool grounded { get; private set; }
	
	void FixedUpdate() {
		checkGround();
	}
	void CheckGround() {
		grounded = Physics2D.OverlapAreaAll(groundCheck.bounds.min, groundCheck.bounds.max, groundMask).Length >0;
	}
}
```

```C#
public abstract class Core : MonoBehaviour {
	public Rigidbody2D body;
	public Animator animator;
	
	public GroundSensor groundSensor;
	public StateMachine machine;
	
	// Searches through an objects hierarchy, and for each State that it finds will set its core to this
	// Has a constraint that any game object that has states needs to have those states live inside of 
	// it's game object hierarchy but that's pretty reasonable so 
	public void SetupInstances() {
		machine = new StateMachine();
		State[] allChildStates = GetComponentsInChildren<State>();
		foreach (State state in allChildStates) {
			state.SetCore(this);
		}
	}
	
}
```

```C#
public abstract class State : MonoBehaviour {
	public bool isComplete { get; protected set; }
	protected float startTime;
	public float time => Time.time - startTime;
	
	protected Core core;
	protected Rigidbody2D body => core.body;
	protected Animator animator => core.animator;
	
	
	public StateMachine machine;
	public State parent; // keeping a reference to our parent state lets us traverse up the tree
	public State state => machine.state; //just lets us call it a little more quickly
	
	// Just wrapping the function so we don't have to call machine.Set everytime
	protected void Set(State newState, bool forceReset = false){
		machine.Set(newState, forceReset);
	}
	
	public void SetCore(Core _core) {
		core = _core;
	}
	
	public virtual void Enter() {}
	public virtual void Do() {}
	public virtual void FixedDo() {}
	public virtual void Exit() {}
	
	// First calls Do()
	// If the state has a child, will repeat the Do() call recursively 
	public void DoBranch() {
		Do();
		state?.DoBranch();
	}
	
	public void FixedDoBranch() {
		FixedDo();
		state?.FixedDoBranch();
	}
	
	public void Initialise() {
		isComplete = false;
		startTime = Time.time;
	}
}
```

```C#
public class NPC : Core {
	void Start() {
		SetupInstances();
	}
	
	void Update() {
		if (state.isComplete) {
		
		}
		state.Do();
	}
}
```

```C#
public class StateMachine {
	public State state;
	
	public void Set(State newState, bool forceReset = false) {
		if (state != newState || forceReset) {
			state?.Exit();
			state = newState;
			state.Initialise();
			state.Enter();
		}
	}
}
```

```C#
public class PlayerMovement : Core {
	
	public AirState airState;
	public IdleState idleState;
	public RunState runState;
	public State kneelState
	
	public float acceleration;
	[Range(0f, 1f)]
	public float groundDecay;
	public float maxXSpeed;
	
	
	public float xInput { get; private set; }
	public float yInput { get; private set; }
	
	void Start() {
		
		// Inherited from Core
		SetupInstances();
		machine.Set(idleState);
	}
	
	void Update() {
		CheckInput();
		HandleJumpInput();
		SelectState();
		machine.state.Do();
	}
	
	void SelectState() {

		if (core.groundSensor.grounded) {
			if (yInput < 0) {
				machine.Set(kneelState);
			} else if (xInput == 0) {
				machine.Set(idleState);
			} else {
				machine.Set(runState);
			}
		} else {
			machine.Set(airState);
		}
	}
	
	void CheckInput() {
		xInput = Input.GetAxis("Horizontal");
		yInput = Input.GetAxis("Vertical");
	}
	
	void HandleXMovement() {
		if (Mathf.Abs(xInput) > 0) {
			float increment = xInput * acceleration;
			float newSpeed = Mathf.Clamp(body.velocity.x + increment, -maxXSpeed, maxXSpeed);
			body.velocity = new Vector2(newSpeed, body.velocity.y);
			
			FaceInput();
		}
	}
	
	void FaceInput() {
		float direction = Mathf.Sign(xInput);
		transform.localScale = new Vector3(direction, 1, 1);
	}
	
	void HandleJumpInput() {
		if (Input.GetButtonDown("Jump") && groundSensor.grounded) {
			body.velocity = new Vector2(body.velocity.x, airState.jumpSpeed);
		}
	}
	
	
	
	void ApplyFriction() {
		if (groundSensor.grounded && xInput == 0 && body.velocity.y <= 0) {
			body.velocity *= groundDecay;
		}
	}
}
```




