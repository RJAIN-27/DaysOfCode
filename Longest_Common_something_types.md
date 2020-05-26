#### Longest common subsequence problem DP:
    https://leetcode.com/problems/longest-common-subsequence/
    
    
      def longestCommonSubsequence(self, text1, text2):
        dp=[[0 for i in range(len(text1)+1)] for j in range(len(text2)+1)]
        for i in range(1,len(text2)+1):
            for j in range(1,len(text1)+1):
                if text2[i-1]==text1[j-1]:
                    dp[i][j]=1+dp[i-1][j-1]
                else:
                    dp[i][j]=max(dp[i-1][j],dp[i][j-1])
        return dp[len(text2)][len(text1)]


#### Another application of the Longest common subsequence problem - The UNCROSSED LINE PROBLEM 
    https://leetcode.com/problems/uncrossed-lines/
    
        def maxUncrossedLines(self, A, B):
        ans=[[0 for i in range(len(A)+1)] for j in range(len(B)+1)]
        for i in range(1, len(B)+1):
            for j in range(1, len(A)+1):
                if A[j-1]==B[i-1]:
                    ans[i][j]=1+ans[i-1][j-1]
                else:
                    ans[i][j]=max(ans[i-1][j],ans[i][j-1])
        return ans[len(B)][len(A)]
