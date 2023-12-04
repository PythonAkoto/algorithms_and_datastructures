# 739. Daily Temperatures
## Compnay: Meta

Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` *is the number of days you have to wait after the* `ith` `day to get a warmer temperature.` If there is no future day for which this is possible, keep `answer[i] == 0` instead.

Example 1:

Input: `temperatures = [73,74,75,71,69,72,76,73]`
Output: `[1,1,4,2,1,1,0,0]`

Example 2:

Input: `temperatures = [30,40,50,60]`
Output: `[1,1,1,0]`

Example 3:

Input: `temperatures = [30,60,90]`
Output: `[1,1,0]`

# Python
```
from typing import List

class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        # Initialize a list to store the result with default values of 0
        res = [0] * len(temperatures)

        # Initialize a stack to keep track of temperatures and their indices
        stack = []  # Stack elements: [temperature, index]

        # Iterate through each temperature and its index
        for i, t in enumerate(temperatures):
            # Check if the current temperature is greater than the temperature at the top of the stack
            while stack and t > stack[-1][0]:
                # If it is greater, pop the stack and update the result for the popped index
                stackTemp, stackInd = stack.pop()
                res[stackInd] = i - stackInd

            # Push the current temperature and its index onto the stack
            stack.append((t, i))

        # Return the list of results representing the number of days until warmer temperatures
        return res
```

# JavaScript
```
// Function to calculate the number of days until warmer temperatures for each day
var dailyTemperatures = function(temperatures, hottest = 0) {
    // Initialize an array to store the result with default values of 0
    const days = new Array(temperatures.length).fill(0);

    // Iterate through each day in reverse order
    for (let day = (temperatures.length - 1); (0 <= day); day--) {
        // Get the temperature for the current day
        const temperature = temperatures[day];

        // Check if the current temperature is hotter than or equal to the hottest temperature
        const isHotter = hottest <= temperature;
        if (isHotter) {
            hottest = temperature;
            continue; // Move to the next iteration if the current temperature is hotter or equal
        }

        // If the current temperature is not hotter, perform a search for the next warmer day
        search(temperatures, day, temperature, days);
    }

    // Return the array representing the number of days until warmer temperatures for each day
    return days;
}

// Function to search for the next warmer day
const search = (temperatures, day, temperature, days, dayCount = 1) => {
    // Helper function to check if the temperature on the next day is hotter than the current temperature
    const isHotter = () => temperatures[day + dayCount] <= temperature;

    // Continue searching until a warmer day is found
    while (isHotter()) {
        // Increment the day count by the number of days until warmer temperatures from the next day
        dayCount += days[day + dayCount];
    }

    // Update the result array with the number of days until warmer temperatures for the current day
    days[day] = dayCount;
}

```