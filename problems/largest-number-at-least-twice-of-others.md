# Find All Numbers Disappeared in an Array - from [LeetCode](https://leetcode.com)
[View this problem on LeetCode](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/)

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:

Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]

## My Solution - Version I
```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> res = new ArrayList<Integer>();
        
        for (int i = 0; i < nums.length; i++){
            int val = Math.abs(nums[i]) - 1;
            if (nums[val] > 0)
                nums[val] = -(nums[val]);
        }
        
        for (int i = 0; i < nums.length; i++){
            if (nums[i] > 0)
                res.add(i+1);
        }
        return res;
    }
}
```

Time Complexity: O(n)

Space Complexity: O(1)