```cpp
class TrieNode { 
 public:
    std::vector<TrieNode*> children;
    bool isWord;
    TrieNode() : children(26) {
        this->isWord = false;
    }
};

class Trie {
private:
    TrieNode* root;
    
public:
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string word) {
        TrieNode* p = root;
        for (auto& x: word) {
            int charInd = x - 'a';
            if (p->children[charInd] == nullptr)
                p->children[charInd] = new TrieNode();
            p = p->children[charInd];
        }
        p->isWord = true;
    }
    
    bool search(string word) {
        TrieNode* p = this->root;
        for (auto& x: word) {
            int charInd = x - 'a';
            if (p->children[charInd] == nullptr)
                return false;
            p = p->children[charInd];
        }
        return p->isWord;
    }
    
    bool startsWith(string prefix) {
        TrieNode* p = this->root;
        for (auto& x: prefix) {
            int charInd = x - 'a';
            if (p->children[charInd] == nullptr)
                return false;
            p = p->children[charInd];
        }
        return true;
    }
};
```
