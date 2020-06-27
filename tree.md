



## 二叉树

树的遍历

递归 非递归

BFS  DFS 

层序遍历

二叉树的路径

构造二叉树

#### 二叉树遍历

![image-20200627132834261](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200627132834261.png)

#### 前序遍历

###### 递归

```python
###
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        self.pre(root,res)
        return res
        
    def pre(self,root,res):
        if root == None:
            return []
        res.append(root.val)
        self.pre(root.left,res)
        self.pre(root.right,res)
```

###### 非递归

```python
###
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack =[]
        cur = root
        
        while stack or cur:
            while cur:
                stack.append(cur)
                res.append(cur.val)
                cur = cur.left
            top = stack.pop()
            cur= top.right
        return res
                
```



#### 中序遍历

先遍历左子树，再访问根节点，最后遍历右子树

##### 递归

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        travel = []
        self.inorder(root,travel)
        return travel
        
    def inorder(self,root,travel):
        if root == None:
            return None
        self.inorder(root.left,travel)
        travel.append(root.val)
        self.inorder(root.right,travel)
```

##### 非递归

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        res = []
        stack = []
        cur = root
        
        while stack or cur:
            while cur:
                stack.append(cur)
                cur = cur.left
            top = stack.pop()
            res.append(top.val)
            cur = top.right
        return res
```



#### 后序遍历

先遍历左子树，右子树，最后访问节点

##### 递归

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        travel = []
        self.postorder(root,travel)
        return travel
        
    def postorder(self,root,travel):
        if root == None:
            return None
        self.postorder(root.left,travel)
        
        self.postorder(root.right,travel)
        travel.append(root.val)
            
```

##### 非递归

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        travel = []
        self.postorder(root,travel)
        return travel
        
    def postorder(self,root,travel):
        if root == None:
            return None
        self.postorder(root.left,travel)
        
        self.postorder(root.right,travel)
        travel.append(root.val)
            
```





#### BFS

层序遍历

只需要输出最后遍历的结果，[3, 9, 20, 15, 7]

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        queue = []
        res = []
        
        queue.append(root)
        while queue:
            top = queue.pop(0)
            res.append(top.val)
            if top.left:
                queue.append(top.left)
            if top.right:
                queue.append(top.right)
        
        return res
```

需要按不同的层划分

![image-20200627154300849](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200627154300849.png)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if root == None:
            return []
        queue = []
        res = []
        
        queue.append(root)
        while queue:
            level = []
            for i in range(len(queue)): #循环当前队列中的个数，区别每一层
                top = queue.pop(0)
                level.append(top.val)
                if top.left:
                    queue.append(top.left)
                if top.right:
                    queue.append(top.right)
            if level:
                res.append(level)
        return res
```





#### 二叉树的深度

![image-20200626172453510](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200626172453510.png)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if root == None:
            return 0
        if root.left == None and root.right == None: #判断是否叶子节点
            return 1
        return max(self.maxDepth(root.left),self.maxDepth(root.right)) +1
```



#### 对称二叉树

![image-20200627155747668](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200627155747668.png)

两种思路：（1） 使用递归，判

（2） 判断每层的节点是否回文

##### 递归

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        return self.helper(root,root)
        
    
    def helper(self,root1,root2):
        if root1 == None and root2 == None:
            return True
        if root1 ==None or root2 == None:
            return False
        if root1.val != root2.val:
            return False
        return self.helper(root1.left,root2.right) and self.helper(root1.right,root2.left)
```

##### 判断每层是否回文

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        queue = []
        queue.append(root)

        while queue:
            level = []
            for i in range(len(queue)):
                cur = queue.pop(0)
                if cur == None:
                    level.append('null')
                else:
                    level.append(cur.val)
                    queue.append(cur.left)
                    queue.append(cur.right)
            if level != level[::-1]:
                return False
        return True
            
                    
```



#### 路径总和I

![image-20200627195346347](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200627195346347.png)

递归

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def hasPathSum(self, root: TreeNode, sum: int) -> bool:
        if root==None:
            return False
        sum -= root.val
        if root.left is None and root.right is None:
            return sum == 0
        
        return self.hasPathSum(root.left,sum) or self.hasPathSum(root.right,sum)
        
```



找出所有满足条件的路径

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def hasPathSum(self, root: TreeNode, sum: int) -> bool:
        self.all_router = []
        self.router = []
        self.findrouter(root,sum)
        print(self.all_router)
        
        
    
    def findrouter(self,root,sum):
        if root == None:
            return []
        
        self.router.append(root.val)
        sum -= root.val
        if root.left == None and root.right == None:
            # print(self.router)
            if sum == 0:
                # print(self.router)
                self.all_router.append(self.router[:])
        
        self.findrouter(root.left,sum)
        self.findrouter(root.right,sum)
        self.router.pop()  #灵魂所在 每次遍历完一条路径，返回上个节点
```



#### 构造二叉树

##### 前序和中序 构造二叉树

![image-20200627203127032](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200627203127032.png)

**思路：还是使用递归的方法，每次找到根节点以及它的位置**  

**递归每次找到它左右子在遍历中的范围。**

![image-20200627203324408](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200627203324408.png)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if preorder ==[]:
            return None
        root = TreeNode(preorder[0])
        root_index = inorder.index(preorder[0])
        root.left = self.buildTree(preorder[1:root_index+1],inorder[:root_index])
        root.right = self.buildTree(preorder[root_index+1:],inorder[root_index+1:])
        
        return root
```

##### 中序后序 构造二叉树

![image-20200627203503719](C:\Users\lili\AppData\Roaming\Typora\typora-user-images\image-20200627203503719.png)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> TreeNode:
        if postorder == []:
            return None
        
        root_index = inorder.index(postorder[-1])
        root = TreeNode(postorder[-1])
        
        root.left = self.buildTree(inorder[:root_index],postorder[:root_index])
        root.right = self.buildTree(inorder[root_index+1:],postorder[root_index:-1])
        return root
```





### 未完成

#### 完美二叉树

#### 二叉树的公共祖先

#### 二叉搜索树

#### N叉树



...