# Binary Search

## Property of Binary Search Tree
1. The largest element in the left subtree cannot be greater than its acenstor.
2. The largest element in the right subtree cannot be less than its acenstor.

## Code of Binary Search.
The "if(target < range[m])" part can be modified to any other conditions that 
result in searching for left part, so as the else part and the last (range[left] == target)? left:-1

```
int binary_search(int left, int right, int target, vector<int> range)
{
  while(left < right)
  {
    int mid = left + (right - left) / 2 ;
    if (target == range[mid] ) return mid ;
    if (target < range[mid]) r = mid ;
    else left = mid + 1 ;
  }
  
  return (range[left] == target)? left:-1; 
}
```
