Given an m x n grid of characters board and a string word, return true if word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.


```
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if (board.empty() || board[0].empty()) return false;
        vector<vector<bool>> visited(board.size(), vector<bool>(board[0].size(), false));
        
        for (int i = 0; i < board.size(); ++i) {
            for (int j = 0; j < board[0].size(); ++j) {
                if (backtrack(board, word, i, j, 0, visited)) {
                    return true;
                }
            }
        }
        return false;
    }
    
private:
    bool backtrack(vector<vector<char>>& board, const string& word, int i, int j, int k, vector<vector<bool>>& visited) {
        if (k == word.length()) return true;
        if (i < 0 || i >= board.size() || j < 0 || j >= board[0].size() || visited[i][j] || board[i][j] != word[k]) {
            return false;
        }

        visited[i][j] = true;
        bool found = backtrack(board, word, i + 1, j, k + 1, visited) ||
                     backtrack(board, word, i - 1, j, k + 1, visited) ||
                     backtrack(board, word, i, j + 1, k + 1, visited) ||
                     backtrack(board, word, i, j - 1, k + 1, visited);

        visited[i][j] = false;
        return found;
    }
};

```
