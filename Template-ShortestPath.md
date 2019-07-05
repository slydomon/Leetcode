# Shortest Path

## All pair shortest path: Floye-Washell
Limitation: Not allowed negative edges that forms a cycle
Input is a Graph formed by a 2D array.
```
vector<vector<int> > FW(vector<vector<int> > graph)
{
  int size = graph.size() ;
  for(int k = 0 ; k < size ; ++k)
  {
    //update the distance for every pairs that with a certain intermediate point
    for(int j = 0 ; j < size ; ++j)
    {
      for(int i = 0 ; i < size ; ++i)
      {
        int tmp = graph[i][k] + graph[k][j] ;
        if(graph[i][j] > tmp) 
          graph[i][j] = tmp ;
      }
    }
  }
  return graph ;
}
```

## one pair shortest path: Dijkstra
```
limitation: No negative edge is allowed.
Input adjacent list.
```

```
vector<int> Dijkstra(vector<vector<int> > graph, int k)
{
  vector<pair<int, int> > g ;
  for(int i = 0 ; i < graph.size() ++i)
  {
    for(int j = 0 ; j < graph[i].size() ; ++j)
    {
      g[i] = make_pair(j, graph[i][j] ;
    }
  }
  constexpr int MAX_DIST = INT_MAX ;
  vector<int> dist(num_of_node + 1, MAX_DIST) ;
  vector<int> visited(num_of_node+ 1, false) ;
  dist[k] = 0 ;
  priority_queue<pair<int, int>, vector<pair<int, int>, std::greater<pair<int, int> > pq ;
  pq.push(make_pair(0, k)) ;
  int u, v, weight ;
  while(!pq.empty())
  {
    auto current = pq.top() ; 
    pq.pop() ;
    u = current.second  ;
    if(!visited[u])
    {
      for(auto& to: g[u])
      {
        v = to.first, weight = t.second ;
        if(dist[v] > dist[u] + weight)
        {
          dist[v] = dist[u] + w ;
          pq.push(make_pair(dist[v], v)) ;
        }
      }
      visited[u] = true ;
    }
    
  }
  return dist ;
}

```

## one pair shortest path: Bellman-Ford
```
limitation: support negative edge is allowed.
Input adjacent list.
```


```
return k-to-all shortest path;

vector<int> bellman_ford(vector<vector<int> > graph, int k)
{
  constexpr int MAX_DIST = int_max ;
  vector<int> dist(num_of_node, MAX_DIST) ;
  dist[k] = 0 ;
  for(int i = 1 ; i < N ; ++i)
  {
    for(const auto& edge: graph)
    {
      int start = edge[0], end = edge[1], weight = edge[2] ;
      dist[v] = min(dist[v], dist[start] + weight) ;
    }
  }
}

return dist ;
```
