#Sovle prefix sum problem

```data not mutable: DP```
```data mutable: Fenwick Tree. (value mutable not size***)```

##idea
```Every node contain a partial solution of any query.```
```By retrieving partial solution from require node, we can achieve O(logn) time complexity.```

##implementation
###update
```index of parent node is the current index += lowest_bit.```
```low_bit = x & -x```
```update: root.val = sum(children.val) + num[root.id]```
###query
```index of parent node is current index -= lowest_bit.```
```sum(all node)```

###code
```
class FenwickTree
{
  FenwickTree(int n): sum_(vector<int>(n+1, 0)) {}
  
  void update(int i, int delta)
  {
    while(i < sum.size())
      sums_[i] += delta ;
      i += lowbit(i) ;
  }
  
  int query(int i) const
  {
    int sum = 0 ;
    while(i > 0)
    {
      sum += sums_[i];
      i -= lowbit(i);
    }
    return sum ;
  }
private:
  inline in lowbit(int x) {return x &(-x);}
  vector<int> sums_;
}
```



