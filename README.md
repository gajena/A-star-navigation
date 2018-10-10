A* (pronounced "A - star") is one of the most popular methods for finding the shortest path between two locations in a mapped area.  A* was developed in 1968 to combine heuristic approaches like Best-First-Search (BFS) and formal approaches like Dijsktra's algorithm.

The defining characteristics of the A* algorithm are the building of a "closed list" to record areas already evaluated, a "fringe list" to record areas adjacent to those already evaluated, and the calculation of distances traveled from the "start point" with estimated distances to the "goal point".

The fringe list, often called the "open list", is a list of all locations immediately adjacent to areas that have already been explored and evaluated (the closed list).

The closed list is a record of all locations which have been explored and evaluated by the algorithm.

The heuristic used to evaluate distances in A* is:

f(n) = g(n) + h(n)

where g(n) represents the cost (distance) of the path from the starting point to any vertex n, and h(n) represents the estimated cost from vertex n to the goal.

Euclidean distance (straight line distance) is a common method to used for h(n).

x2 = coordinate of the goal location
x1 = coordinate of the current location
y2 = coordinate of the goal location
y1 = coordinate of current location
dx = | x2 - x1 |
dy = | y2 - y1 |

Distance = sqrt(dx2 + dy2)

The A* algorithm is fairly simple. There are two sets, FRINGE and CLOSED. The FRINGE set contains those nodes that are candidates for examining. Initially, the FRINGE set contains just one element: the starting position. The CLOSED set contains those nodes that have already been examined. Initially, the CLOSED set is empty. Graphically, the FRINGE set is the "frontier" and the CLOSED set is the "interior" of the visited areas. Each node also keeps a pointer to its parent node so that we can determine how it was found.

There is a main loop that repeatedly pulls out the best node n in FRINGE (the node with the lowest f value) and examines it. If n is the goal, then we're done. Otherwise, node n is removed from FRINGE and added to CLOSED. Then, its neighbors n' are examined. A neighbor that is in CLOSED has already been seen, so we don't need to look at it. A neighbor that is in FRINGE will be examined if its f value becomes the lowest in FRINGE. Otherwise, we add it to FRINGE, with its parent set to n. The path cost to n', g(n'), will be set to g(n) + movementcost(n, n').

### Pseudocode
Sometimes things are easier to understand in pseudocode.

Inputs
map
start and goal locations
 

Internal Data

fringe - a list of map locations to be evaluated, in ascending order of estimated distance
closedList - a list of map locations that have been fully evaluated
 

Data Structure

RouteNode, contains

a map location
pointer to this node's parent node
d, the actual distance traveled to reach this node
dPlusL2, which is d + linear distance to goal
 

Search()

Put start node onto fringe
endNode = findRoute()
 

findRoute()

if fringe is empty
// No route exists between start and goal.
return 0
else
node = remove first fringe node (it will have the shortest estimated distance to the goal)
if node's location is the goal
return RouteNode data for current location
else
if node's location is not on the closedList
add node to closedList
addChildrenToFringe(node)
return findRoute()
 

addChildrenToFringe(parentNode)

for all children of parentNode
if child's location is not on closedList
childNode = new RoutNode()
childNode.parent = parentNode
childNode.d = parent.d + linearDistance(parent, child)
L2 = linearDistance(childNode, goal)
childNode.dPlusL2 = childNode.d + L2
Add childNode to fringe, maintaining ascending dPlusL2 order
 

Rendering the Path From the Closed List
After all the iterations, and the goal has been reached, the path is then rendered by backtracking from the goal to start.  This is often done by iterating backward through the closedlist, going from the goal node's parent node to each preceding node's parent until the start is found.
