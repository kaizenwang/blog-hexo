---
title: 两个数组的交集II
date: 2019-06-01 09:46:47
tags:
---

题目：[两个数组的交集II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)



## 解法一

直接对数组进行比较，保存相同的元素，并将元素设置为 MAX_VALUE。

时间复杂度：O(n)

空间复杂度：O(n)

代码：

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        int[] k = new int[nums1.length];
        int s = 0;
        for (int i = 0; i < nums1.length; i++) {
            for (int j = 0; j < nums2.length; j++) {
                if (nums1[i] == nums2[j]) {
                    k[s++] = nums1[i];
                    nums1[i] = Integer.MAX_VALUE;
                    nums2[j] = Integer.MAX_VALUE;
                    break;
                }
            }
        }
        return Arrays.copyOf(k, s);
    }
}
```

## 解法二

对数组进行排序后求解，还是依次比较元素，相同的添加到新数组当中。

时间复杂度：O(n)
空间复杂度：O(n)
代码：

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int[] k = new int[nums1.length];
        int i = 0, j = 0;
        int index = 0;
        while (i++ < nums1.length && j++ < nums2.length) {
            if (nums1[i - 1] == nums2[j - 1]) {
                k[index++] = nums1[i - 1];
            } else if (nums1[i - 1] < nums2[j - 1]) {
                j--;
            } else {
                i--;
            }
        }
        return Arrays.copyOf(k, index);
    }
}
```

