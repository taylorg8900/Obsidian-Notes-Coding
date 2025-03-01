ARVIS
- interface that lets you simulate your robot?
- this might just be a custom process that sends out info actually
- rviz?
	- this might be the actual program

rectangles are processes, parallelograms are messages?

managers, planners, publishers, sensor readings, state estimator, path follower, world visualization

bunch of things communicating with each other in parallel

intro to ros 5345 is the class name
# intro to ros slides
nodes
- can receive or publish things to other nodes, inputs and outputs
- inter node communiction is 'peer to peer'
- pub/sub
- emphasis on the point that publishers do not care where the data they are publishing go
- publisher -> topic like 'blob' or 'image', basically pick a name -> subscribers
- can turn off publishing if there are no subscribers, to reduce amount of running processes if you want

Services
- synchronous bi directional communication
- request and response
- like a function call, except it is run externally on a separate process or node
- good example is UAV waypoint follower coming up to a final waypoint, requestion a new path from the path planner, and that process might run on a different computer where it is capable of computing that sort of thing
- another example is a process whose job it is to listen for a 'reset' request, and then goes on to reset some state machine
- a single node can have requests, responses, publishes, subscribes, pretty much as modular as you want

Action
- combines both a service and a request (i think)
- periodic feedback
- started with a service, publishes updates, then gives result as a service call
- publishes topics and services together through magic

Parameters
- configures a node
- specific to a single node
- global variable of a program sort of 
- maybe it's like attributes of a class or something 









python3-rostopic? 
- sudo apt install python3 rostopic?
- might be how to install not sure just saw it pop up on his cmd

ros2 topic list goal_poseros2 topic echo /goal_pose