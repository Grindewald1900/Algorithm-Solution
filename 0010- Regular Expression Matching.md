# 10- Regular Expression Matching

## Description:
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.  

'.' Matches any single character.  
'*' Matches zero or more of the preceding element.  
The matching should cover the entire input string (not partial).  

Note:  

s could be empty and contains only lowercase letters a-z.  
p could be empty and contains only lowercase letters a-z, and characters like . or *.  

### Example 1:

Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
### Example 2:

Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
### Example 3:

Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
### Example 4:

Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
### Example 5:

Input:
s = "mississippi"
p = "mis*is*p*."
Output: false

## Solution 1.0
This is a wrong solution and I'm confused about the test case until now...  
1. Traverse the pattern and string with two pointers.  
2. For each iteration, cope with the character in pattern.
3. When the character is '.', pointer1++.  
4. When the character is '*', compare pattern.charAt(pointer2-1) with string.charAt(pointer).

```java
class Solution {
    private int s1, s2; 
    private int p1 = 0, p2 = 0;
    private String s0;

    public boolean isMatch(String s, String p) {
        s0 = s;
        s1 = s.length();
        s2 = p.length();
        while(p2 < s2){
            switch(p.charAt(p2)){
                case '.':
                    matchPoint();
                    break;
                case '*':
                    if(matchStar(p.charAt(p2-1))){
                        return true;
                    }
                    break;
                default:
                    if(p.charAt(p2) != s.charAt(p1)){
                        p2++;
                    }else{
                        p1++;
                        p2++;
                    }
                    break;
            }
            if(p1 == s1){
                return true;
            }
        }
        return false;
    }

    private void matchPoint(){
        p1++;
        p2++;
    }

    private boolean matchStar(char c){
        if(c == '.'){
            return true;
        }
        if(s0.charAt(p1) == c){
            p1++;
            if(p1 == s1){
                return true;
            }
            matchStar(c);
        }else{
            p2++;
        }
        return false;
    }
}
```

## Solution 2.0




