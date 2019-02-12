# Union Find

## Problem
1. Cycle detect among several edges.
2. Determine when two node belong to the same connected component.

## Code
```
class union_find
{
  union_find(int num_element)
  {
    //init the parent ;
    parent = vector<int>(num_element, 0) ;
    rank = vector<int>(num_element, 1) ;
    for(int i = 0 ; i < num_element ; ++i)
    {
      parent[i] = i ;
    }
  }
  
  int find(int element)
  {
    if(parent[element] != element)
      parent[element] = find(parent[element]) ;
    return parent[element] ;
  }
  
  void union(int a, int b)
  {
    int pa = find(a) ;
    int pb = find(b) ;
    if(rank[pa] > rank[pb]) parent[pb] = parent[pa] ;
    else parent[pa] = parent[pb] ;
    return ;
  }
  
  private:
    vector<int> parent ; //can be string:string. In this case we can use unordered_map<string, string>. 
    vector<int> rank ;
}
```
