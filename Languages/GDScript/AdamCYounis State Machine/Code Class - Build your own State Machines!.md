[link](https://www.youtube.com/watch?v=-jkT4oFi1vk)

Component Based State Machine

Blackboard (some term to look up later, mentioned around 26:30)

Essentially he has an update function inside of the PlayerMovement that will select new states if whichever state currently selected has its `isComplete` set to true, and it looks like this right now
- This is different than what I have because the decision for which state to enter is handled up here instead of inside the individual states

```C#
void Update() {
	CheckInput();
	HandleJumpInput();
	if (state.isComplete) {
		SelectState();
	}
	state.Do();
}
void SelectState() {
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
	state.Initialise();
	state.Enter();
}
```

After that, he talks about being able to interrupt states through input, and he changes it to look like this instead

```C#
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
```


```C#
public class PlayerMovement : MonoBehaviour {}
```


```C#
public abstract class State : MonoBehaviour {
	
	public bool isComplete {
		get;
		protected set;
	}
	
	protected float startTime;
	public float time => Time.time - startTime;
	
	protected Rigidbody2D body;
	protected Animator animator;
	protected PlayerMovement input;
	
	public virtual void Enter() {
	
	}
	public virtual void Do() {
	
	}
	
	public virtual void FixedDo() {
	
	}
	public virtual void Exit() {
	
	}
	
	public void Setup(Rigidbody2D _body, Animator _animator){
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

```C#
public class AirState : State {
	
	public float jumpSpeed;
	
	
	public override void Enter(){
		animator.Play("Jump");
	}
	
	public override void Do() {
		float time = Map(body.velocity.y, jumpSpeed, -jumpSpeed, 0, 1, true);
		animator.Play("Jump", 0, time);
		animator.speed = 0;
		
		if (input.grounded) {
			isComplete = true;
		}
	}
	
	public override void Exit() {
	
	}

}
```