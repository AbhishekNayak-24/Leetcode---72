# Leetcode---72
Edit Distance
//code in java
public class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        
        // Create a 2D array to store the minimum edit distance.
        int[][] dp = new int[m + 1][n + 1];
        
        // Initialize the first row and first column.
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int j = 0; j <= n; j++) {
            dp[0][j] = j;
        }
        
        // Fill the dp array.
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j - 1],  // Replace
                                             Math.min(dp[i - 1][j],    // Delete
                                                      dp[i][j - 1]));  // Insert
                }
            }
        }
        
        return dp[m][n];
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        String word1 = "horse";
        String word2 = "ros";
        int result = solution.minDistance(word1, word2);
        System.out.println("The minimum edit distance is: " + result);
    }
}
