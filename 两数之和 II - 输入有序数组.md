#### [167. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

难度简单362

给定一个已按照***升序排列\*** 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2*。*

**说明:**

- 返回的下标值（index1 和 index2）不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

**示例:**

```
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

这题用双重for这种简单的暴力是可以水过去的但这里重点不是这两种方法。

这道题可以使用 [两数之和](https://leetcode-cn.com/problems/two-sum/) 的解法，使用 O(n^2) 的时间复杂度和 O(1)的空间复杂度暴力求解，或者借助哈希表使用 O(n)的时间复杂度和 O(n) 的空间复杂度求解。但是这两种解法都是针对无序数组的，没有利用到输入数组有序的性质。利用输入数组有序的性质，可以得到时间复杂度和空间复杂度更优的解法。

#### 方法一：二分查找

在数组中找到两个数，使得它们的和等于目标值，可以首先固定第一个数，然后寻找第二个数，第二个数等于目标值减去第一个数的差。利用数组的有序性质，可以通过二分查找的方法寻找第二个数。为了避免重复寻找，在寻找第二个数时，只在第一个数的右侧寻找。

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        for (int i = 0; i < numbers.length; ++i) {
            int low = i + 1, high = numbers.length - 1;
            while (low <= high) {
                int mid = (high - low) / 2 + low;
                if (numbers[mid] == target - numbers[i]) {
                    return new int[]{i + 1, mid + 1};
                } else if (numbers[mid] > target - numbers[i]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }
        }
        return new int[]{-1, -1};
    }
}
```

**复杂度分析**

- 时间复杂度：O*(*n*log*n)，其中 n是数组的长度。需要遍历数组一次确定第一个数，时间复杂度是 *O*(*n*)，寻找第二个数使用二分查找，时间复杂度是O*(log*n*)，因此总时间复杂度是 O*(*n*log*n*)。
- 空间复杂度：O(1)。

### 第二种双指针比较好理解这里直接放代码了

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int low = 0, high = numbers.length - 1;
        while (low < high) {
            int sum = numbers[low] + numbers[high];
            if (sum == target) {
                return new int[]{low + 1, high + 1};
            } else if (sum < target) {
                ++low;
            } else {
                --high;
            }
        }
        return new int[]{-1, -1};
    }
}
```

**复杂度分析**

- 时间复杂度：O(n)，其中 n 是数组的长度。两个指针移动的总次数最多为 n 次。
- 空间复杂度：O(1)