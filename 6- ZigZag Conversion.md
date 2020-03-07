# 1. Longest Substring Without Repeating Characters 

## Description:

### The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

P   A   H   N  
A P L S I I G  
Y   I   R  
### And then read line by line: "PAHNAPLSIIGYIR"

### Write the code that will take a string and make this conversion given a number of rows:

### string convert(string s, int numRows);

## Example:

Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3.   
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.  
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Solution 1.0
Divide the problem into three parts:  
(1) The first line of the ZigZag  
(2) The medial lines of the ZigZag(if have)  
(3) The last line of the ZigZag(if have)  
![a](http://15.222.11.163/wp-content/uploads/2020/03/LeetCode-6-2.png)
![a2](http://15.222.11.163/wp-content/uploads/2020/03/LeetCode-6-3.png)
```java
class Solution {
    public String convert(String s, int numRows) {
        int size = s.length();
        char[] str = s.toCharArray();
        char[] result = new char[size];
        int n=0, m=0 , pointer=0;
        if(numRows == 1){
            return s;
        }

        while(pointer < size){
            result[n++] = str[pointer];
            pointer = 2*n*(numRows-1);
        }

        for(int row=1; row<numRows-1; row++){
            int column = 0, p=row;
            while(p < size){
                result[n++] = str[p];
                column++;
                p = (0 == column%2) ? row + column*(numRows-1) : row + (column+1)*(numRows-1) - 2*row;
            }
        }
        pointer = numRows - 1;
        while(pointer < size){
            result[n++] = str[pointer];
            m++;
            pointer = (2*m + 1)*(numRows - 1);
        }
        return String.valueOf(result);
    }
}
```
Runtime: 2 ms, faster than 100.00% of Java online submissions for ZigZag Conversion.
Memory Usage: 41.4MB, less than 19.15% of Java online submissions for ZigZag Conversion.

## Solution 1.1

```java
class Solution {
    public String convert(String s, int numRows) {
        int size = s.length();
        char[] str = s.toCharArray(), result = new char[size] ;
        int n=0, pointer=0, pointer1=0, pointer2=numRows - 1;
        int column1=0, column2=0;

        if(numRows == 1){
            return s;
        }

        while(pointer1 < size){
            result[n++] = str[pointer1];
            pointer1 = 2*n*(numRows-1);
        }
        for(int row=1; row<numRows-1; row++){
            column1 = 0;
            pointer = row;
            while(pointer < size){
                result[n++] = str[pointer];
                column1++;
                pointer = (0 == column1%2) ? row + column1*(numRows-1) : row + (column1+1)*(numRows-1) - 2*row;
            }
        }
        while(pointer2 < size){
            result[n++] = str[pointer2];
            column2++;
            pointer2 = (2*column2 + 1)*(numRows - 1);
        }
        return String.valueOf(result);
    }
}
```
Runtime: 2 ms, faster than 100.00% of Java online submissions for ZigZag Conversion.
Memory Usage: 41.6B, less than 19.15% of Java online submissions for ZigZag Conversion.




