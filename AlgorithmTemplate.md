# Algorithm Template

## Iterative Tree Traversal

### preorder

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
    for(int i = 0 ; i < size ; ++i)
      s.push(children[i]) ;
  }
}

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
  while(!cur.empty())
  {
    Node* tmp = cur.top() ;
    tmp->visited = 1 ;
    tmp->level = level ;
    cur.pop() ;
    int size = tmp->children->size() ;
    for(int i = 0 ; i < size ; ++i)
    {
      if(children[i]->visited != 1)
        next.push(children[i]) ;
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
```
