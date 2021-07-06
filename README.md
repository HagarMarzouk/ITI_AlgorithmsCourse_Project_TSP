# ITI_AlgorithmsCourse_Project_TSP


This project was delivered to the Algorithms course in ITI, the purpose was to discucc many posible algorithms solutions for  a specific problem, in our case Travel Salesman problem (TSP), and to check the implementation of it.
-The implementation used here is after the Public notebooks: /services/public/dblank / jupyter.cs / FLAIRS-2015

In this project:
## Jupyter Notebook
That is an implementation of four approximate algorithms (Nearest Neighbor, Greedy Algorithm, Divide and conqure and Minimum Spanning Tree) that solve the TSP.
## Presentation 
That is presentt the whole problem from the begining, showing the assumbtions and how to implement the solutions, then discussing each one of the four suggested solution and making a comparison between them at th end.

## Travel Sales Man Problem: 
Given a set of cities and the distances between each pair of cities, what is the shortest possible tour that visits each city exactly once, and returns to the starting city?

The notebook starts with an algorithm that is guaranteed to solve the problem (although it is inefficient for large sets of cities).
> All Tours Algorithm: Generate all possible tours of the cities, and choose the shortest tour (the one with minimum tour length).*


But we will ignore the fully general TSP and concentrate on an important special case, the **Euclidean TSP**, where the straight-line distance between points in a two-dimensional plane is used.

## Here are four general algorithms that were implemented in the notebook:

* **Nearest Neighbor Algorithm**: Make the tour go from a city to its nearest neighbor. Repeat.
* **Greedy Algorithm**: Find the shortest distance between any two cities and include that edge in the tour. Repeat.
* **Divide and Conquer**: Split the input in half, solve the problem for each half, and then combine the two partial solutions.
* **minimum spanning tree**: generate a tour by doing a pre-order traversal, which means the tour starts at the root, then visits all the cities in the pre-order traversal of the first child of the root, followed by the pre-order traversals of any other children.

In addition, three very general strategies that apply not only just to TSP but many optimization problems were applied also. the strategies are:

* **Repetition Strategy**: Take some algorithm and re-run it multiple times, varying some aspect each time, and take the solution with the best score.
* **Alteration Strategy**: Use some algorithm to create a solution, then make small changes to the solution to improve it.
* **Ensemble Strategy**: Take two or more algorithms, apply all of them to the problem, and pick the best solution.

In the notebook atached here, you will find the expansion of these ideas into full algorithms.
