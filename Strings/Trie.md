```cpp
class TrieNode { 
 public:
    // std::vector<TrieNode*> children;
    TrieNode* 
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
	
	// erase function may not work 100% of the time
	void erase(string word) {
	    TrieNode* p = this->root;
	    std::stack<TrieNode*> stack;
	    for (int i = 0; i < word.length(); i++) {
	        int ind = word[i] - 'a';
	        if (p->children[ind] == nullptr)
	            return;
	        stack.push(p);
	        p = p->children[ind];
	    }
		
	    p->isWord = false;
		
	    int i = word.length() - 1;
	    while (!stack.empty()) {
	        TrieNode* prev = stack.top(); stack.pop();
	        int ind = word[i--] - 'a';
	        prev->children[ind] = nullptr;
	        p = prev;
	    }
	}
};
```

![[Pasted image 20240907233126.png]]