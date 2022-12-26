Assume each word as a node connected to another node which is its one off. This forms a graph and we only have to find the shortest path from `beginWord` to `endWord`.
This can easily be done using `BFS`.
```cpp
using std::string;

class Solution {
public:
    // Time: O(26 * M * N), space: O(M * N)
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        std::unordered_set<string> words(wordList.begin(), wordList.end());
        std::queue<string> queue;
        queue.push(beginWord);
        int res = 0;
        
        // total time = O(26 * M * N)
        while (!queue.empty()) { // O(N)
            int levelSize = queue.size();
            while (levelSize--) {
                string word = queue.front(); queue.pop();
                if (word == endWord)
                    return ++res;
                words.erase(word);
                // O(26 * M)
                for (int i = 0; i < word.size(); i++) {
                    char original = word[i];
                    for (int j = 0; j < 26; j++) {
                        word[i] = 'a' + j;
                        if (words.find(word) != words.end())
                            queue.push(word);
                    }
                    word[i] = original;
                }
            }
            res++;
        }
        return 0;
    }
};
```