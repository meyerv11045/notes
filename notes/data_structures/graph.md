**Graph Theory** is the mathematical theory of the properties and applications of graphs/networks

<u>Types of Graphs</u>

**Undirected Graph**- edges have no orientation (i.e. edge (u,v) == edge (v,u) )

**Directed Graph**- edges have orientations (i.e. edge (u,v) is the edge from node u to node v)

**Weighted Graphs**- edges contain a certain weight that represent an arbitrary value such as cost, distance, quantity, etc. (Can be directed or undirected). 

​	Ex: (u, v, w) is the edge from node u to node v with a weight of w

<u>Special Graphs</u>

**Tree** an undirected graph with no cycles (equivalent definition- a connected graph with N nodes and N - 1 edges)

**Rooted Tree** is a tree with a designated root node where every edge either points away from or towards the root node

​	**Arborescence (out-tree)**- edges point away from the root

​	**Anti-arborescence (in-tree)**- edges point towards the root

**Directed Acyclic Graphs (DAGs)**- directed graphs with no cycles. Imporant in representing strctures with dependencies and prerequisites. (All out-trees are DAGs but not all DAGs are out-trees)

**Bipartite Graph**- the vertices can be split into two independent groups U, V such that every edge connects between U and V. Other definitions are- the graph is two colourable or there is no odd length cycle

**Complete Graph**- there is a unique edge between every pair of nodes (complete graph with n vertices is denoted as Kn)

<u>Representing Graphs:</u>

