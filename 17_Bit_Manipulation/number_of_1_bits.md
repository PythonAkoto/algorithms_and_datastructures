# 191. Number of 1 Bits
## Company: 

Write a function that takes the binary representation of an unsigned integer and returns the number of `'1'` bits it has (also known as the [Hamming weight](https://en.wikipedia.org/wiki/Hamming_weight)).

**Note:**

- Note that in some languages, such as Java, there is no unsigned integer type. In this case, the input will be given as a signed integer type. It should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
- In Java, the compiler represents the signed integers using [2's complement notation](). Therefore, in **Example 3**, the input represents the signed integer. `-3`.
 

Example 1:

Input: `n = 00000000000000000000000000001011`
Output: `3`
Explanation: The input binary string `00000000000000000000000000001011` has a total of three `'1'` bits.

Example 2:

Input: `n = 00000000000000000000000010000000`
Output: `1`
Explanation: The input binary string `00000000000000000000000010000000` has a total of one `'1'` bit.
Example 3:

Input: `n = 11111111111111111111111111111101`
Output: `31`
Explanation: The input binary string `11111111111111111111111111111101` has a total of thirty one `'1'` bits.
 

**Constraints:**

- The input must be a **binary string** of length `32`.

# Python
```
class Solution:
    def hammingWeight(self, n: int) -> int:
        # Initialize a variable to count the number of set bits (1s)
        res = 0

        # Iterate until 'n' becomes 0
        while n:
            # Use bitwise AND (&) with (n - 1) to unset the rightmost set bit
            # This operation effectively removes one '1' from the binary representation of 'n'
            n &= n - 1

            # Increment the count of set bits
            res += 1

        # Return the total count of set bits
        return res
```

# JavaScript
```
// Function to count the number of set bits (1s) in the binary representation of an integer
var hammingWeight = function(n) {
    // Initialize variables for counting set bits and creating a bitmask
    let [ bits, mask ] = [ 0, 1 ];
    
    // Iterate through each bit of the integer (32 bits for a 32-bit integer)
    for (let i = 0; i < 32; i++) {
        // Check if the current bit is set (equal to 1)
        const hasBit = ((n & mask) !== 0);
        
        // If the current bit is set, increment the count of set bits
        if (hasBit) bits++;
        
        // Move the bitmask to the next bit position using left shift
        mask <<= 1;
    }
    
    // Return the total count of set bits in the binary representation of the integer
    return bits;
}
```