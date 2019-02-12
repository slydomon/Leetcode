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


## one pair shortest path: Dijkstra
limitation: No negative edge is allowed.
Input adjacent list.

