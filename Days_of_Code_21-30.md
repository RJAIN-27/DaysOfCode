# DaysOfCode

## I felt like doing some Tree questions to have a grasp.

#### 31 - 700. Search in a Binary Search Tree - https://leetcode.com/problems/search-in-a-binary-search-tree/
    
       def searchBST(self, root, val):
            if root:
                if root.val==val or root is None:
                    return root
                elif root.val > val:
                    return self.searchBST(root.left, val)
                elif root.val < val:
                    return self.searchBST(root.right, val) 

#### 701. Insert into a Binary Search Tree - https://leetcode.com/problems/insert-into-a-binary-search-tree/

        def insertIntoBST(self, root, val):
            if root is None:
                return TreeNode(val)
            if root.val < val:
                root.right = self.insertIntoBST(root.right, val)
            else:
                root.left = self.insertIntoBST(root.left, val) 
            return root

### 450. Delete Node in a BST - https://leetcode.com/problems/delete-node-in-a-bst/

