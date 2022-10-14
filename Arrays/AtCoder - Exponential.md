You are given a positive integer X. Find the largest _perfect power_ that is at most X. Here, a perfect power is an integer that can be represented as b^p, where b is an integer not less than 1 and p is an integer not less than 2.

### Constraints
-   1≤ X ≤ 1000
-   X is an integer.

### Sample Test Cases
 - 10 - Output: 9
 - 1 - Output: 1
 - 999 - Output: 961

```cpp
void solve()
{
    int n, m, x, y, q, a, b, k;
    cin >> n;
    if (n == 1) {
        cout << 1 << endl;
        return;
    }
    v32 powers;
    for (int i = 2; i < 32; i++) {
        int curr = i;
        for (int j = 2; j <= 10; j++) {
            powers.push_back(curr * i);
            if (curr > n)
                break;
            curr = powers.back();
        }
    }
    sort(all(powers));
    cout << *prev(upper_bound(powers.begin(), powers.end(), n)) << endl;
}
```