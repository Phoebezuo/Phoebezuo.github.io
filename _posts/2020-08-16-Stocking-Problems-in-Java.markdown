---
layout:     post
title:      Stocking Problems in Java
date:       2020-08-16
summary:    Summaries a few questions in Leetcode about Best Time to Buy and Sell Stock
categories: Algorithm Leetcode
---

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
