[题目链接](https://leetcode-cn.com/problems/2VG8Kg/)

思路：可以采用滑动窗口的方法，遍历一遍就找到最终的值，我们最初让left和right都指向第一个值，同时维护一个sum，表示left和right之间所有数字的和，每次循环让right递增，然后sum对应增加。如果此时sum>=target，那就让left--，同时更新sum和result，直到sum < target

**复杂度分析**
+  时间复杂度：左右指针各遍历了一遍数组，所以是O(N)
+  空间复杂度：O(1)

```java
public int minSubArrayLen(int target, int[] nums) {
        int result = Integer.MAX_VALUE, left = 0, right = 0, sum = 0;

        for (right = 0; right < nums.length; right++) {

            sum += nums[right];
            while (sum >= target && left <= right) {
                result = Math.min(result, right - left + 1);
                sum -= nums[left++];
            }
        }

        return Integer.MAX_VALUE == result ? 0 : result;
    }
```