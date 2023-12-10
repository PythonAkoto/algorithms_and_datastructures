# 567. Permutation To String 
## Company: Microsoft

Given two strings `s1` and `s2`, return `true` if `s2` *contains a permutation* of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

 

Example 1:

Input: `s1 = "ab", s2 = "eidbaooo"`
Output: `true`
Explanation: `s2` contains one permutation of `s1` ("ba").

Example 2:

Input: `s1 = "ab", s2 = "eidboaoo"`
Output: `false`

# Python
```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        # Check if the length of s1 is greater than the length of s2, in which case s1 cannot be a permutation of s2
        if len(s1) > len(s2):
            return False

        # Initialize count arrays for each character in the alphabet (26 characters)
        s1Count, s2Count = [0] * 26, [0] * 26

        # Count the occurrences of characters in the first window of length s1 in both strings
        for i in range(len(s1)):
            s1Count[ord(s1[i]) - ord("a")] += 1
            s2Count[ord(s2[i]) - ord("a")] += 1

        # Initialize a variable to track the number of matches between the count arrays
        matches = 0

        # Check for matches in the initial window
        for i in range(26):
            matches += 1 if s1Count[i] == s2Count[i] else 0

        # Sliding window approach to check for permutation in the rest of the string
        l = 0
        for r in range(len(s1), len(s2)):
            # If all characters have the same count, return True
            if matches == 26:
                return True

            # Update the count array for the new character at the right end of the window
            index = ord(s2[r]) - ord("a")
            s2Count[index] += 1

            # Update the matches count based on the change in counts
            if s1Count[index] == s2Count[index]:
                matches += 1
            elif s1Count[index] + 1 == s2Count[index]:
                matches -= 1

            # Update the count array for the character that goes out of the window from the left end
            index = ord(s2[l]) - ord("a")
            s2Count[index] -= 1

            # Update the matches count based on the change in counts
            if s1Count[index] == s2Count[index]:
                matches += 1
            elif s1Count[index] - 1 == s2Count[index]:
                matches -= 1

            # Move the left pointer to slide the window
            l += 1

        # Check for matches in the last window
        return matches == 26
```

# JavaScript
```
/**
 * Function to check if s1 is a permutation of s2
 * @param {string} s1 - The first string
 * @param {string} s2 - The second string
 * @returns {boolean} - True if s1 is a permutation of s2, otherwise false
 */
function checkInclusion(s1, s2) {
    // Check if the length of s1 is greater than the length of s2, in which case s1 cannot be a permutation of s2
    if (s1.length > s2.length) {
        return false;
    }

    // Initialize an object to store the count of characters in s1
    const s1Chars = Object.create(null);

    // Count the occurrences of characters in s1
    for (const ch of s1) {
        if (!(ch in s1Chars)) {
            s1Chars[ch] = 0;
        }
        ++s1Chars[ch];
    }

    // Calculate the last index to start checking for permutations in s2
    const last = s2.length - s1.length;
    let i = 0;

    // Iterate through possible windows in s2
    while (i <= last) {
        // Move the pointer to the next character in s2 that is in s1
        while (i <= last && !(s2[i] in s1Chars)) {
            ++i;
        }

        // If there are no more characters in s1, return false
        if (i > last) {
            return false;
        }

        // Initialize an object to store the count of characters in the current window of s2
        const subChars = Object.create(null);
        let j = i;

        // Count the occurrences of characters in the current window of s2 that are also in s1
        while (j < s2.length && s2[j] in s1Chars) {
            const ch = s2[j];

            if (!(ch in subChars)) {
                subChars[ch] = 0;
            }
            ++subChars[ch];

            // Break if the count of a character in the current window exceeds its count in s1
            if (subChars[ch] > s1Chars[ch]) {
                break;
            }

            ++j;
        }

        // Check if the length of the current window is equal to the length of s1
        if (s1.length === j - i) {
            return true;
        }

        // Move the pointer to the next character in s2 that is different from the current character
        if (j < s2.length && s2[j] in s1Chars) {
            while (s2[i] !== s2[j]) {
                ++i;
            }
            ++i;
        } else {
            i = j;
        }
    }

    return false;
}
```