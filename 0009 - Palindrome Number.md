# 9. Palindrome Number

## Description:

### Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

### Example 1:

Input: 121
Output: true
### Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
### Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

## Solution 1.0
1. Convert int to string.
2. Scan the string from two sides with two pointers.
3. Compare string.charAt(p) and string.charAt(size-p).

```java
class Solution {
    public boolean isPalindrome(int x) {
        String s = Integer.toString(x);
        int pointer2 = s.length()-1;
        int pointer1 = 0;
        while(pointer1 < pointer2){
            if(s.charAt(pointer1) != s.charAt(pointer2)){
                return false;
            }
            pointer1++;
            pointer2--;
        }
        return true;
    }
}
```
Runtime: 7 ms, faster than 74.46% of Java online submissions for Palindrome Number.
Memory Usage: 38.9 MB, less than 5.02% of Java online submissions for Palindrome Number.
