# 1. Longest Substring Without Repeating Characters 

## Description:

### There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

### Example:

nums1 = [1, 3]
nums2 = [2]

The median is 2.0
Example 2:

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
## Solution 1.0
Pick up the element from two arrays with ascending order until find the median(one or two integer).
```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length, n = nums2.length;
        int i = 0, j = 0;
        int mid = (m+n+2)/2;
        int[] s = new int[mid];
        boolean odd = (m+n)%2 == 1 ? true : false;

        while(i+j < mid){
            if(i>=m){
                s[i+j] = nums2[j++];
            }else if(j>=n){
                s[i+j] = nums1[i++];
            }else{
                s[i+j] = nums1[i] < nums2[j] ? nums1[i++] : nums2[j++];
            }
        }
        return odd ? (double) s[mid-1] : (double)(s[mid-1] + s[mid-2])/2;
    }
}
```
Runtime: 2 ms, faster than 99.87% of Java online submissions for Median of Two Sorted Arrays.
Memory Usage: 41.8 MB, less than 100.00% of Java online submissions for Median of Two Sorted Arrays.



