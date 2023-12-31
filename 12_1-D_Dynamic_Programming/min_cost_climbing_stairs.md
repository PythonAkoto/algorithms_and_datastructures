# 746. Min Cost Climbing Stairs
## Company: Google

You are given an integer array `cost` where `cost[i]` is the cost of `ith` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

*Return the minimum cost to reach the top of the floor.*

 

Example 1:

Input: `cost = [10,15,20]`
Output: `15`

Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.

Example 2:

Input: `cost = [1,100,1,1,1,100,1,1,100,1]`
Output: `6`
Explanation: You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.

# Python
```
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        # Traverse the 'cost' list in reverse order, starting from the second-to-last element (len(cost) - 3).
        for i in range(len(cost) - 3, -1, -1):
            # Update the cost of reaching the current step by adding the minimum cost of reaching the next two steps.
            cost[i] += min(cost[i + 1], cost[i + 2])

        # After the loop, the 'cost' list will have the accumulated minimum cost for each step.
        # The minimum cost to reach the top of the stairs will be the minimum between the first and second step.
        return min(cost[0], cost[1])
```
# JavaScript
```
 var minCostClimbingStairs = (cost) => {
    const tabu = new Array(cost.length + 1).fill(0);

    for (let i = 2; i < tabu.length; i++) {
        const [ prev, prevPrev ] = [ (i - 1), (i - 2) ];
        const downOne = tabu[prev] + cost[prev];
        const downTwo = tabu[prevPrev] + cost[prevPrev];

        tabu[i] = Math.min(downOne, downTwo);
    }

    return tabu[tabu.length - 1];
}
```