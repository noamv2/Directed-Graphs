<p align = "center"><img src = "https://github.com/noamv2/Directed-Graphs/blob/master/pics/Graph_Calculator%20(1).png">  </p>
<p>
<h2>  Project review</h2>
Graph calculator is a simple GUI app capable of creating, loading, and editing weighted directed graphs. After receiving/loading a graph from a JSON file it can be used as the basis for many graph operations, such as finding the shortest path between two nodes, finding the center, etc...<br>
The manipulated graph can be saved to json file.
</p>
<h2> How to run the calculator</h2>

<p>
To run the calculator you should first create a JSON file that holds a graph. You can check the "data" directory in the main repository to see some examples of graphs files.<br>
Download the jar file found in the top level of the repository, and run it from a terminal using the following command:<br><strong> java -jar Ex2.jar graph.json </strong>, replacing, of course, graph.json with your file name.<br>  
Now you should be looking at a visual representation of your graph.
  
<p align = "center"> <img src = "https://user-images.githubusercontent.com/74304423/145209052-ac8e5f0a-3205-4bb5-80eb-dc56a32618e1.jpg"> </p>
from now on, all the interactions with the app will be done through the GUI.
</p>

<h3>Editing the graph</h3>

![image](https://user-images.githubusercontent.com/74304423/145213867-65247f39-aa98-463a-8203-e546787c2710.png)
<br>
You can change the graph components (Nodes and edges) via the "Edit" tab, all changes will be shown immediatly at the screen.
changes can be save via the "File" tab

<h3>Graph Algorithms</h3>

  ![image](https://user-images.githubusercontent.com/74304423/145225953-fe86dfe1-3990-4652-b1d0-5e9c17a0e78e.png)

  
The calculator provides several operations(algorithms) to run on the graph.

<ul>
  <li><strong>Is connected: </strong> check if the graph is <strong>strongly connected</strong></li>
 
  <li><strong>Shortest path dist: </strong>get a source and destination nodes from the user and return the distance of the shortest path between them</li>
  <li><strong>Shortest path: </strong>get a source and destination nodes from the user and color all the edges of the path with Black (default is red)</li>
  <li><strong>Center: </strong>Mark the Center node of the graph</li>
  <li><strong>Tsp-Traveling salesmen problem: </strong>The calculator receives a list of nodes and returns the shortest path it can find that traverse them all. The user should insert the nodes id separated by comma.</li>
</ul>

<h2>The algorithms behind the scenes</h2>
 
 <ul>
  <li> <strong> Is connected:</strong> Using BFS, we "color" the graph vertices with white, black, and gray starting from an arbitrary node. after The BFS is done we look for white nodes, if no white node is found it means that there is a path from the source node to any other node in the graph. However, this does not guarantee connectivity since we deal we directed graph, so we recolor the nodes with white, reverse all the edges and perform another BFS. 
if again we can't find white nodes then the graph is <strong>Strongly connected</strong>  </li>
  <br>
  <li> <strong>Shortest path - distance: </strong> We use our implementation of Dijkstra's algorithm on the source node, get the resulting distances' array, and simply return the distance to the required vertex </li>
  <li> <strong>Shortest path: </strong>We call Dijkstra's algorithm on the source node, fetch the parents array it returns, and use it to calculate the path to the destination vertex </li>
  <li> <strong> Center: </strong>The implementation is rather simple, we first compute the eccentricity of each node <a href="https://en.wikipedia.org/wiki/Distance_(graph_theory)">(eccentricity:wikipedia) </a> using Dijkstra's algorithm on each vertex and taking the max distance. then, we  pick the vertex with the smallest eccentricy as the center</li>
  
  <li> <strong> Tsp-Traveling salesmen problem: </strong> We start from some random node from the list, perform the Dijkstra algorithm, and travel to the closest Unvisited node from the list, we keep doing that until we reached all the nodes from the list. following this method will yield us a valid path, albeit not necessarily the shortest. we repeat this process for each node in the list, each time picking another vertex as a starting point. in the end we return the shortest path we've found</li>  
</ul>

<h3>Dijkstra's algorithms </h3>
<p> 
 Dijkstra's algorithm played a major part in our work, being part of almost every algorithm. After our first implementation of the algorithm (using regular priority queue) proved to be too slow for our purposes, we implemented it again using a Fibonacci heap. The implementation for Fibonacci is an open-source code that can be found <a href = "https://keithschwarz.com/interesting/code/?dir=fibonacci-heap">here. </a> 
  <br>
  Using the new implementation, we managed to greatly improve our complexity cutting between 70 to 80 percent of the running time. 
  
  <h2>UML diagram</h2>
  
  ![image](https://user-images.githubusercontent.com/74304423/145448408-17f76957-da58-466b-b8db-abb712777f2f.png)

  
</p>
<h2> Running time analysis </h2>
<p> 
  We tested the algorithms on graphs with rising number of nodes to see how efficient they are.
  
![image](https://user-images.githubusercontent.com/91602396/145709328-cc12aa47-34d6-4950-96ab-93990ffcce8f.png)

  ![image](https://user-images.githubusercontent.com/91602396/145709354-5d49b3bc-9d85-4493-8a93-bb7df28f80d4.png)

  
  <br>
  <strong> nodes to visit </strong> = we look for a path containing all these nodes. <br>
  In graphs bigger than 100,000 nodes some of the heavier algorithms run out of memory. 
  <strong>The code was executed on a 5-year-old laptop, on a newer machine the results would be way better </strong>
  
</p>


     

