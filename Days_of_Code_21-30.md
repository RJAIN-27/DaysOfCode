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

### 23 - 450. Delete Node in a BST - https://leetcode.com/problems/delete-node-in-a-bst/
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
            
#### 25 - https://leetcode.com/problems/interval-list-intersections/

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
            
        
