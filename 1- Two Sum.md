# 1. Two Sum 

## Description:

### Given an array of integers, return indices of the two numbers such that they add up to a specific target.

### You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

## Solution 1.0
Double loop, complexity O(n^2)
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int size = nums.length;
        int[] r = new int[2];
        for(int i=0; i<size; i++ ){
            int temp = target - nums[i];
            for(int j=i+1; j<size; j++){
                if(nums[j] == temp){
                    r[0] = i;
                    r[1] = j;
                }
            }
        }
        return r;
    }
}
```
Runtime: 47 ms, faster than 25.97% of Java online submissions for Two Sum.
Memory Usage: 39.3 MB, less than 8.27% of Java online submissions for Two Sum.

## Solution 2.0
Use a HashMap, which has a O(1) complexity(the worst case is O(n)), instead of the for loop to find the complement number of nums[i].

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int temp = target - nums[i];
        if (map.containsKey(temp) && map.get(temp) != i) {
            return new int[] { i, map.get(temp) };
        }
    }
    throw new IllegalArgumentException("No solution!");
    }
}
```
Runtime: 2 ms, faster than 80.73% of Java online submissions for Two Sum.
Memory Usage: 41.9 MB, less than 5.65% of Java online submissions for Two Sum.


## Solution 2.1
Then, I remove the element in the HashMap if nums[i] is not the exact solution, so that the scale of the HashMap will decrease with the iterations.

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int temp = target - nums[i];
        if (map.containsKey(temp) && map.get(temp) != i) {
            return new int[] { i, map.get(temp) };
        }else{
            map.remove(nums[i]);
        }
    }
    throw new IllegalArgumentException("No solution!");
    }
}
```
Runtime: 3 ms, faster than 50.04% of Java online submissions for Two Sum.
Memory Usage: 41.8 MB, less than 5.65% of Java online submissions for Two Sum.


