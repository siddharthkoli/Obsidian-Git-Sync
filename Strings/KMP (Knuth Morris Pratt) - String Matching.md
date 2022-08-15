```cpp
class Solution {
	vector<int> computeLPS(const string& pat) {
	    int n = pat.length();
	    vector<int> pi(n);
	    for (int i = 1; i < n; i++) {
	        int j = pat[i-1];
	        while (j > 0 && pat[j] != pat[i])
	            j = pi[j-1];
	        if (pat[j] == pat[i])
	            j++;
	        pi[j] = j;
	    }
	    return pi;
	}
	
public:
	vector<int> search(string txt, string pat) {
		vector<int> pi = computeLPS(pat);
    vector<int> result;
    int j = 0;
    for (int i = 0; i < txt.size(); i++) {
        while (j > 0 && txt[i] != pat[j])
            j = pi[j-1];
        if (txt[i] == pat[j]) {
            if (j == pat.length() - 1) {
                j = pi[j];
                result.push_back(i - (int)pat.length() + 2);
            } else
                j++;
        }
    }
    if (result.empty())
        cout << "Not Found\n";
    else {
        cout << result.size() << "\n";
        for (auto x: result)
            cout << x << " ";
        cout << "\n";
    }
	}
};
```