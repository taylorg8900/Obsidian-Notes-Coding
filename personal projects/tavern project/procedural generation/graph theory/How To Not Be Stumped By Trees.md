notes from [this website](https://medium.com/basecs/how-to-not-be-stumped-by-trees-5f36208f68a7)

nonlinear data structure

# linear data structures
what makes data linear?
	if there is a sequence and order to how data is constructed, like arrays and linked lists
elements in a linear data structure can only be traverses sequentially

# non-linear data structures
data doesn't follow an obvious order (maybe if you're dumb that is)
you traverse non linear data strctures in a non sequential manner

Trees are made of nodes and links, just like linked lists
trees can have more than just one link, so one node can connect to 2 other ones

# terms
Root: the first node of the tree, doesn't have any edges connecting to it
Edge: the reference that a parent node contains that tells it what its child node is 
Child: any node that has a parent node that links to it
Parent: any node that has a reference or link to another node
Sibling: any group of nodes that are the children of the same node
Internal: any node that has a child node (basically all parent nodes)
Leaf: any node that does not have a child node in the tree, opposite of a root 

data is hierarchical here

# truths
if a tree has n nodes, it will always have one less number of edges (n-1)
trees contain trees inside themselves, called subtrees
	this means they are recursive data structures
	this is why recursive search algorithms are used to search through trees

Depth of a node
	how far away it is from the root
	find by just counting the number of links that it took to reach that node from the root node
Height of a node
	how far the node is from its furthest-away leaf

Balanced
	if any two sibling subtrees do not differ in height by more than one level
	i.e. if the height of the two sibling nodes are about the same
	mention of something called Binary Trees, notes in [[Leaf It Up To Binary Trees]]
Unbalanced
	if any two sibling nodes have a significantly different height value

Examples
	File structures in computers and stuff
	object oriented languages, main Object and classes that inherit from it