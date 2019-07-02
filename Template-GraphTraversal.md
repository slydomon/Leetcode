# Algorithm Template-Traversal

## Iterative Tree Traversal

### preorder

```
void preorder(TreeNode* root)
{
  stack<TreeNode*> s ;
  s.push(root) ;
  while(!s.empty())
  {
    TreeNode* tmp = s.top() ;
    s.pop() ;
    //do something here ...
    int size = tmp->children.size() ;
    for(int i = size-1 ; i >= 0 ; ++i)
      s.push(children[i]) ;
  }
}
```

### inorder


```
void inorder(TreeNode* root)
{
  stack<TreeNode*> s;
  TreeNode* cur = root ;
  while(!cur || !s.empty())
  {
    //TreeNode* tmp = cur ;
    while(!cur)
    {
      s.push(cur)
      cur = cur->left ;
    }
    
    TreeNode* tmp = s.top() ;
    s.pop() ;
    //do something here...
    cur = cur.right ;
  }
}
```

### postorder

```
void postorder(TreeNode* root)
{
  stack<TreeNode*> s1 ;
  stack<TreeNode*> s2 ;
  s1.push(root) ;
  while(!s1.empty())
  {
    TreeNode* tmp = s1.top() ;
    s1.pop() ;
    s2.push(tmp) ;
    int size = tmp->children.size() ;
    for(int i = 0 ; i < size ; ++i)
    {
      s1.push(children[i]) ;
    }
  }
  
  while(!s2.empty())
  {
    TreeNode* tmp = s2.top() ;
    s2.pop() ;
    //do something here ; 
  }
}

```

### Morris Traversal preorder (space complexity = O(1) )

```print, build bridge, traverse, visited again thruogh bridge, destruct bridge```

```
while(root)
{
  if(!root->left)
  {
    cout << root->data ;
    root = root->right ;
  }
  
  else
  {
    node* current = root->left ;
    //find proper node to build bridge.
    while(current->right && current->right != node)
      current = current -> right ;
    
    //visited again
    if(current == node)
    {
      current = nullptr ;
      root->right ;
    }
    //build bridge
    else
    {
      cout << root->data ;
      current->right = root ;
    }
  }
}
```
### Morris Traversal inorder.

```traverse, print,  build bridge, visited again, distruct```

```
while(root)
{
  if(!root->left)
  {
    cout << root->data ;
    root->right ;
  }
  else
  {
    node* current = root->left ;
    while(current->right && current->right != root) current = current -> right ;
    
    if(current == root)
    {
      cout << root->data ;
      current->right = null ;
      root = root->right ;
    }
    else
    {
      root->left ;
    }
  }
}
```

## Graph Traversal

### DFS

Remember the visited flag, and if traversing directed graph, remember circle detection.

```
void DFS(Node* node)
{
    node->visited = 1 ;
    int size = node->children.size() ;
    for(int i = 0 ; i < size ; ++i)
    {
      if(node->visited != 1)
        DFS(children[i]) ;
      else if(node->CircleFlag == 0) //visited == 1 && CircleFlag == 0 ;
      {
        cout << "circle" << endl;
        abort() ;
      }
    }
  }
  node->CircleFlag = 1 ;
}

void DFS_DRIVER(unordered_map<int, Node*> graph)
{
  for(auto it = graph.begin() ; it != graph.end() ; ++it)
  {
    Node* cur = it->second ;
    if(cur->visited != 1)
        DFS(children[i]) ;
     else if(node->CircleFlag == 0) //visited == 1 && CircleFlag == 0 ;
       cout << "circle" << endl;
  }
}
```

### BFS

1. Remember the visited flag ;
2. Using two queues to maintain the level ;
3. Circle detection: if next->visited == 1 && next->level < cur->level, then there is a cycle .

```
void BFS(Node* node)
{
  int level = 0 ;
  queue<Node*> cur ;
  queue<Node*> next ;
  cur.push(node) ;
  node->visited = 1 ; //mark at here is important ;
  while(!cur.empty())
  {
    Node* tmp = cur.top() ;
    //tmp->visited = 1 ; ***mark the visited as soon as the node is put into ready queue to avoid duplicate put.
    tmp->level = level ;
    cur.pop() ;
    int size = tmp->children->size() ;
    for(int i = 0 ; i < size ; ++i)
    {
      if(children[i]->visited != 1)
      {
        next.push(children[i]) ;
        children[i]->visited = 1 ;
      }
      else if(children[i]->level < cur->level)
        cout << "cycle" << endl ;
    }
    if(cur.empty())
    {
      swap(cur, next) ;
      ++level ;
    }
  }
}

void BFS_DRIVER(unordered_map<int, Node*> graph)
{
  for(auto it = graph.begin() ; it != graph.end() ;++it)
  {
    Node* tmp = it->second() ;
    if(tmp->visited != 1)
      BFS(tmp)
  }
}
```

## Topological Sort
Need cycle detection to vaildate the acyclic property

### BFS
1. Calculate the indegree.
2. Start with node with 0 indegree.
3. When visiting a node, eliminate the node from graph and minus the indegree value of all its children.

```
void BFS_Topological_Sort(unordered_map<int, Node*> graph)
{
  //Calculate indegree
  for(auto it = graph.begin() ; it != graph.end() ; ++it)
  {
    Node* cur = it->second ;
    int size = cur->children.size() ;
    for(int i = 0 ; i < size ; ++i)
    {
      ++children[i]->indegree ;
    }
  }
  
  //add node with 0 indegree to ready queue, others with be in pending set
  queue<Node*> ready ; //node with 0 indgree ;
  unordered_set<int> pending ;
  for(auto it = graph.begin() ; it != graph.end() ; ++it)
  {
    if(it->second->indegree == 0)
      ready.puhs(it->second) ;
    else
      pending.insert(it->first) ;
  }
  
  while(!ready.empty())
  {
    Node* cur = ready.front() ;
    ready.pop() ;
    //do something here ;
    int size = cur->children.size() ;
    for(int i = 0 ; i < size ; ++i)
    {
      --children[i]->indegree ;
      if(children[i]->indegree == 0)
      {
        pending.erase(children[i].value) ;
        ready.push(children[i]) ;
      }
    }
    
    if(ready.empty() && !pending.empty())
    {
      cout << "cycle detected" << endl; 
      abort() ;
    }
  }
}
```

### DFS
1. Print the node from the leaf-like node, so the ordered is reversed.
2. We can save it in a stack and print it out at the end.

```
void DFS_Topological_Sort(Node* node, stack<Node*>& record)
{
  node->visited = 1 ;
  int size = node->children->size() ;
  for(int i = 0 ; i < size ; ++i)
  {
    if(node->children[i]->visited != 1)
      DFS_Topological_Sort(node->children[i]) ;
    else if(cycle == 0) //visited == 1 && cycle == 0
    {
      cout << "detect cycle" endl ;
      abort() ;
    }
  }
  record.push(node) ;
  node->cycle = 1 ;
}

void DFS_DRIVER(unordered_map<int, Node*> graph)
{
  stack<Node*> record ;
  for(auto it = graph.begin() ; it != graph.end() ; ++it)
  {
    Node* cur = it->second ;
    if(cur->visited != 1)
      DFS_Topological_Sort(cur, record) ;
    else if(cur->cycle == 0) //visited == 1 && cycle == 0
    {
      cout << "detect cycle" endl ;
      abort() ;
    }
  }
  
  while(!record.empty())
  {
    Node* tmp = record.top() ;
    record.pop() ;
    //do something here ;
  }
  return ;
}
```
