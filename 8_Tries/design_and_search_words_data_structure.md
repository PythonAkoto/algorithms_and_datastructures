# 211. Design and Search Words Data Structure
### Company: Google

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

WordDictionary() Initializes the object.
void addWord(word) Adds word to the data structure, it can be matched later.
bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.
 

Example:

Input
```
["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
[[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
```
Output
```
[null,null,null,null,false,true,true,true]
```

Explanation
```
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // return False
wordDictionary.search("bad"); // return True
wordDictionary.search(".ad"); // return True
```

# Python 
```
class TrieNode:
    def __init__(self):
        self.children = {}  # Dictionary to store child nodes (characters to TrieNode mapping)
        self.word = False  # Indicates if this node represents a complete word


class WordDictionary:
    def __init__(self):
        self.root = TrieNode()  # Create a TrieNode to serve as the root of the trie

    def addWord(self, word: str) -> None:
        """
        Add a word to the trie.
        """
        cur = self.root  # Start traversal from the root

        # Traverse through each character in the word
        for c in word:
            if c not in cur.children:  # If the character isn't in the children of the current node
                cur.children[c] = TrieNode()  # Create a new TrieNode for this character
            cur = cur.children[c]  # Move to the next TrieNode

        # Mark the last node as a complete word
        cur.word = True

    def search(self, word: str) -> bool:
        """
        Search for a word in the trie. '.' can match any character.
        """
        def dfs(j, root):
            cur = root  # Start traversal from the given root

            # Traverse through each character starting from position j
            for i in range(j, len(word)):
                c = word[i]  # Current character in the word

                if c == ".":
                    # If the character is '.', it can match any character.
                    # Recur for each child of the current node.
                    for child in cur.children.values():
                        if dfs(i + 1, child):
                            return True
                    return False
                else:
                    # If the character is a specific letter, move to the corresponding child.
                    # If the character is not present, the word does not exist in the trie.
                    if c not in cur.children:
                        return False
                    cur = cur.children[c]  # Move to the next TrieNode

            return cur.word  # Return whether the last node represents a complete word

        # Start the depth-first search from the beginning (position 0) and the root of the trie
        return dfs(0, self.root)

        


# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```

# JavaScript
```
class TrieNode {
    constructor() {
        this.children = {};
        this.isWord = false;
    }
}

class WordDictionary {
    constructor() {
        this.root = new TrieNode();
    }

    // create new word
    addWord(word, node = this.root) {
        for (const char of word) {
            const child = node.children[char] || new TrieNode();

            node.children[char] = child;

            node = child;
        }

        node.isWord = true;
    }

    // search for a word
    search(word) {
        return this.dfs(word, this.root, 0);
    }
    // depth of search function

    dfs(word, node, level) {
        if (!node) return false;

        const isWord = level === word.length;
        if (isWord) return node.isWord;

        const isWildCard = word[level] === '.';
        if (isWildCard) return this.hasWildCard(word, node, level);

        return this.dfs(word, node.children[word[level]], level + 1);
    }
    
    // wildcard func
    hasWildCard(word, node, level) {
        for (const char of Object.keys(node.children)) {
            const child = node.children[char];

            const hasWord = this.dfs(word, child, level + 1);
            if (hasWord) return true;
        }

        return false;
    }
}
```