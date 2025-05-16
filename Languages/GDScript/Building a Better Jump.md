[video](https://www.youtube.com/watch?v=hG9SzQxaCm8)

How do we define our jump
- We should start by knowing certain parameters, like how high we are jumping instead of tweaking gravity and jump force values, which are sort of 'magic numbers'

One solution for finding what gravity should be, if we know our desired height and the time it takes for the jump to complete
![[2025.05.10 jump1.PNG]]

The two formulas for finding initial velocity and gravity. Velocity is 2* height of jump / time
![[2025.05.10 jump2.PNG]]

"Now we are going to start talking about the horizontal distance that we cover on the way to the peak of the jump and we're also going to be talking about our foot speed. You can pick two of these but the third one necessarily has to be a function of the other two so for my money I think it makes the most sense to define the horizontal distance to the peak of the jump and to find the foot speed and allow the duration of the jump to be a function of those, just because when we're talking about the duration of a jump usually we're talking about fractions of a second and that's not necessarily the most intuitive thing to speak about or the most intuitive thing to design upfront"

![[2025.05.10 jump3.PNG]]

Equations
- Variables
	- `t sub h` = time to reach height of jump
	- `x sub h` = horizontal distance to height of jump
	- `v sub x` = foot speed, or x velocity
	- `v sub 0` = initial y velocity
	- `h` = height of jump
	- `g` = gravity
- (time to peak of jump) = (horizontal distance to peak of jump) / (x velocity)
- (initial y velocity) = (2 * height of jump) / (time to reach height of jump)
- (gravity) = (-2 * height of jump) / (time to reach height of jump * time to reach height of jump)
- (initial y velocity) = (2 * height of jump * x velocity) / (horizontal distance to peak of jump)
- (gravity) = (-2 * height of jump * (x velocity * x velocity)) / (horizontal distance to peak of jump * horizontal distance to peak of jump)

![[2025.05.10 jump4.PNG]]




 I found this simplified [video](https://www.youtube.com/watch?v=IOe1aGY6hXA) which summarizes the above one quite nicely and quickly but doesn't talk about variable jump height so yeah