# 1. Longest Substring Without Repeating Characters 

## Description:

### Given a string, find the length of the longest substring without repeating characters.

Example:

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
Double for loop, complexity O(n^2)
```java
class Solution {
     public int lengthOfLongestSubstring(String s) {
        int size = s.length();
        char[] str = s.toCharArray();
        if(size < 2){
            return size;
        }
        int max = 0;
        Map<Character, Integer> m = new HashMap<>();
        for(int i=0; i<size-1; i++){
            m.put(str[i],i);
            for(int j=i+1; j<size; j++){
                if(m.containsKey(str[j])){
                    if(j-i > max){
                        max = j-i;
                    }
                    break;
                }else{
                    if(j-i+1 > max){
                        max = j-i+1;
                    }
                    m.put(str[j],j);
                }
            }
            m.clear();
        }
        return max;
    }
}
```
Runtime: 82 ms, faster than 13.69% of Java online submissions for Longest Substring Without Repeating Characters.
Memory Usage: 42.1 MB, less than 5.20% of Java online submissions for Longest Substring Without Repeating Characters.

## Solution 2.0
Use a sliding window, which means a window between int i and int j, move the window from start to end.If there's a duplicate character when moving,
remove all the characters before the first duplicate character.



```java
class Solution {
     public int lengthOfLongestSubstring(String s) {
        int size = s.length();
        char[] str = s.toCharArray();
        int max = 0, i=0, j=0;
        Map<Character, Integer> m = new HashMap<>();
        while(i<size && j<size){
            if(!m.containsKey(str[j])){
                if(max< j-i+1){
                    max = j-i+1;
                }
            }else{
                int k =  m.get(str[j]);
                for(int t=i; t<k+1; t++){
                    m.remove(str[t]);
                }
                i = k + 1;
            }
            m.put(str[j],j);
            j++;
        }
        return max;
    }
}
```
Runtime: 7 ms, faster than 70.85% of Java online submissions for Longest Substring Without Repeating Characters.
Memory Usage: 41.7 MB, less than 5.20% of Java online submissions for Longest Substring Without Repeating


## Something related
### Sliding Window Algorithm 

![avatar](https://miro.medium.com/max/332/1*202N86YExc2Y3JupOZZptQ.png) 


