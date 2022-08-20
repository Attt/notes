[剑指 Offer II 006. 排序数组中两个数字之和](https://leetcode.cn/problems/kLl5u1/)

跟[剑指 Offer 57. 和为s的两个数字](../%E5%89%91%E6%8C%87%20Offer%2057/%E5%89%91%E6%8C%87%20Offer%2057.md)一样的题目。。


```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int l = 0, r = numbers.length - 1;
        while(l < r){
            int sum = numbers[l] + numbers[r];
            if(sum < target) l++;
            else if(sum > target) r--;
            else return new int[]{l, r};
        }
        return new int[0];
    }
}
```