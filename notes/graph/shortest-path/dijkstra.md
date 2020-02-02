# Dijkstra's algorithm

Dijkstra's original algorithm found the shortest path between two given nodes, but a more common variant fixes a single node as the "source" node and finds shortest paths from the source to all other nodes in the graph, producing a **shortest-path tree**.

It's a greedy BFS algorithm.

## Implementation

```cpp
typedef unordered_map<int, unordered_map<int, int>> Graph;
typedef pair<int, int> iPair;
vector<int> dijkstra(Graph &graph, int N, int source) {
    priority_queue<iPair, vector<iPair>, greater<iPair>> pq;
    vector<int> dists(N, INT_MAX);
    pq.emplace(0, source);
    dists[source] = 0;
    while (pq.size()) {
        int u = pq.top().second;
        pq.pop();
        for (auto neighbor : graph[u]) {
            int v = neighbor.first, weight = neighbor.second;
            if (dists[v] > dists[u] + weight) {
                dists[v] = dists[u] + weight;
                pq.emplace(dists[v], v);
            }
        }
    }
    return dists;
}
```

## Problems

* [743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)
* [787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)

## Reference
* [Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)