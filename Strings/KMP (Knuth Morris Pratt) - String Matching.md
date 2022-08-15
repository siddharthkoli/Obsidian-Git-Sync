#### Pi\[i] answers the following question: Given a pattern pat of length n, how many characters from the start (prefix) of the substring pat\[0...i] are also the suffix? The answer is Pi\[i].

![[Pasted image 20220815192045.png]]
So we did encounter the mismatch at some point in the comparison between the pattern and the target text. `**E**` is not equal to `**C**`, what a bummer. However, we can be sure that the pattern sub-string till the pattern pointer matches the target sub-string till the target pointer (red dashed line). Otherwise, we wouldn’t reach this point according to our definition of the second phase. Additionally, our LPS array for the current pattern sub-string tells us that the prefix of length `3` is equal to the suffix (shaded in green). With this information in hand, we can safely move the pattern pointer back to the fourth symbol (the first symbol after LPS) and leave the target pointer at the same place, as demonstrated below.

#### From the above picture, `E` is not matched. But to reach `E`, its previous chars have to have matched, or else we wouldn't reach `E`. Also notice that there are 2 sets of `ACA`, one at start, and one at end, in both pattern and target text. LPS definition states that Pi\[j] chars from the end have to be present at the start. In the above eg, Pi\[i] for `A` just before the unmatched `C` is 3. That means 3 chars from start are also present in the end of the substr pat\[0...i]. And since these chars have already matched the end, they can also match for the start and hence need not be compared. Thus the `j` pointer on pat can be moved to just after the `A` following the first `C` in the pat, i.e. index 3 - which also happens to be Pi\[i] (current unmatched `C` from pat).
![[Pasted image 20220815233143.png]]

![[Pasted image 20220815222756.png]]
It’s guaranteed that the part of the pattern before the new pattern pointer matched the target string due to the definition of the LPS. It also holds true that we didn’t miss any possible matches between the current target pointer and the index at which we’ve started to compare last time. 


```cpp
class Solution {
	vector<int> computeLPS(const string& pat) {
	    int n = pat.length();
	    vector<int> pi(n);
	    for (int i = 1; i < n; i++) {
	        int j = pi[i-1];
	        while (j > 0 && pat[j] != pat[i])
	            j = pi[j-1];
	        if (pat[j] == pat[i])
	            j++;
	        pi[i] = j;
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
	    return result;
	}
};
```
- Time: `O(M + N)`
- Space: `O(M)`

can refer: http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/