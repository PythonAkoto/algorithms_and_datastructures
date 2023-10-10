# 208. Implement Trie (Prefix Tree)
### Company: Microsoft

A trie (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- Trie() Initializes the trie object.
- void insert(String word) Inserts the string word into the trie.
- boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
- boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.
 

Example 1:

Input
`["Trie", "insert", "search", "search", "startsWith", "insert", "search"]`
`[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]`
Output
`[null, null, true, false, true, null, true]`

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True


# Python
```
class TrieNode:
    def __init__(self):
        self.children = [None] * 26
        self.end = False


class Trie:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        # start postion at root of tree
        curr = self.root

        for c in word:
            # get position of character
            i = ord(c) - ord("a")
            # if current letter is not in the hashmap
            if curr.children[i] == None:
                # add new node to the letter
                curr.children[i] = TrieNode()

            # if letter exists, update current posit
            curr = curr.children[i]
        curr.end = True

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        curr = self.root
        for c in word:
            i = ord(c) - ord("a")
            if curr.children[i] == None:
                return False
            curr = curr.children[i]
        return curr.end

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        curr = self.root
        for c in prefix:
            i = ord(c) - ord("a")
            if curr.children[i] == None:
                return False
            curr = curr.children[i]
        return True
```

# JavaScript
```
class TrieNode {
    constructor() {
        this.children = {};
        this.isWord = false;
    }
}

class Trie {
    // class constructor to crete a new node at root
    constructor() {
        this.root = new TrieNode();
    }

    /* Time O(N) | Space O(N) */
    insert(word, node = this.root) {
        for (const char of word) {
            // place every character in matching node or new node
            const child = node.children[char] || new TrieNode();

            // shift the node to next child
            node.children[char] = child;

            node = child;
        }
        // set to true when no more letters to add
        node.isWord = true;
    }

    /* Time O(N) | Space O(1) */
    search(word, node = this.root) {
        for (const char of word) {
            const child = node.children[char] || null;

            // if nothing found return false
            if (!child) return false;

            // go to next node
            node = child;
        }

        // evaluate if at end of word - return bool
        return node.isWord;
    }

    /* Time O(N) | Space O(1) */
    startsWith(prefix, node = this.root) {
        for (const char of prefix) {
            const child = node.children[char] || null;

            if (!child) return false;

            node = child;
        }

        return true;
    }
}
```