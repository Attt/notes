[剑指 Offer II 074. 合并区间](https://leetcode.cn/problems/SsGoHC/)

输入：[[1,3],[2,6],[8,10],[15,18]]

s: start

e: end

s1 s2 e3 e6 s8 e10 s15 e18

用栈保存s，空栈第一个s就是当前的[x,y]中的x，遇到e就pop，如果pop完了s，那么当前的e就是[x,y]中的y...

好像不大对


按照区间的第一位排序，然后比较新区间的头和答案中最后一个区间的尾巴大小，用来判断是否重叠。

如果新区间的尾巴要大于最后一个区间的尾巴，说明不是包含的case，更新答案中最后一个区间的尾巴就行了。
结果是可以修改的！

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        // 按照区间的head升序排序
        Arrays.sort(intervals, Comparator.comparingInt(o -> o[0]));

        List<int[]> ans = new ArrayList<>();
        for (int[] interval : intervals) {
            if (ans.size() > 0) {
                if (interval[0] <= ans.get(ans.size() - 1)[1]) { // 后一个区间的head小于等于前一个区间的tail，说明重叠
                    if(interval[1] > ans.get(ans.size() - 1)[1]) {
                        // 当后一个区间的tail大于前一个区间的tail时，更新前一个区间的tail为新的tail
                        ans.get(ans.size() - 1)[1] = interval[1];
                    }
                    continue;
                }
            }
            ans.add(interval);
        }

        return ans.toArray(new int[0][]);
    }
}
```

