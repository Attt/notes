[剑指 Offer 57. 和为s的两个数字](https://leetcode.cn/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int l = 0; l < nums.length; l++){
            for(int r = l + 1; r < nums.length; r++){
                // 满足条件
                if(nums[l] + nums[r] == target) return new int[]{nums[l], nums[r]};
                // 剪枝
                else if(nums[l] + nums[r] > target) break;
            }
        }
        return new int[]{};
    }
}
```
O(n^2)。。。超时了

l右移和r右移都让和增加，所以这题可以两个指针头尾逼近来找，这样如果小于和那就l右移，大于和那就r左移，那有没有可能错过呢？来证明一下：

首先，如果错过就说明l偏右或者r偏左，接下来无论如何移动都不会得到正确的答案。

1. 假如有四个数a b c d,且只有b和d的和满足条件s，开始的时候l=a，r=d，由于该序列递增，此时a+d < s，那么此时只能移动l。
2. 假如a b c d只有a+c=s，开始的时候l=a，r=d，此时a+d > s,只能移动r。
3. 假如a b c d只有b+c=s，同样l=a, r=d, 那么分两种情况：
    1. a+d > s, 此时首先r左移，得到a+c，又可知a+c < s，因此只能移动l。
    2. a+d < s, 此时首先l右移，得到b+d，又可知b+d > s，因此只能移动r。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        while(l < r){
            int sum = nums[l] + nums[r];
            if(sum < target) l++;
            else if(sum > target) r--;
            else return new int[]{nums[l], nums[r]};
        } 
        return new int[0];
    }
}
```
时间复杂度O(n)，空间复杂度O(1)
