# 76. Minimum Window Substring
## Company: Airbnb

Given two strings s and t of lengths m and n respectively, return the minimum window 
substring
 of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

Example 1:

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
Example 2:

Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
Example 3:

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.

# Python 
```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        # Check if t is an empty string
        if t == "":
            return ""

        # Initialize dictionaries to store the count of characters in the current window and the target string t
        countT, window = {}, {}

        # Count the occurrences of characters in t
        for c in t:
            countT[c] = 1 + countT.get(c, 0)

        # Initialize variables for the number of characters we have in the current window and the number of characters we need
        have, need = 0, len(countT)

        # Initialize variables to store the result substring and its length
        res, resLen = [-1, -1], float("infinity")

        # Initialize left pointer
        l = 0

        # Iterate through the string s with the right pointer
        for r in range(len(s)):
            c = s[r]
            window[c] = 1 + window.get(c, 0)

            # Check if a character in the current window reaches the required count
            if c in countT and window[c] == countT[c]:
                have += 1

            # While we have all the required characters in the current window
            while have == need:
                # Update the result if the current window is shorter than the previous result
                if (r - l + 1) < resLen:
                    res = [l, r]
                    resLen = r - l + 1

                # Pop the leftmost character from the window
                window[s[l]] -= 1

                # Check if the removal affects the count of a character in t
                if s[l] in countT and window[s[l]] < countT[s[l]]:
                    have -= 1

                # Move the left pointer to expand the window
                l += 1

        # Extract the result substring from the indices in res
        l, r = res
        return s[l : r + 1] if resLen != float("infinity") else ""
```

# JavaScript
```
/**
 * Function to find the minimum window substring of s that contains all characters of t
 * @param {string} s - The input string
 * @param {string} t - The target string
 * @returns {string} - The minimum window substring, or an empty string if not found
 */
var minWindow = function (s, t) {
    // Check if either s or t is an empty string
    const isMissingArgs = !s.length || !t.length;
    if (isMissingArgs) return '';

    // Initialize the frequency map for characters in t
    const frequencyMap = getFrequencyMap(t);

    // Get the window pointers for the minimum window substring
    const { start, end } = getWindowPointers(s, t, frequencyMap);

    // Get the minimum window substring using the indices from the window pointers
    return getSubString(s, start, end);
};

/**
 * Function to create a frequency map for characters in a string
 * @param {string} str - The input string
 * @param {Map} frequencyMap - The frequency map to update
 * @returns {Map} - The updated frequency map
 */
const getFrequencyMap = (str, frequencyMap = new Map()) => {
    for (const char of str) {
        frequencyMap.set(char, (frequencyMap.get(char) || 0) + 1);
    }

    return frequencyMap;
};

/**
 * Function to find the window pointers for the minimum window substring
 * @param {string} s - The input string
 * @param {string} t - The target string
 * @param {Map} frequencyMap - The frequency map for characters in t
 * @returns {Object} - An object containing the start and end indices of the minimum window substring
 */
const getWindowPointers = (s, t, frequencyMap) => {
    let [left, right, matched, start, end] = [0, 0, 0, 0, s.length + 1];

    // Iterate through the string s with the right pointer
    while (right < s.length) {
        // Update the matched count and frequency map for the right character
        matched = addRightFrequency(s, right, frequencyMap, matched);

        // Check if the window can slide
        const canSlide = () => matched === t.length;
        while (canSlide()) {
            const window = right - left + 1;

            // Update the start and end indices if the current window is smaller than the previous minimum
            const isSmaller = window < end;
            if (isSmaller) {
                [start, end] = [left, window];
            }

            // Update the matched count and frequency map for the left character
            matched = subtractLeftFrequency(s, left, frequencyMap, matched);
            left++;
        }

        // Move the right pointer to expand the window
        right++;
    }

    return { start, end };
};

/**
 * Function to add the frequency of the right character in the window
 * @param {string} s - The input string
 * @param {number} right - The index of the right character in the window
 * @param {Map} frequencyMap - The frequency map for characters in t
 * @param {number} matched - The current count of matched characters
 * @returns {number} - The updated count of matched characters
 */
const addRightFrequency = (s, right, frequencyMap, matched) => {
    const char = s[right];

    // Check if the character is in t
    if (frequencyMap.has(char)) {
        // Update the frequency map and check if the character is within the window
        frequencyMap.set(char, frequencyMap.get(char) - 1);
        const isInWindow = 0 <= frequencyMap.get(char);
        if (isInWindow) matched++;
    }

    return matched;
};

/**
 * Function to subtract the frequency of the left character from the window
 * @param {string} s - The input string
 * @param {number} left - The index of the left character in the window
 * @param {Map} frequencyMap - The frequency map for characters in t
 * @param {number} matched - The current count of matched characters
 * @returns {number} - The updated count of matched characters
 */
const subtractLeftFrequency = (s, left, frequencyMap, matched) => {
    const char = s[left];

    // Check if the character is in t
    if (frequencyMap.has(char)) {
        // Check if the character is leaving the window and update the frequency map
        const isOutOfWindow = frequencyMap.get(char) === 0;
        if (isOutOfWindow) matched--;

        frequencyMap.set(char, frequencyMap.get(char) + 1);
    }

    return matched;
};

/**
 * Function to extract the substring from s using start and end indices
 * @param {string} s - The input string
 * @param {number} start - The start index of the substring
 * @param {number} end - The end index of the substring
 * @returns {string} - The extracted substring
 */
const getSubString = (s, start, end) =>
    end <= s.length ? s.slice(start, start + end) : '';
```