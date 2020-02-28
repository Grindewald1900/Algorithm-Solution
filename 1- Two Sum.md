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
```
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

