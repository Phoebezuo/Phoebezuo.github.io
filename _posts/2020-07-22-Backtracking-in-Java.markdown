---
layout: post
title:  "Backtracking in Java"
date:   2020-07-22
summary: Summaries a few questions in Leetcode about Backtracking
categories: Algorithm Backtracking Leetcode
---

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
