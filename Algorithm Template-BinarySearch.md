# Binary Search

## Property of Binary Search Tree
1. The largest element in the left subtree cannot be greater than its acenstor.
2. The largest element in the right subtree cannot be less than its acenstor.

## Code of Binary Search.
The "if(target < range[m])" part can be modified to any other conditions that 
result in searching for left part, so as the else part. 

```
int binary_search(int left, int right, int target, vector<int> range)
{
  while(l < r)
  {
    int m = l + (r-l) / 2 ;
    if (target == range[m] ) return m ;
    if (target < range[m]) r = m ;
    else l = m + 1 ;
  }
  return -1; //no such answer.
}
```
