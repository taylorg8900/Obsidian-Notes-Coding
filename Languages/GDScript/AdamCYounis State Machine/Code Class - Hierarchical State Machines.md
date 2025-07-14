[link](https://www.youtube.com/watch?v=Z0fmGAQSQG8&t=1428s)

If I ever want to check out the source code completely its a couple dollars [here](https://uppon-hill.itch.io/indietales-state-machine)

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

![[2025.05.15 hierarchical state machine diagram.PNG]]

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
	
	
	public StateMachine machine; // So that states can have their own statemachines and call states
	public State parent; // keeping a reference to our parent state lets us traverse up the tree
	public State state => machine.state; //just lets us call it a little more quickly
	
	// Just wrapping the function so we don't have to call machine.Set everytime
	protected void Set(State newState, bool forceReset = false){
		machine.Set(newState, forceReset);
	}
	
	public void SetCore(Core _core) {
		machine = new StateMachine();
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
	
	public void Initialise(StateMachine _parent) {
		parent = _parent;
		isComplete = false;
		startTime = Time.time;
	}
}
```

```C#
public class NPC : Core {
	
	public Patrol patrol;
	public Collect collect;
	
	void Start() {
		SetupInstances();
		Set(patrol);
	}
	
	// Same as physics_process in godot, called each frame
	void Update() {
		if (state.isComplete) {
			if(state == collect){
				Set(patrol);
			}
		}
		
		if (state == patrol) {
			collect.checkForTarget();
			if (collect.target != null) {
				Set(collect);
			}
		}
		state.DoBranch();
	}
	void FixedUpdate() {
		state.FixedDoBranch();
	}
}
```

```C#
public class Patrol : State {
	public State navigate;
	public IdleState idle;
	public Transform anchor1;
	public Transform anchor2;
	
	void GoToNextDestination() {
		float randomSpot = Random.Range(anchor1.position.x, anchor2.position.x);
		navigate.destination = new Vector2(randomSpot, core.transform.position.y);
		Set(navigate, true);
	}
	
	public override void Enter() {
		GoToNextDestination();
	}
	
	public override void Do() {
		if (machine.state == navigate) {
			if (navigate.isComplete) {
				Set(idle, true);
				body.velocity = new Vector2(0, body.velocity.y);
			}
		} else {
			if (machine.state.time > 1) {
				GoToNextDestination();
			}
		}
	}
}
```

```C#
public class Navigate : State {
	public Vector2 destination;
	public float speed = 1;
	public float threshold = 0.1f;
	// Leaving this as a state because we don't know if they will walk/fly/crawl whatever
	public State animation;
	
	public override void Enter() {
		Set(animation, true);
	}
	
	public override void Do() {
		if (Vector2.Distance(core.transform.position, destination) < threshold) {
			isComplete = true;
		}
		FaceDestination();
	}
	
	public override void FixedDo() {
		Vector2 direction = (destination - (Vector2)core.transform.position).normalized;
		body.velocity = new Vector2(direction.x * speed, body.velocity.y);
	}
	
	void FaceDestination() {
		core.transform.localScale = new Vector3(Mathf.Sign(body.velocity.x), 1, 1);
	}
}
```

```C#
public class Collect : State {
	public List<Transform> souls;
	public Transform target;
	public Navigate navigate;
	public IdleState idle;
	public float collectRadius;
	public float vision = 1;
	
	public override void Enter() {
		navigate.destination = target.position
		Set(navigate, true);
	}
	
	public override void Do() {
		if (state == navigate) {
			if (CloseEnough(target.position)) {
				Set(idle, true);
				body.velocity = new Vector2(0, body.velocity.y);
				target.gameObject.SetActive(false);
			} else if (!InVision(target.position)) {
				Set(idle, true);
				body.velocity = new Vector2(0, body.velocity.y);
			} else {
				navigate.destination = target.position;
				Set(navigate, true);
			}
		} else { // if we are idling
			if (state.time > 1) {
				isComplete = true;
			}
		}
		
		if (target == null) {
			isComplete = true;
			return;
		}
	}
	
	public override void Exit() {
	
	}
	
	public bool CloseEnough(Vector2 targetPos) {
		return Vector2.Distance(core.transform.position, targetPos) < collectRadius;
	}
	
	public bool Invision(Vector2 targetPos) {
		return Vector2.Distance(core.transform.position, targetPos) < vision;
	}
	
	public Transform CheckForTarget() {
		foreach (Transform soul in souls) {
			if (InVision(soul.position) && soul.gameObject.aciveSelf) {
				target = soul;
				return;
			}
		}
		return null;
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




