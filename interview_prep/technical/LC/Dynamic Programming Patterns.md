

# Knapsack 0/1

> **Overview**: You have `n` items. Each item can be chosen **once or not chosen at all**. Each item has a “cost/weight” and usually some “value/profit.” You want the best value without exceeding a capacity.

### Classic problem statement

You are given:

```
weights = [2, 3, 4, 5]
values  = [3, 4, 5, 6]
capacity = 5
```

Each item has:

```
item 0: weight 2, value 3
item 1: weight 3, value 4
item 2: weight 4, value 5
item 3: weight 5, value 6
```

Goal: **Maximize total value while total weight <= capacity.**

For a bottom up approach, the way you should think of this is solving every sub problem between 0... n items, and 0...w weight/target. This is where the  **O(number_of_items * capacity)** complexity comes from.

A index like `dp[i][w]` will show the result given we considering all items from 0 .. i, and a max target/weight of w

### Example: [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)(LC 416)

Given an integer array `nums`, return `true` _if you can partition the array into two subsets such that the sum of the elements in both subsets is equal or_ `false` _otherwise_.

**Steps:**

##### 1) Compute the target, which will be the total sum of nums, divided by 2. 

`target = total // 2`
return false if total sum is odd, as you can't divide into two equal subsets

##### 2) Create a DP table (use 2D for this example, can be compressed to 1D because we only rely on previous sub problem)

Example: 
```cpp
vector<int> nums = {1,5,11,5};
vector<vector<false>> dp(nums.size(), vector<int>(target, false));

// need to check all subproblems from 0..i amount of items, and 0...w of target
// thus the nums.size() X target size matrix

// can we get capacity w using items 0..i
```

![](../../../pasted_images/Pasted%20image%2020260513212456.png)

This is where the time complexity **O(number_of_items * capacity)** comes from

##### 3) For every single item,  check if that specific target is achievable by taking or not taking the item. 

The first item (1), can be taken or not taken, meaning we can reach targets 0 and 1.

![](../../../pasted_images/Pasted%20image%2020260513211038.png)

The second item (5), can be taken or not taken, meaning we can reach targets 0, 1, 5, 6.

![](../../../pasted_images/Pasted%20image%2020260513211527.png)
In code this will look like:
```cpp
//skip item i
dp[i][curTarget] = dp[i - 1][curTarget]

// take item i (ONLY POSSIBLE IF curTarget - num[i] >= 0)
dp[i][curTarget] = dp[i - 1][curTarget - num[i]]
```

Doing this for every item:
![](../../../pasted_images/Pasted%20image%2020260513212043.png)

##### 4. Check table Complete subrange

In this case we will check the result of `dp[4][11]` becasue we want to know if using all **four** items, if we can reach the **target 11**

Is this case the answer is **True**



# Subsequences

Subsequence is similar to knapsack 0/1, in the sense at each character, you usually have the decision to **skip it** or **use it**?

### DP states
##### Pattern A: Prefix DP

```
dp[i][j] = answer using s[:i] and target[:j]

Meaning:
first i characters of source
first j characters of target
```

This naturally builds from top-left to bottom-right (answer).

##### Pattern B: Suffix DP

```
dp[i][j] = answer using s[i:] and target[j:]

Meaning:
source from i onward
target from j onward
```

This naturally asks at s[i], do I skip it or use it for target[j]?  Builds from bottom-right to top-left (answer).

### Problem Statements:
##### Counting problem

Question asks:

```
How many ways?
```

Usually transition uses:

```
skip + use
```

Example:

```
dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1]
```

##### Optimization problem

Question asks:

```
Longest?
Shortest?
Minimum?
Maximum?
```

Usually transition uses:

```
max(...)
min(...)
dp[...][...] + 1
```

Example:

```
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
```
### Example: Counting subsequences

Note this can be condensed to 1d with a CUR and PREV dp array, but 2d is shown for better explanation.

 Count how many ways `target` appears as a subsequence of `s`.

example:
```
s = "babgbag"  
target = "bag"
```

We will use a prefix state, where `dp[n][t]`, where t is the amount number of ways to form target from 0...t, using characters 0...n from s.

Our base cases are `dp[n][0] = 1`, as you can always form an empty target.

##### Bottom-Up:

From bottom-left to top-right. We will add because we are counting.

If characters do not match:

```
if s[n - 1] != target[t - 1]
dp[n][t] = dp[n - 1][t]
```

If characters match:

```
s[n - 1] == target[t - 1]
dp[n][t] = dp[n - 1][t] + dp[n - 1][t - 1]
```

The intuition is that if the character don't match at that index, adding that character (increasing the range of `s` to 0...n) won't improve the amount of subsequences. 

However if they do match, we will still have the same amount of subsequences if we didn't take the character, but also subsequences of 0...(t-1) if the next character we add is matching. 

##### Visual:

How to read this table. An example like `dp[6][2]` means the string `"babgba"` contains 4 unique subsequences of the string `"ba"`
	
![430](../../../pasted_images/Pasted%20image%2020260524022348.png)
![431](../../../pasted_images/Pasted%20image%2020260524023001.png)