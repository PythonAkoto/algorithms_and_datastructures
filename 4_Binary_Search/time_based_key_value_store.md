# 981. Time Based Key Value Store
## Company: Google

Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

Implement the TimeMap class:

- `TimeMap()` Initializes the object of the data structure.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the `value` value at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.
 

Example 1:

Input
`["TimeMap", "set", "get", "get", "set", "get", "get"]
[[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]`
Output
`[null, null, "bar", "bar", null, "bar2", "bar2"]`

Explanation
```
TimeMap timeMap = new TimeMap();
timeMap.set("foo", "bar", 1);  // store the key "foo" and value "bar" along with timestamp = 1.
timeMap.get("foo", 1);         // return "bar"
timeMap.get("foo", 3);         // return "bar", since there is no value corresponding to foo at timestamp 3 and timestamp 2, then the only value is at timestamp 1 is "bar".
timeMap.set("foo", "bar2", 4); // store the key "foo" and value "bar2" along with timestamp = 4.
timeMap.get("foo", 4);         // return "bar2"
timeMap.get("foo", 5);         // return "bar2"
```

# Python
```
class TimeMap:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        # Dictionary to store the mapping of keys to lists of [value, timestamp] pairs
        self.keyStore = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        # If the key is not already in the keyStore, initialize it with an empty list
        if key not in self.keyStore:
            self.keyStore[key] = []
        # Append the [value, timestamp] pair to the list associated with the key
        self.keyStore[key].append([value, timestamp])

    def get(self, key: str, timestamp: int) -> str:
        # Initialize result variable to store the final value to be returned
        res = ""
        # Get the list of [value, timestamp] pairs associated with the key, or an empty list if the key is not present
        values = self.keyStore.get(key, [])
        
        # Initialize pointers for binary search
        l, r = 0, len(values) - 1
        
        # Perform binary search on the list of [value, timestamp] pairs
        while l <= r:
            m = (l + r) // 2
            # If the timestamp at the middle index is less than or equal to the target timestamp,
            # update the result and move the left pointer to search for larger timestamps
            if values[m][1] <= timestamp:
                res = values[m][0]
                l = m + 1
            # If the timestamp at the middle index is greater than the target timestamp,
            # move the right pointer to search for smaller timestamps
            else:
                r = m - 1
        
        # Return the final result (the value associated with the latest timestamp not greater than the target timestamp)
        return res
```

# JavaScript
```
class TimeMap {
    constructor() {
        // Initialize an empty map to store key-value pairs with timestamps
        this.map = {};
    }

    /**
     * Set a key-value pair with the given timestamp
     * @param {string} key
     * @param {string} value
     * @param {number} timestamp
     * Time complexity: O(1)
     * Space complexity: O(1)
     * @return {void}
     */
    set(key, value, timestamp) {
        // Get the bucket associated with the key or initialize an empty array if it doesn't exist
        const bucket = this.map[key] || [];

        // Update the map with the bucket
        this.map[key] = bucket;

        // Push the [value, timestamp] pair into the bucket
        bucket.push([value, timestamp]);
    }

    /**
     * Get the value associated with the given key at the specified timestamp
     * @param {string} key
     * @param {number} timestamp
     * Time complexity: O(log(N)) where N is the size of the bucket
     * Space complexity: O(1)
     * @return {string}
     */
    get(key, timestamp, value = '', bucket = this.map[key] || []) {
        // Initialize pointers for binary search
        let [left, right] = [0, bucket.length - 1];

        // Perform binary search on the bucket
        while (left <= right) {
            const mid = (left + right) >> 1;
            const [guessValue, guessTimestamp] = bucket[mid];

            // Check if the timestamp at the middle index is less than or equal to the target timestamp
            const isTargetGreater = guessTimestamp <= timestamp;
            if (isTargetGreater) {
                // Update the value and move the left pointer to search for larger timestamps
                value = guessValue;
                left = mid + 1;
            }

            // Check if the timestamp at the middle index is greater than the target timestamp
            const isTargetLess = timestamp < guessTimestamp;
            if (isTargetLess) right = mid - 1;
        }

        // Return the final value (the value associated with the latest timestamp not greater than the target timestamp)
        return value;
    }
}
```