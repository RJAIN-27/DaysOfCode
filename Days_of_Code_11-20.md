# DaysOfCode

#### 11 - 102. Binary Tree Level Order Traversal - https://leetcode.com/problems/binary-tree-level-order-traversal/

 This question is just like doing a BFS on a graph and now since this is a tree there wont be any cycles, so we do not need a 
 visited array to ensure if cycles are made or not.
 
 Another good thing in the question was how they have managed to make levels for each level of the tree. 
 
    def levelOrder(self, root):
         if not root:
             return []

         queue=[]
         queue.append(root)
         level=[]
         l=0
         while queue:
             lq=len(queue)
             level.append([])
             for i in range(lq):
                 node=queue.pop(0)
                 level[l].append(node.val)
                 if node.left!=None:
                     queue.append(node.left)
                 if node.right!=None:
                     queue.append(node.right)
             l=l+1
         return level
         
#### 12 - 103. Binary Tree Zigzag Level Order Traversal - https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

This problem is just a slight variation to the above level order traversal problem. We just need to check if the level is even or odd and append appropriately.

     def zigzagLevelOrder(self, root):
         if not root:
             return []

         queue=[]
         queue.append(root)
         level=[]
         l=0
         while queue:
             lq=len(queue)
             level.append([])
             for i in range(lq):
                 node=queue.pop(0)
                 if l%2==0:
                     level[l].append(node.val)
                 else:
                     level[l].insert(0,node.val)
                 if node.left!=None:
                     queue.append(node.left)
                 if node.right!=None:
                     queue.append(node.right)
             l=l+1
         return level
         
#### 13 - 987. Vertical Order Traversal of a Binary Tree - https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/
      
        def verticalTraversal(self, root):
          d=defaultdict(list)
          if not root:
              return []

          queue=[]
          X=0
          Y=0
          queue.append((root,X,Y))
          level=[]
          while queue:
              lq=len(queue)
              for i in range(lq):
                  node,X,l=queue.pop(0)
                  level.append((node.val,X,Y))
                  if node.left!=None:
                      queue.append((node.left,X-1,Y))
                  if node.right!=None:
                      queue.append((node.right,X+1,Y))
              Y=Y+1

          for i in level:
              d[i[1]].append((i[0],i[2]))

          sd = sorted(d.items())
          ans=[]
          for i in range(len(sd)):
              ans.append((sd[i][1]))

          fans=[]
          l=0
          for i in ans:
              fans.append([])
              a=sorted(i, key=lambda element: (element[1], element[0]))
              for x in a:
                  fans[l].append(x[0])
              l=l+1
          return fans

 #### 14 - 567. Permutation in String - https://leetcode.com/problems/permutation-in-string/
 
 This is a very simple problem just like the anagram problem (10-438) that you had done.
 
    def checkInclusion(self, s1, s2):
           a=[0]*26
           b=[0]*26

           l1=len(s1)
           l2=len(s2)

           for i in s1:
               a[ord(i)-ord('a')]=a[ord(i)-ord('a')]+1

           for i in range(l2):
               b[ord(s2[i])-ord('a')]=b[ord(s2[i])-ord('a')]+1
               if i >= l1:
                   b[ord(s2[i-l1])-ord('a')]=b[ord(s2[i-l1])-ord('a')]-1
               if b==a:
                   return True
           return False
           
 
  #### 15 - 207. Course Schedule - https://leetcode.com/problems/course-schedule/
  
  This one of the best implementations of DFS problem that I have found.
  
  While doing this problem I realised that if I just have to do DFS, I will need only one array visited that can take care and help us not visit the node if its already visited.
  
  This is very simple and can be seen in the Geeks for Geeks link - https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/
  
  But while I want to detect if there is a cycle, I need a visited array that has 3 values, one that shows visited, not visited and visiting.
  
However, for detecting a cycle I checked the solution from leetcode, after making my code wrong several times.

https://leetcode.com/problems/course-schedule/discuss/58606/Python-Solution-with-Detailed-Explanation

Below is my code:

     def detect(self,i, s, d):
        s[i]=1
        for j in d[i]:
            if s[j] == 1:
                return True
            elif s[j] == 0: 
                if self.detect(j, s, d):
                    return True
        s[i]=2
        return False
        
    def detect_cycle(self,d, numCourses):
        s=[0]*numCourses
        for i in range(numCourses):
            if s[i]==0:
                if self.detect(i, s, d):
                    return True
        return False
    
    def canFinish(self, numCourses, prerequisites):
        d=defaultdict(list)
        
        for i in prerequisites:
            nc=i[0]
            pc=i[1]
            d[pc].append(nc)
        
        if self.detect_cycle(d, numCourses) ==True:
            return False
        return True
            
 #### 16 - 210. Course Schedule II - https://leetcode.com/problems/course-schedule-ii/
 
 This code I have improvised, the above code to make it better and return the topological sort.

       def detect(self,i, s, d, ans):
        s[i]=1
        for j in d[i]:
            if s[j] == 1:   
                return True
            elif s[j] == 0: 
                if  self.detect(j, s, d, ans) == True:  
                    return True
        s[i]=2
        ans.append(i)
        return ans 
        
    def detect_cycle(self,d, numCourses, ans):
        s=[0]*numCourses
        for i in range(numCourses):
            if s[i]==0:
                x=self.detect(i, s, d, ans)
                if x==True:
                    return True
        return x
    
    def findOrder(self, numCourses, prerequisites):
        d=defaultdict(list)
        for i in prerequisites:
            nc=i[0]
            pc=i[1]
            d[pc].append(nc)
            
        ans=[]
        ans=self.detect_cycle(d, numCourses, ans)
        if ans == True:
            return []
        else:
            return ans[::-1]

 #### 17 - 901. Online Stock Span - https://leetcode.com/problems/online-stock-span/
 
 This stack question is tricky and small stack question.
 
    def __init__(self):
        self.stack=[]        

    def next(self, price):

        if not self.stack:
            self.stack.append((price,1))
        else:
            a=0
            while self.stack and self.stack[-1][0]<=price:
                x,y=self.stack.pop()
                a=a+y
            self.stack.append((price,a+1))
        return self.stack[-1][1]

#### 18 - 739. Daily Temperatures - https://leetcode.com/problems/daily-temperatures/

I never got a chance to understand the stack implementation of this question properly. Was always baffeled. But the video link: https://www.youtube.com/watch?v=WGm4Kj3lhRI worked wonders.

        def dailyTemperatures(self, T):
            results=[0]*(len(T))
            stack=[]
            for i in xrange(len(T)-1, -1, -1):
                while stack and T[i] >= stack[-1][0]:
                    stack.pop()
                if stack and stack[-1][0]>T[i]:
                    results[i]=(stack[-1][1]-i)
                stack.append((T[i],i))
            return results

#### 19 - 139. Word Break - https://leetcode.com/problems/word-break/

This is a dynamic programming question which is pretty simple to understand. 

It becomes difficult to come up with the solution at the moment.

The solution is:

       def wordBreak(self, s, wordDict):
           l=[]
           for i in wordDict:
               l.append(len(i))

           ans=[False]*(len(s)+1)

           ans[0]=True

           for i in range(1,len(s)+1):
               for j in l:
                   if ans[i-j] and s[i-j:i] in wordDict:
                       ans[i]=True
                       break
           print ans
           return ans[-1]
           
We consider a final answer array in the above solution its name is arr.

The size of this array is len(s)+1 where s is the string that is being inputted.

Below is how it will be filled up in 1 different scenarios:

 >> https://github.com/RJAIN-27/DaysOfCode/blob/master/IMG_7858.JPG

#### 20 - 230. Kth Smallest Element in a BST - https://leetcode.com/problems/kth-smallest-element-in-a-bst/

This question i realised that the  inorder traversal that is left root right is ascendiing order for a BST.

    def kthSmallest(self, root, k):
        ans=[]
        def inorder(root,ans):
            if root:
                inorder(root.left,ans)
                ans.append(root.val)
                inorder(root.right,ans)
        inorder(root,ans)
        return ans[k-1]
