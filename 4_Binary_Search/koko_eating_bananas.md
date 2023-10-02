# 875. Koko Eating Bananas
### Company: Google

Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

*Return the minimum integer `k` such that she can eat all the bananas within `h` hours.*

 

Example 1:

Input: `piles = [3,6,7,11], h = 8`
Output: `4`

Example 2:

Input: `piles = [30,11,23,4,20], h = 5`
Output: `30`

Example 3:

Input: `piles = [30,11,23,4,20], h = 6`
Output: `23`

# Python
```
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        # set left & right pointers
        l, r = 1, max(piles)

        # initialise result to max number in list
        res = r

        while l <= r:
            # get the value of k (middle value in list)
            k = (l + r) // 2

            totalTime = 0
            # loop through each item in list
            for p in piles:
                # divide list item by k
                totalTime += math.ceil(float(p) / k)

            # update result if hours less or equal to input
            if totalTime <= h:
                res = k
                # update right pointer to find left portion of list
                r = k - 1
            else:
                # update left pointer to find right side of list
                l = k + 1
        
        # return the result
        return res
```

# JavaScript
```
/**
 * @param {number[]} piles
 * @param {number} h
 * @return {number}
 */
var minEatingSpeed = function(piles, h) {
    // set left & right pointers
    let left = 1, right = Math.max(...piles);
    // set result to highest number (this is only temporary)
    let result = right;
    
    while (left <= right) {
        // get the value of k 
        const k = Math.floor((left + right) / 2);
        let totalTime = 0;
        
        // loop through each item in list
        for (const pile of piles) {
            // update total time by dividing pile by k
            // use Math.ceil() to round up to nearest number
            totalTime += Math.ceil(pile / k);
        }
        
        // binary search
        
        // update the result if totalTime is less or equal to hours
        if (totalTime <= h) {
            result = k;
            // update right pointer to search the left side of list
            right = k - 1;
        } else {
            // update left pointer to search the right side of list
            left = k + 1;
        }
        
    }
    // return the result after the loop has finished
    return result;
    
};

const piles = [30,11,23,4,20], hours = 5;
console.log(minEatingSpeed(piles, hours));
console.log('Yaw Akoto');
```