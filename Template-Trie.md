# Trie

## Use case
1. Optimize for the situation that we have plenty of element and require to search many times.
2. Trie can optimize the time complexity of search operation. 
3. time complexity is O(L) where L is the length of the longest word.
4. space complexity is O(N*L), where N is the number of words and L is the length of each word.

## Code
```
class trie
{
  trie()
  {
    root = new node() ; // dummy head
  }
  
  ~trie() //prevent memory leak
  {
    for(int i = 0 ; i < 26 ; ++i){
      if(children[i])
        delete children[i] ;
    }
  }
  
  void insert(string s)
  {
    int size = s.size() ;
    node* cur = root ;
    for(int i = 0 ; i < size ; ++i)
    {
      if(!cur->children[s[i] - 'a']) //the node does not exist.
      {
        cur->children[s[i] - 'a'] = new node() ;
        cur->val = s[i] ;
      }
      else
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
    struct node
    {
      node():end(false), children(vector<node*>(26,nullptr);
      ~node()
      {
        for(int i = 0 ; i < 26 ; ++i)
        {
          if(children[i])
            delete children[i] ;
        }
      }
      char val ; // val = "", if it is dummy head. 
      bool end ;
      vector<node*> children(26, nullptr) ;
    }
    
    node* root ;
}
```
