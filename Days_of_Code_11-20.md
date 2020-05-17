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

 
 
 
 
