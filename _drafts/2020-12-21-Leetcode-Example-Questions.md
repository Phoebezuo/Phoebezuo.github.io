---
layout:     post
title:      Leetcode Example Questions
date:       2020-12-21
summary:    Summaries a few examples in Leetcode
categories: Leetcode Python Java
---

- [Sliding Window](#sliding-window)
  - [Maximum Subarray](#maximum-subarray)
  - [Minimum Size Subarray Sum](#minimum-size-subarray-sum)
  - [Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
  - [Max Consecutive Ones III](#max-consecutive-ones-iii)
  - [Longest Repeating Character Replacement](#longest-repeating-character-replacement)
- [Two Pointers](#two-pointers)
  - [Remove duplicates From Sorted Array](#remove-duplicates-from-sorted-array)
  - [Squares of a Sorted Array](#squares-of-a-sorted-array)
  - [Sort Colors](#sort-colors)
  - [Subarray Product Less Than k](#subarray-product-less-than-k)
  - [3Sum](#3sum)
  - [3Sum Closest](#3sum-closest)
- [Fast and Slow Pointers](#fast-and-slow-pointers)
  - [Linked List Cycle](#linked-list-cycle)
  - [Linked List Cycle II](#linked-list-cycle-ii)
  - [Happy Number](#happy-number)
- [Merge Intervals](#merge-intervals)
  - [Array](#array)
- [Cyclic Sort](#cyclic-sort)
- [In-place Reversal of a Linked List](#in-place-reversal-of-a-linked-list)
- [Tree BFS](#tree-bfs)
- [Two Heaps](#two-heaps)
- [Subsets](#subsets)
- [Modified Binary Search](#modified-binary-search)
- [Top k Elements](#top-k-elements)
- [K-way Merge](#k-way-merge)
- [0/1 Knapsack](#01-knapsack)
- [Topological Sort](#topological-sort)
- [Backtracking](#backtracking)
  - [Subsets](#subsets-1)
  - [SubSets II](#subsets-ii)
  - [Permutation](#permutation)
  - [Permutation II](#permutation-ii)
  - [Combination Sum](#combination-sum)
  - [Combination Sum II](#combination-sum-ii)
  - [Combination Sum III](#combination-sum-iii)
  - [Palindrome Partitioning](#palindrome-partitioning)
- [Courses Schedule](#courses-schedule)
  - [Course Schedule](#course-schedule)
  - [Course Schedule II](#course-schedule-ii)
  - [Course Schedule III](#course-schedule-iii)
  - [Course Schedule IV](#course-schedule-iv)
- [Stocking Problems](#stocking-problems)
  - [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)
  - [Best Time to Buy and Sell Stock II](#best-time-to-buy-and-sell-stock-ii)
  - [Best Time to Buy and Sell Stock III](#best-time-to-buy-and-sell-stock-iii)
  - [Best Time to Buy and Sell Stock IV](#best-time-to-buy-and-sell-stock-iv)
  - [Best Time to Buy and Sell Stock with Cooldown](#best-time-to-buy-and-sell-stock-with-cooldown)
  - [Best Time to Buy and Sell Stock with Transaction Fee](#best-time-to-buy-and-sell-stock-with-transaction-fee)

# Sliding Window

## [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

Given an integer array, find the contiguous subarray which has the largest sum and return its sum.

🖥 [Video Explanation](https://www.youtube.com/watch?v=m3-Yfqk9bqw&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=96&t=87s&ab_channel=Yufei)

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        largest: int = float('-inf')
        sum: int = 0

        for i in nums:

            # update sum to current element when sum is below zero
            if sum >= 0:
                sum += i
            else:
                sum = i

            if sum > largest:
                largest = sum

        return largest
```

## [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

Given a positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ **s**. If there isn't one, return 0 instead.

🖥 [Video Explanation](https://www.youtube.com/watch?v=1g754XV2uzk&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=164&ab_channel=Yufei)

```
Input: s = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: the subarray [4,3] has the minimal length under the problem constraint.
```

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        ans: int = float("inf")
        left: int = 0
        sum: int = 0

        for i in range(len(nums)):
            sum += nums[i]

            # achieve the condition
            while sum >= s:

                # i + 1 - left means the size of current array
                ans = min(ans, i + 1 - left)

                # subtract the left most element in array
                sum -= nums[left]
                left += 1

        # there does not exist sum >= s
        if ans == float("inf"):
            return 0
        else:
            return ans
```

## [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string s, find the length of the longest substring without repeating characters.

🖥 [Video Explanation](https://www.youtube.com/watch?v=7qrJdCUiqT8&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=165&ab_channel=Yufei)

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        ans: int = 0
        map: dict = {}
        left: int = 0

        for right in range(len(s)):

            # update left counter
            if s[right] in map:
                left = max(map[s[right]], left)

            ans = max(ans, right - left + 1)

            # record right char position in map
            map[s[right]] = right + 1

        return ans
```

## [Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

Given an array A of 0s and 1s, we may change up to K values from 0 to 1. Return the length of the longest (contiguous) subarray that contains only 1s.

🖥 [Video Explanation](https://www.youtube.com/watch?v=1RIjTE6_bpg&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=167&ab_channel=Yufei)

```
Input: A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
Output: 6
Explanation: [1,1,1,0,0,1,1,1,1,1,1]
```

```python
class Solution:
    def longestOnes(self, A: List[int], K: int) -> int:
        left: int = 0
        ans: int = 0
        one_freq: int = 0

        for right in range(len(A)):

            # update the one's frequency
            if A[right] == 1:
                one_freq += 1

            sub_len: int = right - left + 1
            if sub_len - one_freq > K:

                # when replacement from 0 to 1 is bigger than K operations
                if A[left] == 1:
                    # if the left most is 1, decrease the one_freq
                    one_freq -= 1


                # update the left counter
                left += 1

            ans = max(ans, right - left + 1)

        return ans
```

## [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)

Given a string s and k operations on that string, each operation can replace any character to another character. Find the length of substring containing most repeating letters.

🖥 [Video Explanation](https://www.youtube.com/watch?v=sPmhLhcEJ7Q&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=168&ab_channel=Yufei)

```
Input: s = "AABABBA", k = 1
Output: 4
Explanation:
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count: List[int] = [0]*26
        left: int = 0
        most_freq: int = 0
        ans: int = 0

        for right in range(len(s)):
            # update the character's frequency
            count[ord(s[right]) - ord('A')] += 1

            # find the most frequent character
            most_freq = max(most_freq, count[ord(s[right]) - ord('A')])

            sub_len = right - left + 1
            if sub_len - most_freq > k:
                # when the place for replacement is bigger than k operations
                # move left cursor, decrement the frequency of left most
                count[ord(s[left]) - ord('A')] -= 1
                left += 1
            else:
                ans = max(ans, sub_len)

        return ans
```
# Two Pointers

## [Remove duplicates From Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given a sorted array, remove the duplicates in-place such that each element appears only once and returns the new length.

🖥 [Video Explanation](https://www.youtube.com/watch?v=sixDoo1ztbg&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=161&t=2s&ab_channel=Yufei)

```
Input: nums = [1,1,2]
Output: 2, nums = [1,2]
Explanation: Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the returned length.
```

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        left: int = 0

        for right in range(len(nums)):
            if nums[right] != nums[left]:
                left += 1

                # update the value at left cursor if they have different value
                nums[left] = nums[right]

        return left + 1
```

## [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

🖥 [Video Explanation](https://www.youtube.com/watch?v=IXKig_6SuS4&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=160&ab_channel=Yufei)

```
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
```

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        ans_idx: int = 0
        ans: List[int] = list()

        # located two pointers at the middle
        [right, left] = self.locate_pointer(nums)

        # append smaller square from each side of pointers
        while left >= 0 and right < len(nums):
            if nums[left] * nums[left] < nums[right] * nums[right]:
                ans.append(nums[left] * nums[left])
                left -= 1
            else:
                ans.append(nums[right] * nums[right])
                right += 1

        # loop through the remaining element in the list if unbalanced
        while left >= 0:
            ans.append(nums[left] * nums[left])
            left -= 1
        while right < len(nums):
            ans.append(nums[right] * nums[right])
            right += 1

        return ans

    def locate_pointer(self, nums: List[int]) -> List[int]:

        # right pointer is located at the first non-negative number
        right: int = 0
        while right < len(nums) and nums[right] < 0:
            right += 1

        left: int = right - 1

        return [right, left]
```

## [Sort Colors](https://leetcode.com/problems/sort-colors/)

Given an array, sort them in-place so that objects of the same color are adjacent. Notes: use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

🖥 [Video Explanation](https://www.youtube.com/watch?v=Ny7wVpW0M2E&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=155&ab_channel=Yufei)

```
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """

        left: int = 0
        right: int = len(nums)-1
        i = len(nums) - 1

        while left <= i:

            # exchange value of 2 to right most
            if nums[i] == 2:
                nums[i], nums[right] = nums[right], nums[i]
                right -= 1
                i -= 1

            # exchange value of 0 to left most
            elif nums[i] == 0:
                nums[i], nums[left] = nums[left], nums[i]
                left += 1s

            # do not change when current value is 1
            else:
                i -= 1
```

## [Subarray Product Less Than k](https://leetcode.com/problems/subarray-product-less-than-k/)

Given an array of positive integers nums. Count the number of (contiguous) subarrays where the product of all the elements in the subarray is less than k.

🖥 [Video Explanation](https://www.youtube.com/watch?v=3LGNf4HWEG8&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=157&ab_channel=Yufei)

```
Input: nums = [10, 5, 2, 6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        ans: int = 0
        left: int = 0
        prod: int = 1

        for right in range(len(nums)):
            prod *= nums[right]

            # when the product is too big
            while prod >= k and left <= right:

                # divide the left most from prod
                prod /= nums[left]

                # moves window towards right
                left += 1

            ans += right - left + 1

        return ans
```

## [3Sum](https://leetcode.com/problems/3sum/)

Given an array nums of n integers, find all unique triplets in the array which gives the sum of zero.

🖥 [Video Explanation](https://www.youtube.com/watch?v=aSSoPCd6DgI&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=159&ab_channel=Yufei)

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
```

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        ans: List[tuple] = []

        for i in range(len(nums)):
            left: int = i + 1
            right: int = len(nums) - 1

            while left < right:
                curr_sum: int = nums[i] + nums[left] + nums[right]

                if curr_sum == 0:
                    ans.append((nums[i], nums[left], nums[right]))
                    left += 1
                    right -= 1
                elif curr_sum < 0:
                    left += 1
                elif curr_sum > 0:
                    right -= 1

        return list(set(ans))
```

## [3Sum Closest](https://leetcode.com/problems/3sum-closest/)

Given an

🖥 [Video Explanation](https://www.youtube.com/watch?v=kjO3ibekIA0&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=158&ab_channel=Yufei)

```
```

```python
```

# Fast and Slow Pointers

## [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

Given an

🖥 [Video Explanation](https://www.youtube.com/watch?v=vFgnODhnBAM&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=154&ab_channel=Yufei)

```
```

```python
```

## [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

Given an

🖥 [Video Explanation](https://www.youtube.com/watch?v=VOWqqR8r6ac&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=153&ab_channel=Yufei)

```
```

```python
```

## [Happy Number](https://leetcode.com/problems/happy-number/)

Given an

🖥 [Video Explanation](https://www.youtube.com/watch?v=hbiORvvi3aA&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=151&ab_channel=Yufei)

```
```

```python
```

# Merge Intervals

## [Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

Given an

🖥 [Video Explanation](https://www.youtube.com/watch?v=sixDoo1ztbg&list=PLAe7SxBcDVNizQ8ezCReoa5w1OXWKrohz&index=161&t=2s&ab_channel=Yufei)

```
```

```python
```

# Cyclic Sort

# In-place Reversal of a Linked List

# Tree BFS

# Two Heaps

# Subsets

# Modified Binary Search

# Top k Elements

# K-way Merge

# 0/1 Knapsack

# Topological Sort

# Backtracking

## [Subsets](https://leetcode.com/problems/subsets/)

Given a set of **distinct** integers, return all possible subsets.

🖥 [Video Explanation](https://www.youtube.com/watch?v=znxeqMys_ac)

```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

``` java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        backtrack(ans, new ArrayList<Integer>(), nums, 0);
        return ans;
    }

    private void backtrack(List<List<Integer>> ans, List<Integer> temp, int[] nums, int start) {
        ans.add(new ArrayList<Integer>(temp));

        for (int i = start; i < nums.length; i++) {
            temp.add(nums[i]);
            backtrack(ans, temp, nums, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
```

## [SubSets II](https://leetcode.com/problems/subsets-ii/)

Given a set of **some duplicate** integers, return all possible subsets.

🖥 [Video Explanation](https://www.youtube.com/watch?v=hu7ez-Dv0r8)

```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

``` java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        Arrays.sort(nums); // easy to compare
        backtrack(ans, new ArrayList<Integer>(), nums, 0);
        return ans;
    }

    private void backtrack(List<List<Integer>> ans, List<Integer> temp, int[] nums, int start) {
        ans.add(new ArrayList<Integer>(temp));

        for (int i = start; i < nums.length; i++) {
            if (i > start && nums[i] == nums[i - 1]) { continue; } // skip duplicates
            temp.add(nums[i]);
            backtrack(ans, temp, nums, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
}
```

## [Permutation](https://leetcode.com/problems/permutations/)

Given a collection of **distinct** integers, return all possible permutations.

🖥 [Video Explanation](https://www.youtube.com/watch?v=6iOXVmtjO-M&t=2s)

```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

``` java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        backtrack(ans, new ArrayList<Integer>(), nums);
        return ans;
    }

    private void backtrack(List<List<Integer>> ans, List<Integer> temp, int[] nums) {
        if (temp.size() == nums.length) {
            ans.add(new ArrayList<Integer>(temp));
        } else {
            for (int i = 0; i < nums.length; i++) {
                if (temp.contains(nums[i])) { continue; } // skip duplicates
                temp.add(nums[i]);
                backtrack(ans, temp, nums);
                temp.remove(temp.size() - 1);
            }
        }
    }
}
```

## [Permutation II](https://leetcode.com/problems/permutations-ii/)

Given a collection of **some duplicate** integers, return all possible permutations.

🖥 [Video Explanation](https://www.youtube.com/watch?v=ziKo42Q3nQ8&t=8s)

```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

``` java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        Arrays.sort(nums); // easy to compare
        backtrack(ans, new ArrayList<Integer>(), nums, new boolean[nums.length]);
        return ans;
    }

    private void backtrack(List<List<Integer>> ans, List<Integer> temp, int[] nums, boolean[] used) {
        if (temp.size() == nums.length) {
            ans.add(new ArrayList<Integer>(temp));
        } else {
            for (int i = 0; i < nums.length; i++) {
                if (used[i] || (i > 0 && nums[i] == nums[i - 1] && !used[i - 1])) { continue; } // skip duplicates
                used[i] = true;
                temp.add(nums[i]);
                backtrack(ans, temp, nums, used);
                used[i] = false;
                temp.remove(temp.size() - 1);
            }
        }
    }
}
```

## [Combination Sum](https://leetcode.com/problems/combination-sum/)

Given a set of candidate numbers (candidates) **(without duplicates)** and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target. The **same** repeated number may be chosen from candidates **unlimited** number of times.

🖥 [Video Explanation](https://www.youtube.com/watch?v=WXEh-xk9j3k&t=14s)

```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

``` java
class Solution {
    public List<List<Integer>> combinationSum(int[] nums, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(ans, new ArrayList<>(), nums, target, 0);
        return ans;
    }

    private void backtrack(List<List<Integer>> ans, List<Integer> temp, int [] nums, int remain, int start){
        if (remain < 0) {
            return;
        } else if (remain == 0) {
            ans.add(new ArrayList<Integer>(temp));
        } else{
            for(int i = start; i < nums.length; i++){
                temp.add(nums[i]);
                backtrack(ans, temp, nums, remain - nums[i], i); // not i + 1 because we can reuse same elements
                temp.remove(temp.size() - 1);
            }
        }
    }
}
```

## [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a set of candidate numbers (candidates) **(with some duplicates)** and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target. Each number may be chosen from candidates **once**.

🖥 [Video Explanation](https://www.youtube.com/watch?v=tbjipJMXMPs&t=8s)

```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```

``` java
class Solution {
    public List<List<Integer>> combinationSum2(int[] nums, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums); // easy to compare
        backtrack(ans, new ArrayList<>(), nums, target, 0);
        return ans;
    }

    private void backtrack(List<List<Integer>> ans, List<Integer> temp, int [] nums, int remain, int start){
        if (remain < 0) {
            return;
        } else if (remain == 0) {
            ans.add(new ArrayList<Integer>(temp));
        } else{
            for(int i = start; i < nums.length; i++){
                if (i > start && nums[i] == nums[i - 1]) { continue; } // skip duplicates
                temp.add(nums[i]);
                backtrack(ans, temp, nums, remain - nums[i], i + 1);
                temp.remove(temp.size() - 1);
            }
        }
    }
}
```

## [Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)

Find all possible combinations of ***k*** numbers that add up to a number ***n***, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

🖥 [Video Explanation](https://www.youtube.com/watch?v=wE51ZRxZTMA&t=16s)

```
Input: k = 3, n = 9
Output: [[1,2,6], [1,3,5], [2,3,4]]
```

``` java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        backtrack(ans, new ArrayList<Integer>(), k, n, 1);
        return ans;
    }

    private void backtrack(List<List<Integer>> ans, List<Integer> temp, int k, int remain, int start) {
        if (temp.size() > k) {
            return;
        } else if (temp.size() == k && remain == 0) {
            ans.add(new ArrayList<Integer>(temp));
        } else{
            for (int i = start; i <= 9; i++) {
                temp.add(i);
                backtrack(ans, temp, k, remain - i, i + 1);
                temp.remove(temp.size() - 1);
            }
        }
    }
}
```

## [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

Given a string *s*, partition *s* such that every substring of the partition is a palindrome.

🖥 [Video Explanation](https://www.youtube.com/watch?v=FGrapMFgbCA)

```
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```

``` java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> ans = new ArrayList<List<String>>();
        backtrack(ans, new ArrayList<String>(), s, 0);
        return ans;
    }

    public void backtrack(List<List<String>> ans, List<String> temp, String s, int start){
        if (start == s.length()) {
            ans.add(new ArrayList<String>(temp));
        } else {
            for(int i = start; i < s.length(); i++){
                if (!isPalindrome(s, start, i)) { continue; } // skip invalid solution
                temp.add(s.substring(start, i + 1)); // beginIndex is inclusive, endIndex is exclusive
                backtrack(ans, temp, s, i + 1);
                temp.remove(temp.size() - 1);
            }
        }
    }

    public boolean isPalindrome(String s, int low, int high){
        while(low < high) {
            if (s.charAt(low) != s.charAt(high)) { return false; }
            low++;
            high--;
        }
        return true;
    }
}
```
# Courses Schedule

## [Course Schedule](https://leetcode.com/problems/course-schedule/)

There are a total of numCourses courses you have to take, labeled from 0 to numCourses. Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]. Given the total number of courses and a list of prerequisite pairs, **is it possible** for you to finish all courses?

🖥 [Video Explanation](https://www.youtube.com/watch?v=IfmEjwyNrBU)

```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
```

``` java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adjacency = new ArrayList<List<Integer>>();
        for (int i = 0; i < numCourses; i++) {
            adjacency.add(new ArrayList<Integer>());
        }

        // get the indegree and adjacency of every course
        int[] indegrees = new int[numCourses];
        for (int[] cp : prerequisites) {
            // to take course cp[0], you have to first take course cp[1]
            indegrees[cp[0]]++; // it need one more step from cp[1] to get to cp[0]
            adjacency.get(cp[1]).add(cp[0]); // adjaceny of cp[1] is cp[0]
        }

        // get all the courses with the indegree of 0
        Queue<Integer> queue = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] == 0) { queue.add(i); }
        }

        while (!queue.isEmpty()) {
            // has already take this course
            int pre = queue.poll();
            numCourses--;

            // iterate to next course
            for (int cur : adjacency.get(pre)) {
                indegrees[cur]--;

                // get all the courses with the indegree of 0.
                if (indegrees[cur] == 0) { queue.add(cur); }
            }
        }

        return numCourses == 0;
    }
}
```

## [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

There are a total of numCourses courses you have to take, labeled from 0 to numCourses. Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]. Given the total number of courses and a list of prerequisite pairs, return one of **correct orders**.

🖥 [Video Explanation](https://www.youtube.com/watch?v=79jkJGlvuGU)

```
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```

``` java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> adjacency = new ArrayList<List<Integer>>();
        for (int i = 0; i < numCourses; i++) {
            adjacency.add(new ArrayList<Integer>());
        }

        // get the indegree and adjacency of every course
        int[] indegrees = new int[numCourses];
        for (int[] cp : prerequisites) {
            // to take course cp[0], you have to first take course cp[1]
            indegrees[cp[0]]++; // it need one more step from cp[1] to get to cp[0]
            adjacency.get(cp[1]).add(cp[0]); // adjaceny of cp[1] is cp[0]
        }

        // get all the courses with the indegree of 0
        Queue<Integer> queue = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] == 0) { queue.add(i); }
        }

        List<Integer> ans = new ArrayList<Integer>();
        while (!queue.isEmpty()) {
            // has already take this course
            int pre = queue.poll();
            ans.add(pre);
            numCourses--;

            // iterate to next course
            for (int cur : adjacency.get(pre)) {
                indegrees[cur]--;

                // get all the courses with the indegree of 0.
                if (indegrees[cur] == 0) { queue.add(cur); }
            }
        }

        if (numCourses == 0) {
            return ans.stream().mapToInt(i->i).toArray();
        } else {
            return new int[0];
        }
    }
}
```

## [Course Schedule III](https://leetcode.com/problems/course-schedule-iii/)

Each courses represented by pairs (t,d), has duration t and closed on d. A course should be taken continuously for t days and must be finished before or on the d day. Find the **maxima**l number of courses that can be taken.

🖥 [Video Explanation]()

```
Input: [[100, 200], [200, 1300], [1000, 1250], [2000, 3200]]
Output: 3
Explanation:
There're totally 4 courses, but you can take 3 courses at most:
- First, take the 1st course, it costs 100 days so you will finish it on the 100th day, and ready to take the next course on the 101st day.
- Second, take the 3rd course, it costs 1000 days so you will finish it on the 1100th day, and ready to take the next course on the 1101st day.
- Third, take the 2nd course, it costs 200 days so you will finish it on the 1300th day.
The 4th course cannot be taken now, since you will finish it on the 3300th day, which exceeds the closed date.
```

``` java
public class Solution {
    public int scheduleCourse(int[][] courses) {
        // sorted based on end day
        Arrays.sort(courses, (a, b) -> a[1] - b[1]);

        // courses[x][0] -> duration of course
        // courses[x][1] -> end day of course

        int time = 0;
        int count = 0;
        for (int i = 0; i < courses.length; i++) {
            if (time + courses[i][0] <= courses[i][1]) {
                time += courses[i][0];
                count++;
            } else { // cannot take this course due to exceed the ending day

                // find the maximum duration time before current course
                int max_dur = i;
                for (int j = 0; j < i; j++) {
                    if (courses[j][0] > courses[max_dur][0]) { max_dur = j; }
                }

                // when the current does not have maximum duration time
                if (courses[max_dur][0] != courses[i][0]) {
                    // a saving can be achived, which can help to fit in more courses
                    time += courses[i][0] - courses[max_dur][0];
                }

                // indicate this course has not been taken and will not be taken in the future
                courses[max_dur][0] = -1;
            }
        }
        return count;
    }
}
```

## [Course Schedule IV](https://leetcode.com/problems/course-schedule-iv/)

There are total of n courses you have to take, some courses may have direct prerequisite, e.g. to take course 0 you have first to take course 1, whcih is expressed as a pair: [1, 0]. You should answer for each `queries[i]` whether the course `queries[i][0]` is a prerequisite of the course `queries[i][1]` or not.

🖥 [Video Explanation](https://www.youtube.com/watch?v=mjgqp9laZnk)

```
Input: n = 5, prerequisites = [[0,1],[1,2],[2,3],[3,4]], queries = [[0,4],[4,0],[1,3],[3,0]]
Output: [true,false,true,false]
```

``` java
class Solution {
      public List<Boolean> checkIfPrerequisite(int n, int[][] prerequisites, int[][] queries) {
        //      key      higher level
        HashMap<Integer, HashSet<Integer>> map = new HashMap<Integer, HashSet<Integer>>();
        for (int[] val : prerequisites) {
            HashSet<Integer> set; // higher level course for val[0]
            if (map.containsKey(val[0])) {
                set = map.get(val[0]);
            } else {
                set = new HashSet<Integer>();
            }
            set.add(val[1]);
            map.put(val[0], set);
        }

        // loop through all the possible path
        HashSet<String> path = new HashSet<String>();
        for (int i = 0; i < n; i++) {
            bfs(map, i, n, path);
        }

        // check qeries with possible path
        List<Boolean> ans = new ArrayList<Boolean>();
        for (int[] val : queries) {
            ans.add(path.contains(val[0] + "_" + val[1]));
        }
        return ans;
    }

    private void bfs(HashMap<Integer, HashSet<Integer>> map, int i, int n, HashSet<String> path) {
        if (!map.containsKey(i)) { return; }

        LinkedList<Integer> queue = new LinkedList<Integer>();
        boolean[] visited = new boolean[n]; // initialized to be false

        queue.add(i);
        visited[i] = true;

        while (!queue.isEmpty()) {
            HashSet<Integer> higher_level = map.get(queue.poll());
            if (higher_level != null) {

                // loop through all the course of higher level
                for (Integer d : higher_level) {

                    // if have not learn this course
                    if (!visited[d]) {
                        // i -> lower level, d -> higher level
                        path.add(i + "_" + d);
                        queue.add(d);
                        visited[d] = true;
                    }
                }
            }
        }
    }
}
```

# Stocking Problems

## [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

An array for which the ith element is the price of a given stock on day i. Find the maximum profit if only premitted to complete at most one transaction.

🖥 [Video Explanation](https://www.youtube.com/watch?v=VsogmToIwJc)

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5. Not 7-1 = 6, as selling price needs to be larger than buying price.
```

``` java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for (int i = 0; i < prices.length; i++) {
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            } else if (prices[i] - minPrice > maxProfit) {
                maxProfit = prices[i] - minPrice;
            }
        }
        return maxProfit;
    }
}
```

## [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

An array for which the ith element is the price of a given stock on day i. Find the maximum profit if premitted to complete many transactions.

🖥 [Video Explanation](https://www.youtube.com/watch?v=k4qkgFyO00o)

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4. Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

``` java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;

        for (int i = 1; i < prices.length; i++) {
            // ensure only sell stock after own a stock
            maxProfit += Math.max(0, prices[i] - prices[i - 1]);
        }

        return maxProfit;
    }
}
```

## [Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

An array for which the ith element is the price of a given stock on day i. Find the maximum profit if only premitted to complete at most two transactions.

🖥 [Video Explanation](https://www.youtube.com/watch?v=sk1Sz0IG-XE)

```
Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3. Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```

``` java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0) { return 0; }

        // initialize
        int[][] dp = new int[prices.length + 1][5 + 1];
        for (int i = 1; i <= 5; i++) {
            dp[0][i] = Integer.MIN_VALUE;
        }

        dp[0][1] = 0;
        for (int i = 1; i <= prices.length; i++) {
            // phase1,3,5 -> does not own stock
            for (int j = 1; j <= 5; j += 2) {
                // does not won stock all the day, same phase on different day -> maxProfit until yesterday
                dp[i][j] = dp[i - 1][j];

                if (j > 1 && i > 1 && dp[i - 1][j - 1] != Integer.MIN_VALUE) { // phase3,5
                    // maxProfit between 1.dont have stock yesterday    2.have stock yesterday
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - 1] + prices[i - 1] - prices[i - 2]);
                }
            }

            // phase2,4 -> does own stock
            for (int j = 2; j <= 5; j += 2) {
                // just buy a stock today, different phase on different day -> maxProfit until yesterday
                dp[i][j] = dp[i - 1][j - 1];

                if (j > 1 && i > 1 && dp[i - 1][j] != Integer.MIN_VALUE) {
                    // maxProfit between 1.dont have stock yesterday    2.have stock yesterday
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j] + prices[i - 1] - prices[i - 2]);
                }
            }
        }

        // find the maxProfit among different phase
        int ans = 0;
        for (int j = 1; j <= 5; j++) {
            ans = Math.max(ans, dp[prices.length][j]);
        }
        return ans;
    }
}
```

## [Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

An array for which the ith element is the price of a given stock on day i. Find the maximum profit if only premitted to complete at most k transactions.

🖥 [Video Explanation](https://www.youtube.com/watch?v=KWoXZkD-XVU)

```
Input: [2,4,1], k = 2
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
```

``` java
class Solution {
    public int maxProfit(int k, int[] prices) {
        if (prices.length == 0) { return 0; }

        if (k > prices.length / 2) { return greaterK(prices); }

        // initialize
        int phaseLen = 2 * k + 1;
        int[][] dp = new int[prices.length + 1][phaseLen + 1];
        for (int i = 1; i <= phaseLen; i++) {
            dp[0][i] = Integer.MIN_VALUE;
        }

        dp[0][1] = 0;
        for (int i = 1; i <= prices.length; i++) {
            // phase1,3,5,..,2k+1 -> does not own stock
            for (int j = 1; j <= phaseLen; j += 2) {
                // does not won stock all the day, same phase on different day -> maxProfit until yesterday
                dp[i][j] = dp[i - 1][j];

                if (j > 1 && i > 1 && dp[i - 1][j - 1] != Integer.MIN_VALUE) {
                    // maxProfit between 1.dont have stock the day before yesterday    2.have stock the day before yesterday
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - 1] + prices[i - 1] - prices[i - 2]);
                }
            }

            // phase2,4,...,2k -> does own stock
            for (int j = 2; j <= phaseLen; j += 2) {
                // just buy a stock today, different phase on different day -> maxProfit until yesterday
                dp[i][j] = dp[i - 1][j - 1];

                if (j > 1 && i > 1 && dp[i - 1][j] != Integer.MIN_VALUE) {
                    // maxProfit between 1.dont have stock the day before yesterday    2.have stock the day before yesterday
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j] + prices[i - 1] - prices[i - 2]);
                }
            }
        }

        // find the maxProfit among different phase
        int ans = 0;
        for (int j = 1; j <= phaseLen; j++) {
            ans = Math.max(ans, dp[prices.length][j]);
        }
        return ans;
    }

    private int greaterK(int[] prices) {
        int maxProfit = 0;

        for (int i = 1; i < prices.length; i++) {
            // ensure only sell stock after own a stock
            maxProfit += Math.max(0, prices[i] - prices[i - 1]);
        }

        return maxProfit;
    }
}
```

## [Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

An array for which the ith element is the price of a given stock on day i. Find the maximum profit if premitted to complete many transactions with cooldown(after you sell your stock, you cannot buy stock on next day).

🖥 [Video Explanation](https://www.youtube.com/watch?v=tKcNxI-4Gpk)

```
Input: [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```

``` java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) { return 0; }

        int[] sell = new int[prices.length]; //sell[i] -> sell at day i
        int[] cooldown = new int[prices.length]; //cooldown[i] -> day i is cooldown day
        sell[1] = prices[1] - prices[0];

        for (int i = 2; i < prices.length; i++) {
            // 前一天卖🆚不卖，哪个更赚钱
            cooldown[i] = Math.max(sell[i - 1], cooldown[i - 1]);

            // 当天卖出股票的利润➕之前的利润       // hold stock yesterday    // sell the stock that has bought yesterday
            sell[i] = prices[i] - prices[i - 1] + Math.max(sell[i - 1], cooldown[i - 2]);
        }

        return Math.max(sell[prices.length - 1], cooldown[prices.length - 1]);
    }
}
```

## [Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

An array for which the ith element is the price of a given stock on day i. Find the maximum profit if premitted to complete many transactions with transaction fee.

🖥 [Video Explanation](https://www.youtube.com/watch?v=mzRUlY-XZ6k)

```
nput: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
- Buying at prices[0] = 1
- Selling at prices[3] = 8
- Buying at prices[4] = 4
- Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

``` java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int sold = 0;
        int hold = -prices[0];

        for (int i = 1; i < prices.length; i++) {
                        // 昨天   // 今天sell or buy
            sold = Math.max(sold, hold + prices[i] - fee); // sell stock
            hold = Math.max(hold, sold - prices[i]); // buy stock
        }

        return sold;
    }
}
```

