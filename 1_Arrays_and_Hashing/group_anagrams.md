# 49. Group Anagrams
## Company: Amazon

Given an array of strings `strs`, group **the anagrams** together. You can return the answer **in any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

Example 1:

Input: `strs = ["eat","tea","tan","ate","nat","bat"]`
Output: `[["bat"],["nat","tan"],["ate","eat","tea"]]`

Example 2:

Input: `strs = [""]`
Output: `[[""]]`

Example 3:

Input: `strs = ["a"]`
Output: `[["a"]]`

# Python
```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # Initialize a defaultdict to store anagrams grouped by their character counts
        ans = collections.defaultdict(list)

        # Iterate through each string in the input list
        for s in strs:
            # Initialize a list to count the occurrences of each character in the string
            count = [0] * 26

            # Count the occurrences of each character in the string
            for c in s:
                count[ord(c) - ord("a")] += 1

            # Convert the count list to a tuple to use it as a key in the defaultdict
            ans[tuple(count)].append(s)

        # Return the grouped anagrams as a list of lists
        return ans.values()
```

# JavaScript
```
// Function to group anagrams in an array of words
var groupAnagrams = (words, map = new Map()) => {
    // Check if the input array is empty
    if (!words.length) return [];

    // Group the words into anagrams using a helper function
    groupWords(words, map); /* Time O(N * K) | Space O(N * K) */

    // Return the grouped anagrams as an array of arrays
    return [ ...map.values() ]; /* Time O(N) | Space O(N * K) */
}

// Helper function to group words into anagrams using a map
var groupWords = (words, map) => {
    // Iterate through each original word in the array
    for (const original of words) { /* Time O(N) */
        // Get a hash for the original word based on character frequency
        const hash = getHash(original); /* Time O(K) | Space O(1) */
        
        // Retrieve the values (anagrams) corresponding to the hash from the map
        const values = map.get(hash) || [];

        // Add the original word to the list of anagrams
        values.push(original); /* Space O(N) */

        // Update the map with the hash and the updated list of anagrams
        map.set(hash, values); /* Space O(N * K) */
    }
}

// Function to calculate a hash for a word based on character frequency
const getHash = (word) => {
    // Initialize an array to store the frequency of each character in the word
    const frequency = new Array(26).fill(0);

    // Iterate through each character in the word
    for (const char of word) { /* Time O(K) */
        // Get the character code and update the frequency array
        const charCode = getCode(char); /* Time O(1) | Space O(1) */
        frequency[charCode]++; /* Space O(1) */
    }

    // Build a hash from the frequency array
    return buildHash(frequency);
}

// Function to get the character code (0 to 25) for a lowercase letter
const getCode = (char) => char.charCodeAt(0) - 'a'.charCodeAt(0);

// Function to build a hash from a frequency array
const buildHash = (frequency) => frequency.toString();
```