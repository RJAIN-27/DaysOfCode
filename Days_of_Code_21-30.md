# DaysOfCode

## I felt like doing some Tree questions to have a grasp.

#### 31 - 700. Search in a Binary Search Tree - https://leetcode.com/problems/search-in-a-binary-search-tree/
    
      def searchBST(self, root, val):
        def search(root,val):
            if root:
                if root.val==val or root is None:
                    return root
                elif root.val > val:
                    return search(root.left, val)
                elif root.val < val:
                    return search(root.right, val)
        return search(root,val)  
