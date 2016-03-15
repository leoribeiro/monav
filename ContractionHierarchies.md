# Introduction #

The plugin utilizes a variant of Contraction Hierarchies to compute routes almost instantaneously.

# Details #
This plugin encapsulates a variant of Contraction Hierarchies http://algo2.iti.kit.edu/english/1087.php. It is a parallelized version similar to Parallel Time-Dependent Contraction Hierarchies http://algo2.iti.kit.edu/english/1366.php. A mobile / external memory approach is adopted from http://algo2.iti.kit.edu/1264.php. A dynamic approach has also been implemented, but no support for traffic information is obtained at the moment.

For a complete understanding of the inner workings of the plugin and routing technique it is advised to read the respective papers and the diploma thesis it is based on. A short overview is given below:

## Parallel Contraction Hierarchies ##
Two concepts are central to this algorithm: _Contraction_ of a node and _shortcut_ edges.

A shortcut edge is an edge which represents a shortest path from a node _u_ to a node _v_.

The contraction of a node _x_ is performed via:
  * remove _x_ and all neighboring edges from the graph and insert them into the final contraction hierarchy graph.
  * for each pair of edges (_u_,_x_) and (_x_,_v_) determine whether the path from _u_ to _v_ over _x_ constitutes a shortest path. If this is the case, insert a new shortcut edge (_u_,_v_) with the combined length
The result is that _x_ is removed from the graph, but all shortest path distances between the remaining nodes are maintained due to the inserted shortcuts.

To compute a Contraction Hierarchy the plugin determines the sets of nodes to contract next via a node priority:
```
 while( graph not empty ) {
  nodes = getIndependentNodes()
  contractNodes( nodes )
 }
```
The node priority is based on simulated contractions and takes into account the current depth in the hierarchy, the proportion of inserted shortcuts and deleted edges, as well as the proportion of original edges.

In the resulting hierarchy a query is performed via a bidirectional Dijkstra's search. Only edges leading to nodes which were contracted after the current node are used. The inserted shortcuts guarantee that the shortest path is found. As the path found may still contain shortcuts, these have to be replaced by the path they represent.
The query has a very limited search space, making it very fast. It is further optimized by a technique called _stall-on-demand_.

## Mobile Graph ##
To accommodate mobile devices a specialized graph is used. The Contraction Hierarchy graph is ordered as a DAG and the node order is further optimized to enhance locality during the query. Then, the graph is compressed into fixed-size blocks. Each block is highly compressed via several compression schemes, while still allowing for random access. Furthermore, for each shortcut it is explicitly stored which path it represents. This allows for efficient access to the disk, reading whole blocks at a time while minimizing the amount of I/O operations necessary for each query.

## Settings ##

  * The block size can be specified. A value of 12 ( = 4KB ) is recommended for flash memory.
  * The amount of threads used during preprocessing can be limited. Only recommended when running out of RAM during preprocessing.

![http://monav.googlecode.com/svn/wiki/images/CHSettings.png](http://monav.googlecode.com/svn/wiki/images/CHSettings.png)