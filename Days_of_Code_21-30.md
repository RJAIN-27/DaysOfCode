# DaysOfCode

#### 21 - 700. Search in a Binary Search Tree - https://leetcode.com/problems/search-in-a-binary-search-tree/
    
       def searchBST(self, root, val):
            if root:
                if root.val==val or root is None:
                    return root
                elif root.val > val:
                    return self.searchBST(root.left, val)
                elif root.val < val:
                    return self.searchBST(root.right, val) 

#### 22 - 701. Insert into a Binary Search Tree - https://leetcode.com/problems/insert-into-a-binary-search-tree/

        def insertIntoBST(self, root, val):
            if root is None:
                return TreeNode(val)
            if root.val < val:
                root.right = self.insertIntoBST(root.right, val)
            else:
                root.left = self.insertIntoBST(root.left, val) 
            return root

#### 23 - 450. Delete Node in a BST - https://leetcode.com/problems/delete-node-in-a-bst/
    def successor(self, root):
        root = root.right
        while root.left:
            root = root.left
        return root.val
    
    def predecessor(self, root):
        root = root.left
        while root.right:
            root = root.right
        return root.val
    
    def deleteNode(self, root, key):
        if root == None:
            return root
        if key > root.val:
            root.right = self.deleteNode(root.right, key)
        elif key < root.val:
            root.left = self.deleteNode(root.left, key)
        else:
            if not (root.left or root.right):
                root = None
            elif root.right:
                root.val = self.successor(root)
                root.right = self.deleteNode(root.right, root.val)  
            else:
                root.val = self.predecessor(root)
                root.left = self.deleteNode(root.left, root.val)        
        return root

#### 24 - 1277. Count Square Submatrices with All Ones - https://leetcode.com/problems/count-square-submatrices-with-all-ones/

    def countSquares(self, matrix):
            
            rows=len(matrix)
            columns=len(matrix[0])
            
            result=0
            
            helper = [[0 for i in range(columns)] for j in range(rows)]
            
            for i in range(rows):
                if matrix[i][0] == 1:
                    helper[i][0] = matrix[i][0]

            i=0
            for i in range(columns):
                if matrix[0][i] == 1:
                    helper[0][i] = matrix[0][i]

                            
            for i in range(1, rows):
                for j in range(1, columns):
                    if matrix[i][j]==1:
                        helper[i][j]=1+min(helper[i-1][j-1], helper[i-1][j], helper[i][j-1])

            
            for i in range(rows):
                result=result+sum(helper[i])
                
            return result
            
#### 25 - 986. Interval List Intersections - https://leetcode.com/problems/interval-list-intersections/

        def intervalIntersection(self, A, B):
        
            la=len(A)
            lb=len(B)

            i=0
            j=0

            s=0
            e=0

            ans=[]

            while i < la and j < lb:

                oa,ta=A[i]
                ob,tb=B[j]

                if tb<oa:
                    j=j+1
                    continue

                if ta<ob:
                    i=i+1
                    continue

                if oa>=ob:
                    s=oa
                else:
                    s=ob

                if ta<=tb:
                    e=ta
                    i=i+1
                else:
                    e=tb
                    j=j+1

                ans.append([s,e])

            return ans
            
        
#### 26 - 1008. Construct Binary Search Tree from Preorder Traversal - https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/

    def leftright(self, preorder, root):
            l=[]
            r=[]
            if not preorder:
                return 
            for i in range(1,len(preorder)):
                if preorder[i]>=root.val:
                    r.append(preorder[i])
                else:
                    l.append(preorder[i])
            if l:
                root.left=TreeNode(l[0])
            else:
                root.left=None
            if r:
                root.right=TreeNode(r[0])
            else:
                root.right=None

            if l!=None:
                self.leftright(l, root.left)
            if r!=None:
                self.leftright( r, root.right)
            return 

        def bstFromPreorder(self, preorder):
            root=TreeNode(preorder[0])
            self.leftright(preorder, root)
            return root

#### 27 - 322. Coin Change - https://leetcode.com/problems/coin-change/
        
        def coinChange(self, coins, amount):
            dp=[float('inf')]*(amount+1)
            dp[0]=0
            for i in range(1,(amount+1)):
                for j in coins:
                    if i >= j:
                        dp[i]=min(dp[i],dp[i-j]+1) 
            if dp[-1]!=float('inf'):
                return dp[-1]
            else:
                return -1

## 28 - Intvert the Binary Tree - https://leetcode.com/problems/invert-binary-tree/
        def invertTree(self, root):
            if root==None:
                return root
            temp=root.left
            root.left=root.right
            root.right=temp
            self.invertTree(root.left)
            self.invertTree(root.right)
            return root
            

#### 29 - Delete Node in a Linked List - https://leetcode.com/problems/delete-node-in-a-linked-list/
        def deleteNode(self, node):
            node.val=node.next.val
            node.next=node.next.next
        

#### 30 - https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

        def flatten(self, root): 
        r=root
        def flattenT(root):
            if root==None:
                return root
            if root.left==None and root.right==None:
                return root
            left=flattenT(root.left)
            right=flattenT(root.right)
            if left:
                left.right=root.right
                root.right=root.left
                root.left=None
            if right:
                return right
            else:
                return left
        return flattenT(r)
