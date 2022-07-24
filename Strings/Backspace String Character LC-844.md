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

Approach 2: using two pointers
Start pointing the 2 strings from the end and store a variable which keeps a track of number of '#' characters are present in the string.