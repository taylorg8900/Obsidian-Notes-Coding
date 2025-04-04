
# req analysis

provide implementation of the conways game of life thing, refer to wiki link to understand how it works

pay a lot of attention to the four rules of the game
- encode each rule separately

required patterns
 - acorn
 - block
 - blinker
 - glider
 - apparently we encode one state for each pattern, insert it into a simulation, then it will update and do fancy animations and whatever, this means we can choose to insert any state for the pattern and let it rip

each pattern provides an implementation for the following:
```java
public abstract class Pattern {
	public abstract int getSizeX();
	public abstract int getSizeY();
	public abstract boolean getCell(int x, int y);
}
```

LifeSimulator class
- where all of the main code is
- do not add any more public things or change the provided methods either, can add as many private methods as we want
- information about each method in the assingment description

ConwaysLife class
- the `render` method will take the LifeSimulator and render it 

Slides explaining some more stuff I guess:
- cells are booleans which will tell you if the cell is 'alive' or not
- the Pattern classe are just like the templates to set the intial date for the LifeSimulator
- just read values from the Pattern class and put it into the LifeSimulator
- in the LifeSimulator, we go 1. make a completely new grid, then 2. insert a cell into the new grid based on the old grid and if the cell should be alive or not
- if the cell is out of bounds, then it is considered 'dead' unless we are fancy and try to count the other side of the cell as if there were no boundaries like pac-man where it is continuous

looking at the code now
- things we have to do 
	- make the `render(graphics, texSquare, simulation);` line work and take out the `sampleRender(graphics, texSquare);` line 
	- uncomment the `simulation.update();`, make sure that the rules are written so this works
	- in the sampleRender class
		- he says we will make this into the render method? I guess that is what is supposed to happen then
		- make sure to start with `graphics.begin();` and end with `graphics.end();` kind of like drawly
		- don't touch the rBackground
		- don't touch the graphics.draw either

unit tests
- initially all commented out, so that the program compiles before you write code for the tests
- make code then uncomment tests as needed progressively

# pseudocode

first, need to establish the 4 rules
1. live cell with less than two live neighbors dies
2. live cell with 2/3 live neighbors lives
3. live cell with more than 3 neighbors dies
4. dead cell with 3 live neighbors lives

```java
public void update(){
	make a new lifesim with the same size as the one we already have
	
}
```