---
layout: post
title: Reinforcement Learning 
---

### Brief: 

Build a Q-learning agent capable of learning to complete the task of your choice.

### Our Approach:

As a first crack at reinforcement learning (RL), we thought we'd keep it simple and go for the archetypal RL problem, an agent solving a maze. 

In whichever language you prefer (I am using python), there are loads of ready-coded mazes for you out there to choose from - or you can make your own. We were working in python and wanted the ability to generate new mazes to try out with our agent so we opted for [this one](https://gist.github.com/fcogama/3689650). This maze generator is good because it allows you to change the size, density and complexity of the maze you generate. A generated maze will look something like the following, with black pixels representing the walls and white pixels representing the spaces. 

![example](https://artificiallyintelligent.ml/images/example.png "Example Maze")


Now that we have a maze, we need to define a start point and the target. So we defined the start point to be the upper-leftmost space in a given maze and the target to be the lower-rightmost space. Throughout the rest of this post, we will colour the start point in yellow and the target in red. To define the Q-learning model, we need to define a state transition function and reward function. To define these, we need to label each of the spaces in the maze that the agent could occupy. These will be the states of the environment. We start by labeling the start point 0 and assigning the next natural number to each space in the maze from left to right, top to bottom - as if reading a book. We end up with something which looks like this.

![g](https://artificiallyintelligent.ml/images/G.png "Simple Maze")

The actions available to our agent in any given position will be to move to spaces adjacent to its current space, or to stay in the same space. For example the available actions from position 0 are {0,1,5}, the available actions from position 1 are {0,1,2} and so on.

The best way to represent the reward function is in matrix form. To do this, we can [generate an adjacency matrix](https://gist.github.com/amason13/b82eed6b6a3a32a37f7d3117dd8e71e4) from our labeled spaces in the maze, and then set the rewards according to whichever reward function you have choosen. We defined our reward function to award our agent 100 points for reaching the target state, deduce 5 points for staying in the same position, and decude one point for moving positions without reaching the target state. The above maze's reward matrix would look like this. 

![RM](https://artificiallyintelligent.ml/images/RM.png "Reward Matrix")


(Coding this in python, I used -10 in place of the dashes and restricted the agent's choice of actions to indices whose reward is greater than -10.)

There are, of course, infinitely many ways we could have defined our reward function. A common approach is to reward 100 points for reaching the target, and give no rewards or penalties otherwise - and often to restrict the agent from staying in the same state for consecutive time points. We decided not to restrict our agent in this way, as we wanted it to have the same available actions as humans and learn for itself that staying still was ineffective. We included penalties to try and ensure the agent found an optimal solution through the maze rather than accidentally stumbling across a suboptimal one as it explored and converging on that.

Speaking of exploration, when defining a Q-learning problem, we need to choose a learning policy for our agent to implement. The learning policy we opted to use is known as an epsilon greedy one. This means that we pick some number epsilon (between 0 and 1), and tell our agent to explore - ie. choose a random action - with probability epsilon, and choose the action it estimates to be most valuable the rest of the time: the greedy part. At the end of each training episode (when the agent reaches the target), we reduce the value of epsilon a little bit. The idea behind this is that, initially, the agent won't know which actions are valuable and which aren't, so we want it to explore and try out lots of different paths. Then when the agent has reached the target, it should have learnt a little from its experience, so we want it to explore a little less, and exploit its learned knowledge a little more.

There are a handful of parameters in play in Q-learning. Epsilon is one of them, the amount by which we reduce epsilon after each training episode - known as lambda - is another, but you also have the learning rate - alpha, and the discount factor - gamma. Formal definitions are given for them in the [paper](link), but you can think of alpha as the parameter controlling how much learning is done as each action is taken, and gamma as the parameter controlling to what extent future rewards are taken into account. When evaluating our agents performance, we performed a grid search to find the set of parameters which most efficiently found an optimal solution to our maze. 

On the subject of optimality, there was some confusion within our class as to what an optimal solution actually is. Some people were misusing the word optimal to describe the set of parameters which performed best for their task out of the ones they tested. This does **not** mean the solution found under these parameters is optimal! In fact, in some cases it may not even be possible to know whether your solution is optimal or not. There is a [proof](http://users.isr.ist.utl.pt/~mtjspaan/readingGroup/ProofQlearning.pdf) that Q-learning will _eventually_ converge to an optimal solution, but convergence is not guarenteed in any finite number of iterations. This means that without some other metric to test for optimality, we need to be careful when claiming to have found an optimal solution when we actually mean the best solution from the sets of parameters tested.

Fortunately in the case of the maze, we do have another metric to test for optimality. We can represent the maze as a graph and then apply a least path algorithm to find the shortest route from the start point to the target and test this against the path found by our agent. Continuing with the simple maze from above, the graph is shown below. This is a trivial example but shows how optimality can be tested for in this domain.  

![graph](https://artificiallyintelligent.ml/images/graph.png "Graph representation of maze")


We trained our agen over 1000 training episodes in less than 30 seconds, in a 20x20 maze, tested it against the shortest path algorithm (networkx.shortest_path(_graph_,_start_,_end_)) and found that it had successfully found an optimal solution, shown in purple.

![optimal](https://artificiallyintelligent.ml/images/optimal.png "Maze with optimal solution")


We then decided to test how generalisable the trained agent was by dropping it into random starting points and seeing if it could reach the target. We found that the agent had limited success, often failing to reach the target when the starting point was far from the optimal path. To see exactly how generalisable the trained agent is, we systematically dropped the agent at each point in the maze and marked the starting point as green if it could successfully navigate its way out of the maze, and red if it couldn't. (The optimal path is still displayed in purple but this time the target is grey rather than red.)

![colour](https://artificiallyintelligent.ml/images/colour.png "Colourised map of maze generalisability")

As you can see, the agent had little success reaching to the target from much of the maze. Where it did have success, its starting points were close to the optimal path. This acts as a nice reminder that RL agents can be very highly skilled at completing specifical tasks, but the generalisablity of those skills - even in the case of just starting the same task from a different position - can be lacking. 

A really cool project, which I thoroughly enjoyed. I definitely caught the RL bug! 

Full report can be found [here](link).



