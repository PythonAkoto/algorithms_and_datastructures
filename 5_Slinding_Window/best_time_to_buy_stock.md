# 121. Best Time to Buy and Sell Stock
### Company: Google

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return the *maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

 

Example 1:

Input: `prices = [7,1,5,3,6,4]`
Output: `5`
*Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.*
*Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.*

Example 2:

Input: `prices = [7,6,4,3,1]`
Output: `0`
*Explanation: In this case, no transactions are done and the max profit = 0.*

# Python Solution 1
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # create pointers and max points variable
        l, r = 0, 1
        maxP = 0

        # loop through prices with right pointer
        while r < len(prices):

            # if left pointer price is lower than right pointer price
            if prices[l] < prices[r]:
                # find profit by subtracting left & right pointers
                profit = prices[r] - prices[l]
                # update max profit variable
                maxP = max(maxP, profit) 
            # update left pointer to right pointer, if left price higher
            # than right price
            else:
                l = r
            # shift the right pointer to the next day
            r += 1
        # return max profit
        return maxP
```

# Python Solution 2
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        
        lowest = prices[0]
        for price in prices:
            if price < lowest:
                lowest = price
            res = max(res, price - lowest)
        return res
```

# JavaScript Solution 1
```
var maxProfit = function(prices) {
    // store profit - start profit at 0
    let maxProfit = 0;
    // store lowest price - start @ 1st price in list
    let lowestPrice = prices[0];
    
    // loop through each price in list to see if lower
    // than price on the first day
    
    for (price of prices) {
        // if current price in list is lower than the lowest price
        if (price < lowestPrice) {
            // update lowest price
            lowestPrice = price;
        } else {
            // update the profit by subtracting the
            // current price from the updated lowest price
            maxProfit = Math.max(maxProfit, (price - lowestPrice));
        }
    }
    
    // return the maximum profit
    return maxProfit;
    
};
console.log('Solution 1:');
const prices = [7,1,5,3,6,4];
console.log(maxProfit(prices));
console.log('\nYaw Akoto');
```