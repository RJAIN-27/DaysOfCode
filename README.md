# DaysOfCode

#### 53. Maximum Subarray - https://leetcode.com/problems/maximum-subarray/

        def maxSubArray(self, nums):
                n=len(nums)
                local_sum=nums[0]
                global_sum=nums[0]

                for i in range(1,n):
                    local_sum=nums[i]+max(local_sum,0)
                    global_sum=max(global_sum,local_sum)
                return global_sum 

#### 918. Maximum Sum Circular Subarray - https://leetcode.com/problems/maximum-sum-circular-subarray/

        def maxSubarraySumCircular(self, A):
                sub_max = A[0]    
                max_sum = A[0]
                sub_min = A[0]
                min_sum = A[0]
                total_sum = A[0]

                for num in A[1:]:
                    total_sum += num
                    sub_max = max(num, sub_max + num)
                    max_sum = max(max_sum, sub_max)

                    sub_min = min(num, sub_min + num)
                    min_sum = min(min_sum, sub_min)

                if total_sum - min_sum > max_sum and total_sum - min_sum!=0:
                    return total_sum - min_sum
                else:
                    return max_sum

#### 328. Odd Even Linked List - https://leetcode.com/problems/odd-even-linked-list/
        
        def oddEvenList(self, head):
                if  head == None:
                    return head
                odd=head
                even=head.next
                evenhead=even


                while (even!=None and even.next!=None):
                    odd.next=even.next
                    odd=odd.next
                    even.next=odd.next
                    even=even.next

                odd.next=evenhead
                return head
                
 #### 62. Unique Paths - https://leetcode.com/problems/unique-paths/
 
        def uniquePaths(self, m, n):
                d=[[0 for i in range(m)] for j in range(n)]
                
                for i in range(m):
                        d[0][i]=1
                for i in range(n):
                        d[i][0]=1
                        
                        
                for i in range(n):
                        for j in range(m):
                                d[i][j]=d[i-1][j]+d[i][j-1]
                
                return d[n-1][m-1]
                
      # In this problem n is the number of rows and m is the number of columns
      
 #### 127. Word Ladder - https://leetcode.com/problems/word-ladder/
 
        This problem is a typical implementation of Breadth First Search and I really liked the fact how it cannot be done using the Depth First Search Algorithm. We are using the breadth first search because we want to find out the minimum number of transformations to change the begin word in to the end word. In case we just needed to check if the word can be transformed using any number of transformations, we could have done it using the Depth First Search Algorithm.
 
 
 
 
