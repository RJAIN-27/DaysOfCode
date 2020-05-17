# DaysOfCode

#### 1-53. Maximum Subarray - https://leetcode.com/problems/maximum-subarray/

        def maxSubArray(self, nums):
                n=len(nums)
                local_sum=nums[0]
                global_sum=nums[0]

                for i in range(1,n):
                    local_sum=nums[i]+max(local_sum,0)
                    global_sum=max(global_sum,local_sum)
                return global_sum 

#### 2-918. Maximum Sum Circular Subarray - https://leetcode.com/problems/maximum-sum-circular-subarray/

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

#### 3-328. Odd Even Linked List - https://leetcode.com/problems/odd-even-linked-list/
        
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
                
 #### 4-62. Unique Paths - https://leetcode.com/problems/unique-paths/
 
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
      
 #### 5-127. Word Ladder - https://leetcode.com/problems/word-ladder/
 
This problem is a typical implementation of Breadth First Search and I really liked the fact how it cannot be done using the Depth First Search Algorithm. We are using the breadth first search because we want to find out the minimum number of transformations to change the begin word in to the end word. In case we just needed to check if the word can be transformed using any number of transformations, we could have done it using the Depth First Search Algorithm.
 
        def ladderLength(self, beginWord, endWord, wordList):
                if endWord not in wordList:
                    return 0
                L=len(beginWord)
                neighbor_dict=defaultdict(list)

                for word in wordList:
                    for i in range(L):
                        neighbor_dict[word[:i] + "*" + word[i+1:]].append(word)

                queue=[]
                visited={beginWord: True}
                queue.append((beginWord, 1))

                while queue:           
                    current_word, level = queue.pop(0) 
                    for i in range(L):
                        intermediate_word = current_word[:i] + "*" + current_word[i+1:]
                        for word1 in neighbor_dict[intermediate_word]:     
                            if word1 == endWord:
                                return level + 1
                            if word1 not in visited:
                                visited[word1] = True
                                queue.append((word1, level + 1))
                return 0
   
 #### 6-Remove K Digits - https://leetcode.com/problems/remove-k-digits/
 
 This is a really cool implementation of the Greedy approach. 
 
 Let us say the number is - [1,2,3,4,5,2,6,4]
 K=4
 
 The below image exactly explains what is to be done:

 ![](https://github.com/RJAIN-27/DaysOfCode/blob/master/402_algorithm.png)
 
        def removeKdigits(self, num, k):
                s=[]
                fs=[]
                for i in num:
                    while k>0 and s and s[-1]>i:
                        s.pop()
                        k=k-1
                    s.append(i)

                if k > 0:
                    fs=s[:-k]
                else:
                    fs=s

                if  ("".join(fs).lstrip("0"))=="":
                    return "0"
                else:
                    return ("".join(fs).lstrip("0"))
            
#### 7-11. Container With Most Water - https://leetcode.com/problems/container-with-most-water/

The main part of intution for the question lies in the fact that when l=0 and r=len(height)-1 we can say that area can be maximum due to the largest width, but now the area can be increased further by considering bigger walls.

        def maxArea(self, height):
                max_area=0
                area=0
                l=0
                r=len(height)-1
                while l < r:
                    area=(r-l)*min(height[r],height[l])
                    max_area=max(area,max_area)

                    if height[l]<=height[r]:
                        l=l+1
                    else:
                        r=r-1
                return max_area
