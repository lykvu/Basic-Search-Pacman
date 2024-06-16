PROJECT OVERVIEW - 
In this project, your Pacman agent will find paths through his maze world, both to reach a particular location and to collect food efficiently. You will build general search algorithms and apply them to Pacman scenarios.

This project includes an autograder to grade your answers on your machine. This can be run
with the command: python autograder. py

FILES TO EDIT -
1) search.py - Where all the search algorithms will reside.
2) searchAgents.py - Where all the search-based agents will reside.

FILES TO LOOK AT -
1) pacman.py - The main file that runs Pacman games. This file describes a Pacman GameState type,
which you use in this project.
2) game.py - The logic behind how the Pacman world works. This file describes several supporting types like AgentState, Agent, Direction, and Grid.
3) util.py - Useful data structures for implementing search algorithms.

QUESTIONS -
1) Finding a Fixed Food Dot using Depth First Search - In searchAgents.py, you’ll find a fully implemented SearchAgent, which plans out a path through Pacman’s world and then executes that path step-by-step. The search algorithms for formulating a plan are not implemented – that’s your job.
First, test that the SearchAgent is working correctly by running -
python pacman.py -l tinyMaze -p SearchAgent -a fn= tinyMazeSearch
The command above tells the SearchAgent to use tinyMazeSearch as its search algorithm, which
is implemented in search.py. Pacman should navigate the maze successfully.

2) Breadth First Search (BFS) - Implement the breadth-first search (BFS) algorithm in the breadthFirstSearch function in search.py. Again, write a graph search algorithm that avoids expanding any already visited states. Test your code the same way you did for depth-first search.
python pacman.py -l mediumMaze -p SearchAgent -a fn=bfs
python pacman.py -l bigMaze -p SearchAgent -a fn=bfs -z . 5

3) Varying the Cost Function - While BFS will find the fewest action paths to the goal, we might want to find paths that are “best” in other senses. Consider mediumDottedMaze and mediumScaryMaze.
By changing the cost function, we can encourage Pacman to find different paths. For example, we
can charge more for dangerous steps in ghost-ridden areas or less for steps in food-rich areas, and a rational Pacman agent should adjust its behavior in response.
Implement the uniform-cost graph search algorithm in the uniformCostSearch function in search.py.
Look through util.py for some data structures that may be useful in your implementation. You should now observe successful behavior in all three of the following layouts, where
the agents below are all UCS agents that differ only in the cost function they use (the agents and cost functions are written for you):
python pacman.py -l mediumMaze -p SearchAgent -a fn=ucs
python pacman.py -l mediumDottedMaze -p StayEastSearchAgent
python pacman.py -l mediumScaryMaze -p StayWestSearchAgent

4) A* Search - Implement A* graph search in the empty function aStarSearch in search.py. A* takes a heuristic function as an argument. Heuristics take two arguments: a state in the search problem (the main argument), and the problem itself (for reference information). The nullHeuristic heuristic function in search.py is a trivial example.
You can test your A* implementation on the original problem of finding a path through a maze to a fixed position using the Manhattan distance heuristic (implemented already as manhattanHeuristic in searchAgents.py).
python pacman.py -l bigMaze -z . 5 -p SearchAgent -a fn=astar ,
heuristic = manhattanHeuristic

5) Finding All the Corners - The real power of A* will only be apparent with a more challenging search problem. Now, it’s time to formulate a new problem and design a heuristic for it.
In corner mazes, there are four dots, one in each corner. Our new search problem is to find the
shortest path through the maze that touches all four corners (whether the maze actually has food
there or not). Note that for some mazes like tinyCorners, the shortest path does not always go to the closest food first! Hint: the shortest path through tinyCorners takes 28 steps.
Implement the CornersProblem search problem in searchAgents.py. You will need to choose a
state representation that encodes all the information necessary to detect whether all four corners have been reached. Now, your search agent should solve:
python pacman.py -l tinyCorners -p SearchAgent -a fn=bfs ,
prob = CornersProblem
python pacman.py -l mediumCorners -p SearchAgent -a fn=bfs ,
prob = CornersProblem

6) Corners Problem - Heuristic
Implement a non-trivial, consistent heuristic for the CornersProblem in cornersHeuristic.
python pacman.py -l mediumCorners -p AStarCornersAgent -z 0 . 5
