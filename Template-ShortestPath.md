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
  //convert graph to adjacent list
  vector<pair<int, int> > g ;
  for(int i = 0 ; i < graph.size() ++i)
  {
    for(int j = 0 ; j < graph[i].size() ; ++j)
    {
      g[i] = make_pair(j, graph[i][j] ;
    }
  }
  
  //initialize required data structure.
  constexpr int MAX_DIST = INT_MAX ;
  vector<int> dist(num_of_node + 1, MAX_DIST) ;
  vector<int> visited(num_of_node+ 1, false) ;
  dist[k] = 0 ;
  priority_queue<pair<int, int>, vector<pair<int, int> >, std::greater<pair<int, int> > pq ; //pair: dist/node
  pq.push(make_pair(0, k)) ;
  int u, v, weight ;
  
  while(!pq.empty())
  {
    auto current = pq.top() ; 
    pq.pop() ;
    cur = current.second  ;
    if(!visited[cur])
    {
      //include the new node into the group and take it into account to update dist.
      for(auto& to: g[cur])
      {
        v = to.first, weight = to.second ;
        if(dist[v] > dist[u] + weight)
        {
          dist[v] = dist[u] + weight ;
          pq.push(make_pair(dist[v], v)) ; //if dist is update, push new infomation into pq.
        }
      }
      visited[u] = true ; //mark u as member in group(visited) ;
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

```
