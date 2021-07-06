# ITI_AlgorithmsCourse_Project_TSP

This notebook  is an implementation of four approximate algorithms (Nearest Neighbor, Greedy Algorithm, Divide and conqure and Minimum Spanning Tree) that solve the problem of Travel Sales Man problem (TSP)
This project was delivered to the Algorithms course in ITI, the purpose was to discucc many posible algorithms solutions for  a specific problem, in our case the TSP, and to check the implementation of it. The implementation used hear is used after the Public notebooks: /services/public/dblank / jupyter.cs / FLAIRS-2015


Travel Sales Man Problem: 
Given a set of cities and the distances between each pair of cities, what is the shortest possible tour that visits each city exactly once, and returns to the starting city?

Vocublary : 

- **A set of cities**: We will need to represent a set of cities; Python's `set` datatype might be appropriate.
- **Distance between each pair of cities**: If `A` and `B` are cities, this could be a function, `distance(A, B),` or a table lookup, `distance[A][B]`.  The resulting distance will be a real number.
- **City**: All we have to know about an individual city is how far it is from other cities. We don't have to know its name, population, best restaurants, or anything else. So a city could be just an integer (0, 1, 2, ...) used as an index into a distance table, or a city could be a pair of (x, y) coordinates, if we are using straight-line distance on a plane.
- **Tour**: A tour is a specified order in which to visit the cities; Python's `list` or `tuple` datatypes would work. For example, given the set of cities `{A, B, C, D}`, a tour might be the list `[B, D, A, C]`, which means to travel from `B` to `D` to `A` to `C` and finally back to `B`.
- **Shortest possible tour**: The shortest tour is the one whose tour length is the minimum of all tours.
- **Tour length**: The sum of the distances between adjacent cities in the tour (including the last city to the first city).   Probably  a function, `tour_length(tour)`.
- **What is ...**: We can define a function to answer the question *what is the shortest possible tour?*  The function takes a set of cities as input and returns a tour as output. I will use the convention that any such function will have a name ending in the letters "`tsp`", the traditional abbreviation for Traveling Salesperson Problem.

At this stage I have a rough sketch of how to attack the problem.  I don't have all the answers, and I haven't committed to specific representations for all the concepts, but I know what all the pieces are, and I don't see anything that stops me from proceeding.


Let's start with an algorithm that is guaranteed to solve the problem (although it is inefficient for large sets of cities). Here is a sketch of the algorithm:
> All Tours Algorithm: Generate all possible tours of the cities, and choose the shortest tour (the one with minimum tour length).*



But we will ignore the fully general TSP and concentrate on an important special case, the **Euclidean TSP**, where the distance between any two cities is the [Euclidean distance](http://en.wikipedia.org/wiki/Euclidean_distance), the straight-line distance between points in a two-dimensional plane. So a city can be represented by a two-dimensional point: a pair of *x* and *y* coordinates. We will use the constructor function `City`, so that `City(300, 0)` creates a city with x-coordinate of 300 and y coordinate of 0.  Then `distance(A, B)` will be a function that uses the *x* and *y* coordinates to compute the distance between `A` and `B`.

Representing Points and Computing `distance`
---
        
OK, so a city can be represented as just a two-dimensional point. But how will we represent points?  Here are some choices, with their pros and cons:

* **tuple:** A point is a two-tuple of (*x*, *y*) coordinates, for example, `(300, 0)`. **Pro:** Very simple. 
**Con:** doesn't distinguish Points from other two-tuples.  
            
* **class:** Define a custom `Point` class with *x* and *y* slots. **Pro:** explicit, gives us `p.x` and `p.y` accessors.  **Con:** less efficient.
            
* **complex:** Python already has the two-dimensional point as a built-in numeric data type, but in a non-obvious way: as `complex` numbers, which inhabit the two-dimensional (real &times; imaginary) plane.  **Pro:** efficient. **Con:** a little confusing; doesn't distinguish Points from other complex numbers.


Any of these choices would work perfectly well; I decided to use complex numbers and to implement the functions `X` and `Y` to make things less confusing. An advantage of `complex` numbers is that computing the distance between two points is easy&mdash;the absoute value of their difference:





Here are two general plans of how to create a tour:

* **Nearest Neighbor Algorithm**: Make the tour go from a city to its nearest neighbor. Repeat.
* **Greedy Algorithm**: Find the shortest distance between any two cities and include that edge in the tour. Repeat.

We will expand these ideas into full algorithms.

In addition, here are four very general strategies that apply not just to TSP, but to any optimization problem. An **optimization problem** is one in which the goal is to find a solution that is best (or near-best) according to some metric,
out of a pool of many candidate solutions. The strategies are:

* **Repetition Strategy**: Take some algorithm and re-run it multiple times, varying some aspect each time, and take the solution with the best score.
* **Alteration Strategy**: Use some algorithm to create a solution, then make small changes to the solution to improve it.
* **Ensemble Strategy**: Take two or more algorithms, apply all of them to the problem, and pick the best solution.

And here are two more strategies that work for a wide variety of problems:

* **Divide and Conquer**: Split the input in half, solve the problem for each half, and then combine the two partial solutions.
