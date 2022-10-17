The first step is to find which accounts have an email in common and merge them to form a larger connected component. Any problem that involves merging connected components (accounts) is a natural fit for the Disjoint Set Union (DSU) data structure. Since most implementations of DSU use an array to record the root (representative) of each component, we will use integers to represent each component for ease of operability. Therefore, we will give each account a unique ID, and we will map all the emails in the account to the account's ID. We will use a map, `emailGroup`, to store this information.

We chose the account index to be the identifier for all the emails of an account. We will assign the account index as the group when we get the email for the first time and when we get an email that we have already traversed, we will merge the current account and the group that we have previously stored in `emailGroup` using union operation.

After traversing over all the accounts, we will find the representative of all the emails which will inform us about their group. Emails with the same representative belong to the same person/group and hence will be stored together. Also, we can retrieve the account name for our final answer using `accountList` as we have `group` which is the index in the original accounts list.
![[Pasted image 20221017162421.png]]

<hr/>

![[Pasted image 20221017162429.png]]
<hr/>

![[Pasted image 20221017162433.png]]
<hr/>
![[Pasted image 20221017162437.png]]
<hr/>
![[Pasted image 20221017162445.png]]
<hr/>
![[Pasted image 20221017162450.png]]
<hr/>
![[Pasted image 20221017162454.png]]
<hr/>
![[Pasted image 20221017162500.png]]
<hr/>
![[Pasted image 20221017162504.png]]
<hr/>
![[Pasted image 20221017162508.png]]
<hr/>
```cpp
class DSU {
public:
    vector<int> representative;
    vector<int> size;
    
    DSU(int sz) : representative(sz), size(sz) {
        for (int i = 0; i < sz; ++i) {
            // Initially each group is its own representative
            representative[i] = i;
            // Intialize the size of all groups to 1
            size[i] = 1;
        }
    }
    
    // Finds the representative of group x
    int findRepresentative(int x) {
        if (x == representative[x]) {
            return x;
        }
        
        // This is path compression
        return representative[x] = findRepresentative(representative[x]);
    }
    
    // Unite the group that contains "a" with the group that contains "b"
    void unionBySize(int a, int b) {
        int representativeA = findRepresentative(a);
        int representativeB = findRepresentative(b);
        
        // If nodes a and b already belong to the same group, do nothing.
        if (representativeA == representativeB) {
            return;
        }
        
        // Union by size: point the representative of the smaller
        // group to the representative of the larger group.
        if (size[representativeA] >= size[representativeB]) {
            size[representativeA] += size[representativeB];
            representative[representativeB] = representativeA;
        } else {
            size[representativeB] += size[representativeA];
            representative[representativeA] = representativeB;
        }
    }
};

class Solution {
public:
    vector<vector<string>> accountsMerge(vector<vector<string>>& accountList) {
        int accountListSize = accountList.size();
        DSU dsu(accountListSize);
        
        // Maps email to their component index
        unordered_map<string, int> emailGroup;
        
        for (int i = 0; i < accountListSize; i++) {
            int accountSize = accountList[i].size();

            for (int j = 1; j < accountSize; j++) {
                string email = accountList[i][j];
                string accountName = accountList[i][0];
                
                // If this is the first time seeing this email then
                // assign component group as the account index
                if (emailGroup.find(email) == emailGroup.end()) {
                    emailGroup[email] = i;
                } else {
                    // If we have seen this email before then union this
                    // group with the previous group of the email
                    dsu.unionBySize(i, emailGroup[email]);
                }
            }
        }
    
        // Store emails corresponding to the component's representative
        unordered_map<int, vector<string>> components;
        for (auto emailIterator : emailGroup) {
            string email = emailIterator.first;
            int group = emailIterator.second;
            components[dsu.findRepresentative(group)].push_back(email);
        }

        // Sort the components and add the account name
        vector<vector<string>> mergedAccounts;
        for (auto componentIterator : components) {
            int group = componentIterator.first;
            vector<string> component = {accountList[group][0]};
            component.insert(component.end(), componentIterator.second.begin(), 
                             componentIterator.second.end());
            sort(component.begin() + 1, component.end());
            mergedAccounts.push_back(component);
        }
        
        return mergedAccounts;
    }
};
```

Here `N` is the number of accounts and `K` is the maximum length of an account.

-   Time complexity: `O(NK * log NK)`
    
    While merging we consider the size of each connected component and we always choose the representative of the larger component to be the new representative of the smaller component, also we have included the path compression so the time complexity for `find/union` operation is `α(N)` (Here, `α(N)` is the inverse Ackermann function that grows so slowly, that it doesn't exceed `4` for all reasonable `N` (approximately `N < 10^{600}`).
    
    We find the representative of all the emails, hence it will take `O(N K α(N))` time. We are also sorting the components and the worst case will be when all emails end up belonging to the same component this will cost `O(NK(logNK))`.
    
    Hence the total time complexity is `O(NK⋅logNK+NK⋅α(N))`.
    
-   Space complexity: `C++ - O(log N * K) / Java - O(NK)`
    
    List `representative`, `size` store information corresponding to each group so will take `O(N)` space. All emails get stored in `emailGroup` and `component` hence space used is `O(NK)`.
    
    The space complexity of the sorting algorithm depends on the implementation of each programming language. For instance, in Java, Collections.sort() dumps the specified list into an array this will take `O(NK)` space then Arrays.sort() for primitives is implemented as a variant of quicksort algorithm whose space complexity is `O(logNK)`. In C++ `sort()` function provided by STL is a hybrid of Quick Sort, Heap Sort, and Insertion Sort with the worst-case space complexity of `O(logNK)`.