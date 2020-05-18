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

 
 
 
 
