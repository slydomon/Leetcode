# Dynamic Programming

## Basic use case:

1.Listing all the possible partial solutions of subproblem and leverage memoization to resolve duplicate subproblem.
2.Use buttom-up methond to further optimize the performance.
3.If the time complexity of listing all partial solution is the same as the size of lookup table, DP will not be a good fit.



## Idea to crack DP problem:

1.Listing all possible solution and construct a solid base case to handle all situations.
2.Using memoization to save the time and improve the time complexity to size of the lookup table.
3.Using base case above or padding to construct the base case for buttom-up dp such dp[0] so that can resolve the dependency     for the next state.



## Typical DP problem

### Type 1
```
Input size: O(n)
Dependecy for next state: O(1) -> lookup table size: O(n)
Classic problem: Leetcode 70, 198
```
#### Code Template:

##### Memoization
```
//use level-1 as input
int recursize(int level, vector<int>& lookup)
{
  if(level <= 0)
    return n ;
  else if(lookup[level] != -1)
    return lookup[level]
  else
  {
    int tmp = func(recursive(level-1, lookup), recursive(level-2, lookup)) ;
    lookup[level] = tmp ;
    return tmp ;
  }
}
```

##### Dynamic Programming
```
int iterative(int level, vector<int>& dp)
{
  dp[0] = n ; // add padding
  dp[1] = n ; //corresponding to base case above.
  
  for(int i = 0 ; i < level ; ++i)
  {
    dp[i] = func(dp[i-1], dp[i-2]) ;
  }
  return dp[level-1] ;
}
```

#### Code

```
class Solution {
public:
    int climbStairs(int n) {
        vector<int> lookup(n+1, -1) ;
        return iterative_helper(n, lookup) ;
    }
    
    int helper(int cur_pos, vector<int>& lookup)
    {
        if(cur_pos == 0 || cur_pos == 1) return 1 ;
        //else if(cur_pos < 0) return 0 ;
        else if(lookup[cur_pos] != -1) return lookup[cur_pos] ;
        else
        {
            int tmp = helper(cur_pos - 1, lookup) + helper(cur_pos - 2, lookup) ;
            lookup[cur_pos] = tmp ;
            return tmp ;
        }
    }
    
    int iterative_helper(int cur_pos, vector<int>& lookup)
    {
        lookup[0] = 1 ; //set up base case based on the memoization's base case.
        lookup[1] = 1 ; //set up base case based on the memoization's base case.
        for(int i = 2 ; i < cur_pos+1 ; ++i)
        {
            lookup[i] = lookup[i-1] + lookup[i-2] ;
        }
        
        return lookup[cur_pos] ;
    }
};
```

### Type 2(MUST Review)

```
Input size: O(n)
Dependecy for next state: O(n) -> lookup table size: O(n)
Classic problem: Leetcode 139(wordbreak), 300(longest increasing subsequence), 673(nums of longest increasing subsequence)
```

#### Allegator Pacman Type
Top-down: Need to go through all the current choices to find the solution and therefore will have for loop within recursive function.
Buttom-up: The next state relys on all the previous states.
***only have one sub problems

#### Code Template

##### Memoization
```
****
//Use input.size() as input for range;
int recur(const vector<int>& input, range, vector<int>& lookup)
{
  //hit smallest subproblem
  if(range == 0)
  {
    return n ;
  }
  else if(lookup[range] != 0)
    return lookup[range] ;
  else
  {
    int tmp = 0 ;
    int end = input.size() ;
    int start = end - range ;
    //CUT /LEET -> L/EET -> LE/ET -> LEE/T
    for(int cut_pos = start ; cut_pos < end ; ++cut_pos)
    {
      int subproblem_size = cut_pos - start ;
      int rest = end - cut_pos ;
      tmp = func(recursive(input, subproblem_size, lookup), Const(rest)) ;
    }
    lookup[range] = tmp ;
    return tmp ;
  }
}
```

##### Dynamic Programming
```
int iterative(const vector<int>& input, range, vector<int>& dp)
{
  dp[0] = n ; //padding with n ;
  int size = input.size() ; 
  for(int range = 1 ; range <= size ; ++range)
  {
    for(int cut_pos = 0 ; cut_pos < range ; ++cut_pos)
    {
      dp[range] = func(dp[cut_pos], Const(cut_pos, range-cut_pos) ;
    }
  }
  
  return dp[range] ;
}
```

#### Code
```
Note:
1. The methodologies to solve this problem with top-down and buttom-up intuitively different but actually the same.
2. For top-down, we divide the problem into a O(1) subproblem and a O(n-1) subproblem, and keep doing so until the O(n-1)        becomes hit the base case(n = 0)
3. For buttom-up, we construct the solution from dp[0] = 0 (n=0), which is the smallest subproblem in momoization solution.

class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        using vec_it = std::vector<string>::iterator ;
        unordered_set<string_view> dict (move_iterator<vec_it>(begin(wordDict)), move_iterator<vec_it>(end(wordDict))) ;
        size = s.size() ;
        vector<int> lookup(size, -1) ;
        return helper(0, dict, string_view(s), lookup) ;       
    }
    
    bool helper(int idx, const unordered_set<string_view>& dict, string_view cur, vector<int>& lookup)
    {
        if(idx == size) 
            return true ;
        else if(lookup[idx] != -1)
            return lookup[idx] ;
        else
        {
            for(int i = idx ; i < size ; ++i)
            {
                if(dict.find(cur.substr(idx, i - idx + 1)) != dict.end()
                  && helper(i+1, dict, cur, lookup))
                {
                    lookup[idx] = 1 ;
                    return true ;
                }
            }
            lookup[idx] = 0 ;
            return false ;
        }
    }
 private:   
    int size ;
 };  

class Solution {
public:
    bool helper_iterative(const string& segment, const unordered_set<string>& dict, vector<int>& dp)
    {
        dp[0] = true ; //empty is valid although it is not in dict .
        int size = segment.size() ;
        for(int range = 1 ; range <= size ; ++range)
        {
            //try every previous partial solution to see if there is a valid one
            for(int cut_pos = 0 ; cut_pos < range ; ++cur_pos) 
            {
                
                string rest = segment.substr(cut_pos, range-cut_pos) ;
                
                //if both previous solution && rest of the string are valid 
                if(dp[cut_pos] && (dict.find(rest) != dict.end()))
                {
                    dp[range] = true ;
                    break ;
                }
            }
        }        
        return dp[size] ; //goal is to find if there is valid string range from start to end of segment.
    }
       
};


```

### Pacman Type
Top-down: Fixed number of choices and therefore won't have for loop within recursive function.
  ex. Longest common subsequence: move i, move j, or if(s1[i] == s2[j]) move both.
Buttom-up: Only need contant number of previous states to form the next answer
  ex. Longest common subsequence: lookup[i, j] = max(lookup[i-1, j], lookup[i, j-1]).





### Divide and Conquer
Separate into several sub problems and combines the results from all of them `
