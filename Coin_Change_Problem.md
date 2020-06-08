## 518. Coin Change 2

Link : https://leetcode.com/problems/coin-change-2/solution/

I have done this problem in 3 ways.

First I did it using recursion. There was time limit exceeded.

Then I did this problem using a 2d matrix. - DP

Then I did this problem using 1d array. - DP

#### Recursive solution :

https://www.geeksforgeeks.org/coin-change-dp-7/

#### DP using a 2d table:
    def change(self, amount, coins):
            if amount == 0:
                return 1
            if len(coins)==0:
                return 0
            table = [[0 for i in range(amount+1)] for j in range(len(coins))]

            for i in range(len(coins)):
                table[i][0]=1

            for i in range(len(coins)):
                for j in range(1,amount+1):
                    if j >= coins[i]:
                        table[i][j]=table[i-1][j]+table[i][j-coins[i]]
                    else:
                        table[i][j]=table[i-1][j]
            return table[-1][-1]
 #### DP using 1d table:
    def change(self, amount, coins):
        dp = [0] * (amount + 1)
        dp[0] = 1
        
        for coin in coins:
            for x in range(coin, amount + 1):
                dp[x] += dp[x - coin]
        return dp[amount]
