# 853. Car Fleet
## Company: Google

There are n cars going to the same destination along a one-lane road. The destination is `target` miles away.

You are given two integer array `position` and `speed`, both of length n, where `position[i]` is the position of the ith car and `speed[i]` is the speed of the `ith` car (in miles per hour).

A car can never pass another car ahead of it, but it can catch up to it and drive bumper to bumper **at the same speed**. The faster car will **slow down** to match the slower car's speed. The distance between these two cars is ignored (i.e., they are assumed to have the same position).

A **car fleet** is some non-empty set of cars driving at the same position and same speed. Note that a single car is also a car fleet.

If a car catches up to a car fleet right at the destination point, it will still be considered as one car fleet.

Return the **number of car fleets** that will arrive at the destination.

 

Example 1:

Input: `target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]`
Output: `3`
Explanation:
```
The cars starting at 10 (speed 2) and 8 (speed 4) become a fleet, meeting each other at 12.
The car starting at 0 does not catch up to any other car, so it is a fleet by itself.
The cars starting at 5 (speed 1) and 3 (speed 3) become a fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches target.
Note that no other cars meet these fleets before the destination, so the answer is 3.
```

Example 2:

Input: `target = 10, position = [3], speed = [3]`
Output: `1`
Explanation: There is only one car, hence there is only one fleet.

Example 3:

Input: `target = 100, position = [0,2,4], speed = [4,2,1]`
Output: `1`
Explanation:
```
The cars starting at 0 (speed 4) and 2 (speed 2) become a fleet, meeting each other at 4. The fleet moves at speed 2.
Then, the fleet (speed 2) and the car starting at 4 (speed 1) become one fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches target.
```

# Python
```
from typing import List

class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        # Create pairs of position and speed and sort them in reverse order based on position
        pair = [(p, s) for p, s in zip(position, speed)]
        pair.sort(reverse=True)

        # Initialize a stack to keep track of time to reach the target for each car
        stack = []

        # Iterate through the sorted pairs in reverse order
        for p, s in pair:
            # Calculate the time to reach the target for the current car
            stack.append((target - p) / s)

            # Check if there are at least two cars in the stack and the current car is slower than the previous car
            if len(stack) >= 2 and stack[-1] <= stack[-2]:
                stack.pop()  # Remove the previous car from the stack as it is fleet with the current car

        # The length of the stack represents the number of car fleets
        return len(stack)
```

# JavaScript
```
// Function to calculate the number of car fleets
var carFleet = function(target, position, speed) {
    // Get the coordinates representing time to reach the target for each car
    const coordinates = getCoordinates(target, position, speed);

    // Search for car fleets in descending order of time to reach the target
    return searchDescending(coordinates);
};

// Function to get coordinates representing time to reach the target for each car
var getCoordinates = (target, position, speed) => position
    .map((_position, index) => [ _position, speed[index] ])        // Create pairs of position and speed
    .sort(([ aPosition ], [ bPosition ]) => bPosition - aPosition) // Sort the pairs in descending order based on position
    .map(([ _position, _speed ]) => (target - _position) / _speed); // Calculate time to reach the target for each car

// Function to search for car fleets in descending order of time to reach the target
var searchDescending = (coordinates, previous = 0, fleets = 0) => {
    // Iterate through the coordinates in descending order
    for (const coordinate of coordinates) {
        // Check if the current coordinate is greater than the previous one
        const isPreviousLess = previous < coordinate;
        if (!isPreviousLess) continue; // Skip to the next iteration if the previous coordinate is greater or equal

        // Update the previous coordinate and increment the fleet count
        previous = coordinate;
        fleets++;
    }

    // Return the total number of car fleets
    return fleets;
}
```