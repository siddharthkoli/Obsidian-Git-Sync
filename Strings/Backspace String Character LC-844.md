#twopointers 

Approach 1: Remove the '#' character and check if the strings are equal using StringBuilder.
``` java
public boolean backspaceCompare(String s, String t) {
        return sBuilder(s).equals(sBuilder(t));
    }
    private static String sBuilder(String s)
    {
        StringBuilder sbr = new StringBuilder();
        
        for(char c : s.toCharArray())
        {
            if(c != '#')
                sbr.append(c);
            else if(sbr.length() != 0)
                sbr.deleteCharAt(sbr.length() - 1);
        }
        return sbr.toString();
    }
```
Time:O (n + m)
Space: O(n + m)

Approach 2: using two pointers
Start pointing the 2 strings from the end and store a variable which keeps a track of number of '#' characters are present in the string.
If skips are greater than 0, decrement the pointer and if we do not encounter any '#', just break the loop.
``` java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        int S_pointer = s.length() - 1;
        int T_pointer = t.length() - 1;
        
        int s_skips = 0;
        int t_skips = 0;
        
        while(S_pointer >= 0 || T_pointer >= 0)
        {
        while(S_pointer >= 0)
        {
            if(s.charAt(S_pointer) == '#')
            {
                s_skips += 1;
                S_pointer -= 1;
            }
            else if(s_skips > 0)
            {
                S_pointer -= 1;
                s_skips -= 1;
               
            }
            else { break; }
        }
        
        while(T_pointer >= 0)
        {
            if(t.charAt(T_pointer) == '#')
            {
                t_skips += 1;
                T_pointer -= 1;
            }
            else if(t_skips > 0)
            {
                t_skips -= 1;
                T_pointer -= 1;
            }
            else { break; }
        }
        
        //check if the pointers pointing to characters are equal
        if(S_pointer >= 0 && T_pointer >= 0 && s.charAt(S_pointer) != t.charAt(T_pointer))
        {
            return false;
        }
        
        //check length
        if((S_pointer >= 0) != (T_pointer >= 0) )
            return false;
        
        S_pointer -= 1;
        T_pointer -= 1;
        
    
    }
        return true;
    }
    
}
```
Time : O(n + m)
Space: O(1) 

Approach 3: Using stacks
```java
 public boolean backspaceCompare(String s, String t) {
        Stack<Character> s1 = new Stack<>();
        Stack<Character> s2 = new Stack<>();
    
        
        for(int i = 0; i<s.length(); i++)
        {
            if(s.charAt(i) != '#')
                s1.push(s.charAt(i) );
            else if( !s1.isEmpty())
                s1.pop();
        }
        
        for(int i = 0; i<t.length(); i++)
        {
            if(t.charAt(i) != '#')
                s2.push(t.charAt(i) );
            else if( !s2.isEmpty())
                s2.pop();
        }
        
        return s1.equals(s2);
    }
```
Time Complexity : O(N + M)
Space Complexity : O(N + M)