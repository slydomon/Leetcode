# Trie

## Use case
1. Optimize for the situation that we have plenty of element and require to search many times.
2. Trie can optimize the time complexity of search operation. 
3. time complexity is O(L) where L is the length of the longest word.
4. space complexity is O(N*L), where N is the number of words and L is the length of each word.

## Code
```
class Trie {
public:
    /** Initialize your data structure here. */
    Trie() {
        root.reset(new Node) ;
        root->tail = true ;
    }
    
    /** Inserts a word into the trie. */
    void insert(string_view word) {
        Node* cur = root.get() ;
        for(const auto& c : word)
        {
            if(cur->children[c - 'a'].get() == nullptr)
                cur->children[c - 'a'].reset(new Node) ; 
            cur = cur->children[c - 'a'].get() ; 
        }
        cur->tail = true ;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string_view word) {
        Node* cur = root.get() ;
        for(const auto& c: word)
        {
            if(cur->children[c - 'a'].get() == nullptr)
                return false ;
            cur = cur->children[c - 'a'].get() ; 
        }
        return cur->tail ;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string_view prefix) {
        Node* cur = root.get() ;
        for(const auto& c: prefix)
        {
            if(cur->children[c - 'a'].get() == nullptr)
                return false ;
             cur = cur->children[c - 'a'].get() ; 
        }
        return true ;
    }
    
    void delete(string_view s)
    {
      Node* cur = root.get() ;
      int count = 0 ;
      for(const auto& c: s)
      {
        count = 0 ;
        cur = cur->children[c - 'a'] ;
        for(c : cur->children)
        {
          if(c != nullptr)
          { 
            if(++count > 1) break ;
          }
        }
        if(count == 1) 
        {
          cur.~Node() ; //no other children and safely destruct the node and will recursively destruct.
          return ;
        }
      }
      cur->tail = false ;
      for(c : cur->children)
      {
        if(c != nullptr)
          if(++count > 1) return ;
      }
      cur.~Node() ;
    }
    

private:    
    struct Node
    {
        Node()
        {
            //children.reserve(26) ;
           // for(int i = 0 ; i < 26 ; ++i)
                //children.emplace_back(nullptr) ;
        }
        bool tail = false ;
        array<unique_ptr<Node>, 26> children ;
    } ;
    unique_ptr<Node> root ;
};
```
