# section2 二叉树属性
### 题单
- [x] 101.对称二叉树
- [x] 100.相同的树
- [x] 572.另一个树的子树
- [x] 104.二叉树最大深度
- [x] 559.N叉树的最大深度
- [x] 111.二叉树最小深度
- [x] 222.完全二叉树的节点个数
- [x] 110.平衡二叉树
- [x] 257.二叉树的所有路径
- [x] 404.左叶子之和
- [x] 513.找树左下角的值
- [x] 112.路径总和
- [x] 113.路径总和2

### 解析：
##### 101.对称二叉树
核心是`层序遍历`，之后再对每一层的元素进行收尾比较
##### 100.相同的树
核心是`分治法`，两个数相同，一定是当前节点相等，同时各自的左子树相同，同时右子树相同
```python
"""
① 相同树判断
"""
def equal(root1, root2):
    if root1 and not root2:
        return False
    if not root1 and root2:
        return False
    if not root1 and not root2:
        return True
    if root1.val != root2.val:
        return False
    return equal(root1.left, root2.left) and equal(root1.right, root2.right)
```
##### 572.另一个树的子树
遍历节点，然后执行 equal，找打相同则停止遍历；
需要注意的是，递归到子树时，也需要加上判断，如果子树判断是相同树了，就可以直接返回 True 了；
##### 104.二叉树最大深度
深度遍历，找到叶子节点时，判断 max
##### 559.N叉树的最大深度
深度遍历，找到叶子节点时，判断 max
##### 111.二叉树最小深度
深度遍历，找到叶子节点时，判断 min
##### 222.完全二叉树的节点个数
遍历计数，复杂度 O(n)；
有更优的解，以后补充；
##### 110.平衡二叉树
深度遍历，如果数是平衡的，返回树的高度，否则返回-1
```python
def traverse(root):
    if not root:
        return 0
    
    left_h = traverse(root.left)
    if left_h == -1:
        return -1
    right_h = traverse(root.right)
    if right_h == -1:
        return -1
    
    if abs(left_h-right_h) > 1:
        return -1
    
    return max(left_h, right_h) + 1
```
##### 257.二叉树的所有路径
深度遍历过程中记录路径，遇到叶子节点时输出逻辑，需要注意记录的路径(内存空间)是否会在后续遍历中继续修改
##### 404.左叶子之和
深度遍历过程中记录当前节点是否是左子树，遇到叶子节点判断一下是否是左叶子，然后累加 val 即可；
##### 513.找树左下角的值
中序遍历过程中记录深度，遇到叶子节点判断深度大小，深度大才更新最下层做节点；
中序遍历保证了，同一层的叶子节点，第一个一定是最左节点
##### 112.路径总和
深度遍历过程中记录路径累加和，遇到叶子节点则判断是否等于 target；一旦找到 target 则停止遍历
##### 113.路径总和2
深度遍历过程中记录路径和累加和，遇到叶子节点则判断是否等于 target；相等 target 则将路径记录起来，然后继续遍历；

### 总结
记住基础的遍历代码框架，无非是在其基础上做各种变化；增加一些变量，记录一些结果等等；

同时本小节也接触到了`分治法`，后续将经常碰见；