# 二叉排序树
## 删除节点：
### 伪代码实现：
```
delete_val(n){
    if n.left == nullptr and n.right == nullptr
        delete n
    if n.right == nullptr
        tmp = n->left
        delete n
        n = tmp
    elseif n.left == nullptr
        tmp = n->right
        delete n
        n = tmp
    else
        tmp = n
        maxValNode = n.left
        while maxValNode.right != nullptr
            tmp = maxValNode
            maxValNode = maxValNode.right
        n.data = maxValNode.data
        if tmp == n
            tmp.left = maxValNode.left
        else
            tmp.right = maxValNode.left
        delete maxValNode

```
### 证明：
被删除的节点只有4种情况：
1. 没有左右孩子(即为叶子节点)
    - 直接删除当前节点
2. 只有左孩子
    - 删除当前节点，并用左孩子替代当前节点
3. 只有右孩子
    - 删除当前节点，并用右孩子替代当前节点
4. 同时有左右孩子<br>
在这种情况下，删除当前节点后还需要使树仍然具有bst的性质。注意到左子树的任意节点值<待删除节点值<右子树的任意节点值，因此可以找max(左子树值)或者min(右子树值)来替代当前删除节点的值。<br>
下面证明用max(左子树值)进行替代的过程：<br>
假设左子树根节点为L，则仅有以下两种情况：
    - L无右子树，即L节点就是整个左子树最大值。此时删除L，并连接L左子树即可满足bst性质。
    - L有右子树，此时一直向右子树遍历可找到L的最大值节点M。注意此时节点M可能还有左子树，令M的前驱的右孩子为M的左子树，即能使L满足bst性质。
