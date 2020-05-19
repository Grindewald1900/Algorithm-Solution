# 1. Longest Palindromic Substring

## Description:

### Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.


Example:

Example 1:

Example 1:

Input: "babad"
Output: "bab"  
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"

## Solution 1.0
A sliding window, complexity from O(n) to O(n^2).Loop from the first char, if char[i] equals to char[i+1] or char[i+2], it is supposed to be 
a pivot of a palindromic substring.
```java
class Solution {
    public String longestPalindrome(String s) {
        int size = s.length();
        char str[] = s.toCharArray();
        String result;
        int max=1, tempMax=0, start=0, end=0, i=0, j=0, k=0;

        switch(size){
            case 0:
                return "";
            case 1:
                return s;
            case 2:
                return str[0] == str[1] ? s : s.substring(0,1);
        }
        for(i=0; i<size-2; i++){
            j = 0;
            k = 0;
            if(str[i] == str[i+1]){
                j = i;
                k = i+1;
                while(j>-1 && k<size){
                    if(str[j] == str[k]){
                        tempMax = k-j+1;
                        j--;
                        k++;
                    }else{
                        break;
                    }
                }
                if(tempMax > max){
                    max = tempMax;
                    start = j+1;
                    end = k-1;
                }
            }
            if(str[i] == str[i+2]){
                j = i;
                k = i+2;
                while(j>-1 && k<size){
                    if(str[j] == str[k]){
                        tempMax = k-j+1;
                        j--;
                        k++;
                    }else{
                        break;
                    }
                }
                if(tempMax > max){
                    max = tempMax;
                    start = j+1;
                    end = k-1;
                }
            }
        }
        if(max == 1){
            if(str[size-2] == str[size-1]){
                start = size-2;
                end = size-1;
            }else{
                end = 0;
            }
        }
        return s.substring(start,end+1);
    }
}
```
Runtime: 8 ms, faster than 87.48% of Java online submissions for Longest Palindromic Substring.
Memory Usage: 38.2 MB, less than 39.92% of Java online submissions for Longest Palindromic Substring

## Solution 1.1
Abstract the function extendPivot(), remove some duplicate variables.
```java
class Solution {
    private int start=0, end=0, max=1, tempMax=0;
    public String longestPalindrome(String s) {
        int size = s.length();
        char str[] = s.toCharArray();
        String result;
        int i = 0;

        switch(size){  //deal with small size of input 
            case 0:
                return "";
            case 1:
                return s;
            case 2:
                return str[0] == str[1] ? s : s.substring(0,1);
        }
        for(i=0; i<size-2; i++){
            if(str[i] == str[i+1]){ 
                extendPivot(str, i, i+1, size);
            }
            if(str[i] == str[i+2]){   //in case of the condition :"aaa" or "aaaa" 
                extendPivot(str, i, i+2, size);
            }
        }
        if(max == 1){
            return str[size-2] == str[size-1] ? s.substring(size-2, size) : s.substring(0, 1);
        }
        return s.substring(start,end+1);
    }
    
    private void extendPivot(char[] str, int j, int k, int size){
         while(j>-1 && k<size){
             if(str[j] == str[k]){
                tempMax = k-j+1;
                j--;
                k++;  
             }else{
                break;
             }
         }
         if(tempMax > max){
             max = tempMax;
             start = j+1;
             end = k-1;
         }
    }
}
```

