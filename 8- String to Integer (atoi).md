## 8- String to Integer (atoi).md

### Description:

**Implement atoi which converts a string to an integer. The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value. The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function. If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
If no valid conversion could be performed, a zero value is returned.  
Note:  
Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.**

### Example 1:

Input: "42"
Output: 42
### Example 2:

Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
### Example 3:

Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
### Example 4:

Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
### Example 5:

Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.

## Solution 1.0
Use a pointer to scan every digit from left to right.   
1. Check digit until a non-space character.
2. Check the positive or negative sign(if exist)
3. Figure out the result with a while loop(in case the first few zero character)
4. Work out the final result(with a sign multiplied)
5. Check if the result is out of Integer bound.

```java
public class Solution {
    public static int myAtoi(String str) {
        if (str == null || str.isEmpty()) {
            return 0;
        }
        boolean isPositive = true;
        int multi = 1;
        int pointer = 0;
        int size = str.length();
        long result = 0;

        while(pointer < size && str.charAt(pointer)==' '){
            pointer++;
        }
        if(pointer >= size){
            return 0;
        }
        switch(str.charAt(pointer)){
            case '-':
                isPositive = false;
                pointer++;
                break;
            case '+':
                pointer++;
            default:
                break;
        }
        multi = isPositive ? 1 : -1;
        while(pointer < size && Character.isDigit(str.charAt(pointer))){
            result = result*10 + str.charAt(pointer) - '0';
            pointer++;
            if(result*multi > Integer.MAX_VALUE){
                return Integer.MAX_VALUE;
            }
            if(result*multi < Integer.MIN_VALUE){
                return Integer.MIN_VALUE;
            }
        }
        return (int)result*multi;
    }
}
```
Runtime: 2 ms, faster than 79.83% of Java online submissions for String to Integer (atoi).
Memory Usage: 39.4 MB, less than 5.59% of Java online submissions for String to Integer (atoi).

