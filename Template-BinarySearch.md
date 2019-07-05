# Binary Search

## Property of Binary Search Tree
1. The largest element in the left subtree cannot be greater than its acenstor.
2. The largest element in the right subtree cannot be less than its acenstor.

## Code of Binary Search.
```Do not use binary search to find the answer directly. Binary search return a critical point such that [critical point, end) fulfill the predicate.```
```Base on the assumption above, we can use the critical point to resolve the problem.```
```When using the critical point to solve the problem, consider the range.```

```
int binary_search(int target, vector<int> range)
{
  int left = 0 ;
  int right = range.size() ; //important***
  while(left < right)
  {
    int mid = left + (right - left) / 2 ;
    if (target == range[mid] ) return mid ; //optional***
    if (target < range[mid]) r = mid ; //all element [mid, end) (not include end) fulfill the predicate.
    else left = mid + 1 ;
  }
  
  //may be do some range check for l, when using it.
  if(l == range.size() ) return -1(not found) ;
  else return l ;
}
```
