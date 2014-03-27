DijkstraAlgorithm
=================

DijkstraAlgorithm
/*
 * Dijkstra’s Algorithm
- It is a graph search algorithm that solves 
the single-source shortest path problem for 
a graph with nonnegative edge path costs, 
producing a shortest path tree
- For a given source node in the graph, the 
algorithm finds the path with lowest cost 
(i.e. the shortest path) between that node 
and every other node
 * 
 */
 
 
 Reference 1:   http://www.vogella.com/tutorials/JavaAlgorithmsDijkstra/article.html#dijkstra_overview
 Reference 2:   http://blog.csdn.net/javaman_chen/article/details/8254309
 
 
Test:
The following is a small JUnit Test to validate the correctness of the algorithm.

package dijkstra;

import static org.junit.Assert.*;

import org.junit.Test;

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

import dijkstra.DijkstraShortPath;
import dijkstra.Edge;
import dijkstra.Graph;
import dijkstra.Vertex;

public class TestDijkstraAlgorithm {

  private List<Vertex> nodes;
  private List<Edge> edges;

  @Test
  public void testExcute() {
    nodes = new ArrayList<Vertex>();
    edges = new ArrayList<Edge>();
    for (int i = 0; i < 11; i++) {
      Vertex location = new Vertex("Node_" + i, "Node_" + i);
      nodes.add(location);
    }

    addLane("Edge_0", 0, 1, 85);
    addLane("Edge_1", 0, 2, 217);
    addLane("Edge_2", 0, 4, 173);
    addLane("Edge_3", 2, 6, 186);
    addLane("Edge_4", 2, 7, 103);
    addLane("Edge_5", 3, 7, 183);
    addLane("Edge_6", 5, 8, 250);
    addLane("Edge_7", 8, 9, 84);
    addLane("Edge_8", 7, 9, 167);
    addLane("Edge_9", 4, 9, 502);
    addLane("Edge_10", 9, 10, 40);
    addLane("Edge_11", 1, 10, 600);

    // Lets check from location Loc_1 to Loc_10
    Graph graph = new Graph(nodes, edges);
    DijkstraShortPath dijkstra = new DijkstraShortPath(graph);
    dijkstra.execute(nodes.get(0));
    LinkedList<Vertex> path = dijkstra.getPath(nodes.get(10));
    
    assertNotNull(path);
    assertTrue(path.size() > 0);
    
    for (Vertex vertex : path) {
      System.out.println(vertex);
    }
    
  }

  private void addLane(String laneId, int sourceLocNo, int destLocNo,
      int duration) {
    Edge lane = new Edge(laneId,nodes.get(sourceLocNo), nodes.get(destLocNo), duration);
    edges.add(lane);
  }
} 
