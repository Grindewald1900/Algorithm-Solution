# 7. Reverse Integer

## Description:

### Given a 32-bit signed integer, reverse digits of an integer.

## Example:
Example 1:  

Input: 123
Output: 321

Example 2:  

Input: -123
Output: -321

Example 3:  

Input: 120
Output: 21

## Solution 1.0
将int转为long（如果x值为MIN_VALUE，转为正数会越界）  
转为字符串，调换顺序  
转回long，判断是否超出int范围  
超出返回0，不超出返回结果result  

```java
class Solution {
    public static int reverse(int x) {
        boolean isPositive = x >= 0;
        long lx = x;
        if(!isPositive){
            lx = lx * (-1);
        }
        String s = String.valueOf(lx);
        StringBuilder r = new StringBuilder(s);
        int size = s.length();
        long result;

        for(int i=0; i<size; i++){
            r.setCharAt(i,s.charAt(size-1-i));
        }
        result = isPositive == true ? Long.valueOf(r.toString()) : Long.valueOf(r.toString()) * (-1);
        return (result >= Integer.MIN_VALUE && result <= Integer.MAX_VALUE) ? (int)result : 0;
    }
}
```
Runtime: 2 ms, faster than 29.98% of Java online submissions for Reverse Integer.
Memory Usage: 37.4 MB, less than 5.55% of Java online submissions for Reverse Integer.ers.

## Solution 2.0
数字计算：  
remain: 余数  
lx:剩余未计算的部分  
result:最后结果  
```java
 while(lx > 0){
     remain = lx%10;
     lx = lx/10;
     result = result*10 + remain  
 }
```
完整代码如下
```java
class Solution {
   public static int reverse(int x) {
        boolean isPositive = x < 0 ? false : true;
        if(x == Integer.MIN_VALUE){
            return 0;
        }
        long lx = x;
        if(!isPositive){
            lx = lx*(-1);
        }
        long remain, result=0;

        while(lx > 0){
            remain = lx%10;
            lx = lx/10;
            result = result*10 + remain;
        }
        result = isPositive ? result : result*(-1);
        return (result < Integer.MIN_VALUE || result > Integer.MAX_VALUE) ? 0 : (int)result;
    }
}
```
Runtime: 1 ms, faster than 100.00% of Java online submissions for Reverse Integer.
Memory Usage: 37.2 MB, less than 5.55% of Java online submissions for Reverse Integer.




