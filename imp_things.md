## 1. Sort on the basis of multiple attributes 

https://stackoverflow.com/questions/4233476/sort-a-list-by-multiple-attributes?noredirect=1&lq=1

## 2. BFS using Queue

https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/

## 3. You always forget how to write function inside a function in python. Here is the syntax :

        def kthSmallest(self, root, k):
            ans=[]
            def inorder(root,ans):
                if root:
                    inorder(root.left,ans)
                    ans.append(root.val)
                    inorder(root.right,ans)
            inorder(root,ans)
            return ans[k-1]
