# 309. Best Time to Buy And Sell Stock With Cooldown
## Company: Google

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restrictions:

- After you sell your stock, you cannot buy stock on the next day (i.e., cooldown one day).

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

 

Example 1:

Input: `prices = [1,2,3,0,2]`
Output: `3`
Explanation: transactions = [buy, sell, cooldown, buy, sell]

Example 2:

Input: `prices = [1]`
Output: `0`

# Python 
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # State: Buying or Selling?
        # If Buy -> i + 1
        # If Sell -> i + 2

        dp = {}  # Memoization dictionary to store results for subproblems

        def dfs(i, buying):
            # Check if we have reached the end of the prices array
            if i >= len(prices):
                return 0
            # Check if the result for the current state has already been computed
            if (i, buying) in dp:
                return dp[(i, buying)]

            # Recursive case
            cooldown = dfs(i + 1, buying)  # No transaction on the current day
            if buying:
                # If in the buying state, we can either continue to not buy or buy on the current day
                buy = dfs(i + 1, not buying) - prices[i]  # Buy on the current day
                dp[(i, buying)] = max(buy, cooldown)
            else:
                # If in the selling state, we can either continue to not sell or sell on the current day
                sell = dfs(i + 2, not buying) + prices[i]  # Sell on the current day
                dp[(i, buying)] = max(sell, cooldown)

            # Return the maximum profit for the current state
            return dp[(i, buying)]

        # Start the recursive function from the initial state (buying) and return the result
        return dfs(0, True)
```

# JavaScript
```
var maxProfit = (prices) => {
    let [ sold, held, reset ] = [ (-Infinity), (-Infinity), 0 ];

    [ sold, reset ] = search(prices, sold, held, reset);/* Time O(N) */

    return Math.max(sold, reset);
}

var search = (prices, sold, held, reset) => {
    for (const price of prices) {/* Time O(N) */
        const preSold = sold;

        sold = (held + price);
        held = Math.max(held, (reset - price));
        reset = Math.max(reset, preSold);
    }

    return [ sold, reset ];
}
```