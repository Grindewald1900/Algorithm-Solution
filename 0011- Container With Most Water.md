# 11- Container With Most Water

## Description:
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
  
Note: You may not slant the container and n is at least 2.

### Example:  
![avatar](http://15.222.11.163/wp-content/uploads/2020/05/leet11.jpg) 


Input: [1,8,6,2,5,4,8,3,7]  
Output: 49

## Solution 1.0
Very simple solution with two layer of For loop
```java
class Solution {
    public int maxArea(int[] height) {
        int s = height.size();
        int max = 0, temp = 0;
        for(int i=0; i<s-1; i++){
            for(int j=i+1; j<s; j++){
                temp = min(height[i],height[j])*(j-i);
                if(max < temp){
                    max = temp;
                }
            }
        }
        return max;
    }

    private int min(int a, int b){
        return a<b ? a : b;
    }
}
```
Runtime: 373 ms, faster than 10.54% of Java online submissions for Container With Most Water.  
Memory Usage: 39.9 MB, less than 94.87% of Java online submissions for Container With Most Water.

## Solution 2.0
1. Make pointer1 scan from left and pointer2 scan form right.  
2. Calculate the area size.  
3. Move one of the pointers(the shorter side).  
4. When the pointers meets, loop end.  
```java
class Solution {
    public int maxArea(int[] height) {
        int max = 0, temp = 0, h = 0;
        int p1 = 0, p2 = height.length-1;
        while(p1 < p2){
            if(height[p1] < height[p2]){
                h = height[p1];
                p1++;
            }else{
                h = height[p2];
                p2--;
            }
            temp = h*(p2-p1+1);
            max = max < temp ? temp : max;
        }
        return max;
    }
}

```
Runtime: 1 ms, faster than 99.99% of Java online submissions for Container With Most Water.  
Memory Usage: 40 MB, less than 94.87% of Java online submissions for Container With Most Water.
https://leetcode.com/problems/container-with-most-water/solution/
