### [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

难度简单122

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
```

这是我的代码，本来以为水不过去呢哈哈哈哈

```java
public int findRepeatNumber(int[] nums) {
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (nums[i]==nums[i+1]){
                return nums[i];
            }

        }
        return 0;
    }
```

耗时3ms，内存空间击败百分之百

# 面试题03. 数组中重复的数字

[力扣官方题解](https://leetcode-cn.com/u/leetcode-solution/)发布于 2020-02-2048.8k**官方**Java

### 方法一：遍历数组

由于只需要找出数组中任意一个重复的数字，因此遍历数组，遇到重复的数字即返回。为了判断一个数字是否重复遇到，使用集合存储已经遇到的数字，如果遇到的一个数字已经在集合中，则当前的数字是重复数字。

- 初始化集合为空集合，重复的数字 `repeat = -1`
- 遍历数组中的每个元素：
  - 将该元素加入集合中，判断是否添加成功
    - 如果添加失败，说明该元素已经在集合中，因此该元素是重复元素，将该元素的值赋给 `repeat`，并结束遍历
- 返回 `repeat`

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set = new HashSet<Integer>();
        int repeat = -1;
        for (int num : nums) {
            if (!set.add(num)) {
                repeat = num;
                break;
            }
        }
        return repeat;
    }
}
```

**复杂性分析**

- 时间复杂度：

  O(n)

  - 遍历数组一遍。使用哈希集合（`HashSet`），添加元素的时间复杂度为 O(1)，故总的时间复杂度是 O(n)

- 空间复杂度：O(n)。不重复的每个元素都可能存入集合，因此占用 O(n) 额外空间。

### 此外

还有一种精妙的方法，直接上代码了

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        int temp;
        for(int i=0;i<nums.length;i++){
            while (nums[i]!=i){
                if(nums[i]==nums[nums[i]]){
                    return nums[i];
                }
                temp=nums[i];
                nums[i]=nums[temp];
                nums[temp]=temp;
            }
        }
        return -1;
    }
}

```

