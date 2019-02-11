# Trie

## Use case
1. Optimize for the situation that we have plenty of element and require to search many times.
2. Trie can optimize the time complexity of search operation. 

## Code
```
struct node
{
  char val ;
  bool end ;
  vector<node*> children(26, nullptr) ;
}
class trie
{
  trie()
  {
    root = new node() ;
    //a-z and # is end symbol;
  }
  
  void insert(string s)
  {
    int size = s.size() ;
    node* cur = root ;
    for(int i = 0 ; i < size ; ++i)
    {
      if(cur->children[s[i] - 'a'] == '0')
      {
        cur->children[s[i] - 'a'] = new node() ;
        cur->val = s[i] ;
      }
      cur = cur->children[s[i] - 'a'] ;
    }
    cur->end = true ; //there is a word end here
  }
  
  bool search(string s)
  {
    int size = s.size() ;
    node* cur = root ;
    for(int i = 0 ; i < size ; ++i)
    {
      if(cur->children[s[i] - 'a'] == nullptr) 
        return false;
      else
        cur = cur->children[s[i] - 'a'] ;
    }
    return cur->end ; //if true, there is a word end here .
  }
  
  private:
    node* root ;
}
```
