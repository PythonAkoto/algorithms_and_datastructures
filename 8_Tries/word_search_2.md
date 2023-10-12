# 212. Word Search II
### Company: Meta

Given an` m x n board` of characters and a list of strings `words`, return *all words on the board*.

Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are *horizontally or vertically* neighboring. The same letter cell may not be used more than once in a word.

 
Example 1:

Input: `board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]`
Output: `["eat","oath"]`

Example 2:

Input: `board = [["a","b"],["c","d"]], words = ["abcb"]`
Output: `[]`

# Python
```
class TrieNode:
    def __init__(self):
        self.children = {}  # Dictionary to store child nodes (characters)
        self.isWord = False  # Flag to mark the end of a word
        self.refs = 0  # Count of references to this node

    def addWord(self, word):
        cur = self
        cur.refs += 1  # Increment the reference count for the current node
        for c in word:
            if c not in cur.children:
                cur.children[c] = TrieNode()  # Create a new node for the character if it doesn't exist
            cur = cur.children[c]  # Move to the next node in the trie
            cur.refs += 1  # Increment the reference count for the next node
        cur.isWord = True  # Mark the end of the word in the trie

    def removeWord(self, word):
        cur = self
        cur.refs -= 1  # Decrement the reference count for the current node
        for c in word:
            if c in cur.children:
                cur = cur.children[c]  # Move to the next node in the trie
                cur.refs -= 1  # Decrement the reference count for the next node

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        root = TrieNode()  # Create the root node of the trie
        for w in words:
            root.addWord(w)  # Add each word to the trie

        ROWS, COLS = len(board), len(board[0])
        res, visit = set(), set()  # Initialize sets to store results and visited cell positions

        def dfs(r, c, node, word):
            if (
                r not in range(ROWS)  # Check if the row index is within bounds
                or c not in range(COLS)  # Check if the column index is within bounds
                or board[r][c] not in node.children  # Check if the character in the board exists in the trie
                or node.children[board[r][c]].refs < 1  # Check if the next node has references left
                or (r, c) in visit  # Check if the cell has been visited before
            ):
                return

            visit.add((r, c))  # Mark the cell as visited
            node = node.children[board[r][c]]  # Move to the next node in the trie
            word += board[r][c]  # Add the character to the current word

            if node.isWord:
                node.isWord = False  # Mark the end of the word as not a word (to prevent duplicates)
                res.add(word)  # Add the word to the results set
                root.removeWord(word)  # Remove the word from the trie

            # Explore neighboring cells
            dfs(r + 1, c, node, word)
            dfs(r - 1, c, node, word)
            dfs(r, c + 1, node, word)
            dfs(r, c - 1, node, word)

            visit.remove((r, c))  # Unmark the cell as visited

        for r in range(ROWS):
            for c in range(COLS):
                dfs(r, c, root, "")  # Start depth-first search from each cell

        return list(res)  # Convert the results set to a list and return it
```

# JavaScript
```
/**
 * @param {character[][]} board
 * @param {string[]} words
 * Time O((ROWS * COLS) * (4 * (3 ^ (WORDS - 1)))) | Space O(N)
 * @return {string[]}
 */
var findWords = function (board, words) {
    return new Trie(words).searchBoard(board);
};

class TrieNode {
    constructor() {
        this.children = {};
        this.word = '';
    }
}

class Trie {
    constructor(words) {
        this.root = new TrieNode();
        words.forEach((word) => this.insert(word));
    }

    /* Time O(N) | Space O(N) */
    insert(word, node = this.root) {
        for (const char of word) {
            const child = node.children[char] || new TrieNode();

            node.children[char] = child;

            node = child;
        }

        node.word = word;
    }

    /* Time O((ROWS * COLS) * (4 * (3 ^ (WORDS - 1)))) | Space O(N) */
    searchBoard(board, node = this.root, words = []) {
        const [rows, cols] = [board.length, board[0].length];

        for (let row = 0; row < rows; row++) {
            for (let col = 0; col < cols; col++) {
                this.dfs(board, row, rows, col, cols, node, words);
            }
        }

        return words;
    }

    dfs(board, row, rows, col, cols, node, words) {
        const char = board[row][col];
        const child = node.children[char] || null;

        if (this.canSkip(char, child)) return;

        node = child;
        this.checkWord(node, words);
        this.backTrack(board, row, rows, col, cols, node, words);
    }

    canSkip(char, child) {
        const hasSeen = char === '#';
        const isMissingChild = !child;

        return hasSeen || isMissingChild;
    }

    checkWord(node, words) {
        if (!node.word.length) return;

        words.push(node.word);
        node.word = '';
    }

    backTrack(board, row, rows, col, cols, node, words) {
        const char = board[row][col];

        board[row][col] = '#';

        for (const [_row, _col] of this.getNeighbors(row, rows, col, cols)) {
            this.dfs(board, _row, rows, _col, cols, node, words);
        }

        board[row][col] = char;
    }

    getNeighbors(row, rows, col, cols) {
        return [
            [row - 1, col],
            [row + 1, col],
            [row, col - 1],
            [row, col + 1],
        ].filter(([_row, _col]) => !this.isOutOfBounds(_row, rows, _col, cols));
    }

    isOutOfBounds(row, rows, col, cols) {
        const isRowOut = row < 0 || rows <= row;
        const isColOut = col < 0 || cols <= col;

        return isRowOut || isColOut;
    }
}
```