import java.io.File;
import java.io.FileNotFoundException;
import java.util.*;

class Edge {
    int fromIndex;
    int toIndex;
    double weight;

    public Edge(int fromIndex, int toIndex, double weight) {
        this.fromIndex = fromIndex;
        this.toIndex = toIndex;
        this.weight = weight;
    }
}

public class GraphProcessor {
    private int numNodes;
    private List<String> nodeNames;
    private int startingNodeIndex;
    private List<Edge> edges;

    private List<List<Integer>> adjacencyList;

    public void readGraphFromFile(String filePath) throws FileNotFoundException {
        File file = new File(filePath);
        Scanner scanner = new Scanner(file);

        // Read the number of nodes and edges
        numNodes = scanner.nextInt();
        int numEdges = scanner.nextInt();
        scanner.nextLine();

        // Read the node names or check if indexes are to be used
        String nodeNamesLine = scanner.nextLine();
        if (!nodeNamesLine.equals("use-indexes")) {
            // Node names 
            String[] nodeNamesArray = nodeNamesLine.split(" ");
            nodeNames = new ArrayList<>();
            for (String nodeName : nodeNamesArray) {
                nodeNames.add(nodeName);
            }
        }

        // Read the starting node index
        startingNodeIndex = scanner.nextInt();
        scanner.nextLine();

        // Read the edges
        edges = new ArrayList<>();
        for (int i = 0; i < numEdges; i++) {
            int fromIndex = scanner.nextInt();
            int toIndex = scanner.nextInt();
            double weight = scanner.nextDouble();
            scanner.nextLine();

            Edge edge = new Edge(fromIndex, toIndex, weight);
            edges.add(edge);
        }

        scanner.close();
    }

    private void buildAdjacencyList() {
        adjacencyList = new ArrayList<>(numNodes);
        for (int i = 0; i < numNodes; i++) {
            adjacencyList.add(new ArrayList<>());
        }

        for (Edge edge : edges) {
            adjacencyList.get(edge.fromIndex).add(edge.toIndex);
        }
    }

    private List<List<Integer>> findAllPaths(int start, int end) {
        List<List<Integer>> paths = new ArrayList<>();
        List<Integer> currentPath = new ArrayList<>();
        Set<Integer> visited = new HashSet<>();

        dfs(start, end, visited, currentPath, paths);

        return paths;
    }

    private void dfs(int node, int end, Set<Integer> visited, List<Integer> currentPath, List<List<Integer>> paths) {
        visited.add(node);
        currentPath.add(node);

        if (node == end) {
            paths.add(new ArrayList<>(currentPath));
        } else {
            for (int neighbor : adjacencyList.get(node)) {
                if (!visited.contains(neighbor)) {
                    dfs(neighbor, end, visited, currentPath, paths);
                }
            }
        }

        visited.remove(node);
        currentPath.remove(currentPath.size() - 1);
    }

    public void processGraph() {
        buildAdjacencyList();

        List<List<Integer>> shortestPaths = findAllPaths(startingNodeIndex, -1);

        for (int i = 0; i < shortestPaths.size(); i++) {
            List<Integer> path = shortestPaths.get(i);
            System.out.print("Shortest path from " + nodeNames.get(startingNodeIndex) + " to " + nodeNames.get(i) + ": ");
            for (int j = 0; j < path.size(); j++) {
                System.out.print(nodeNames.get(path.get(j)));
                if (j != path.size() - 1) {
                    System.out.print(" -> ");
                }
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        GraphProcessor graphProcessor = new GraphProcessor();

        try {
            graphProcessor.readGraphFromFile("input.txt");
            graphProcessor.processGraph();
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}

  
                                            
                                            
                                            
                                            
                                            
 import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Edge {
    int fromIndex;
    int toIndex;
    double weight;

    public Edge(int fromIndex, int toIndex, double weight) {
        this.fromIndex = fromIndex;
        this.toIndex = toIndex;
        this.weight = weight;
    }
}

public class GraphProcessor {
    private int numNodes;
    private List<String> nodeNames;
    private int startingNodeIndex;
    private List<Edge> edges;

    public void readGraphFromFile(String filePath) throws FileNotFoundException {
        File file = new File(filePath);
        Scanner scanner = new Scanner(file);

        // Read the number of nodes and edges
        numNodes = scanner.nextInt();
        int numEdges = scanner.nextInt();
        scanner.nextLine();

        // Read the node names or check if indexes are to be used
        String nodeNamesLine = scanner.nextLine();
        if (!nodeNamesLine.equals("use-indexes")) {
            // Node names
            String[] nodeNamesArray = nodeNamesLine.split(" ");
            nodeNames = new ArrayList<>();
            for (String nodeName : nodeNamesArray) {
                nodeNames.add(nodeName);
            }
        }

        // Read the starting node index
        startingNodeIndex = scanner.nextInt();
        scanner.nextLine();

        // Read the edges
        edges = new ArrayList<>();
        for (int i = 0; i < numEdges; i++) {
            int fromIndex = scanner.nextInt();
            int toIndex = scanner.nextInt();
            double weight = scanner.nextDouble();
            scanner.nextLine();

            Edge edge = new Edge(fromIndex, toIndex, weight);
            edges.add(edge);
        }

        scanner.close();
    }

    public void processGraph() {
        // This can involve determining if the graph is cyclic or acyclic,
        // and using the appropriate algorithms to find the shortest paths.
    }

    public static void main(String[] args) {
        GraphProcessor graphProcessor = new GraphProcessor();

        try {
            graphProcessor.readGraphFromFile("input.txt");
            graphProcessor.processGraph();
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
                                           
                                            
                                            
