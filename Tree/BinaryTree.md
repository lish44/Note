### 二叉树
--------

### 基本定义
**度** 

一个节点有几个娃儿就有几个度，二叉树的度 **0 <= 度 <= 2** <++>
![binarytree1](../pic/BinaryTree1.png) 

**层** 

![binarytree2](../pic/BinaryTree2.png) 

**特点** 

+ 在二叉树的第i层上最多有2^i-1 个节点 。（i>=1）如第二层最多2个，三层最多4个节点

**深度和高度** 

深度从上到下 计算时从0开始，如果只有一个节点其深度为1，否则结果+1

高度从下到上 计算时从0开始，

计算树高度其实就计算树的深度
+ 递归往下走直到最大叶子节点
```c++
int BinaryTreeHeight(Node *node)
{
    int treeHeight = 0;
    if (node != NULL)
    {
        int leftHeight = BinaryTreeHeight(node->lChild);
        int rightHeight = BinaryTreeHeight(node->rChild);
        treeHeight = leftHeight >= rightHeight? leftHeight + 1:rightHeight + 1;
    }
 
    return treeHeight;
}
```

![BinaryTree3](../pic/BinaryTree3.png) 
```c++
int BinaryTree::Depth(Node* root){
    if (!root) return 0;//没有东西就反0
    
    int left = Depth(root->left);
    int right = Depth(root->right);
    
    return left > right ? left + 1 : right + 1;
}
```

**个数** 
```c++
int BinaryTree::Size(Node* root) const {
    if (!root) return 0;
    return Size(root->left) + Size(root->right) + 1;
}
```

<++>




### 二叉树前序遍历
我想先打印头节点对吧？那我打印完了头节点，我现在想打印左边节点了，<u>我只是告诉计算机我想打印左边结点，之后打印右边结点</u>。

递归
```c++
vector<int> ans;
vector<int> preorderTraversal(TreeNode* root) {
    if(root){//当前节点不为空
        ans.push_back(root -> val);
        preorderTraversal(root -> left);一直递归左边直到为空 出栈返回上一层去右边
        preorderTraversal(root -> right);
    }
    return ans;
}
```

迭代 用栈模拟
```c++
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> ans;
    stack<TreeNode*> s;
    s.push(root);//头先入栈
    while (!s.empty()) {//只要栈里还有东西
        TreeNode* node = s.top(); s.pop();//出栈保存当前节点引用
        ans.push_back(node->val);
        //因为先进后出 右边先进左边再进 出来的时候右边就先出来符合前序遍历要求
        if (node->right) s.push(node->right);
        if (node->left) s.push(node->left);
    }
    
    return ans;
}
```

### 二叉树中序遍历
同上 只不过这次先看左边节点，直到左边没有返回当前父节点，然后在去右边看
```C++
void inOrderIteration(TreeNode* root) {
    if (root){
        inOrderIteration(root->left);
        cout << root->val << " ";
        inOrderIteration(root->right);
    }
}
```

迭代
思路：用一个栈来模拟，创建一个cur指针，一直往左边的节点迭代下去，每次迭代都入栈，当走到最后一个（也就是最左边那个节点）就停止（整个迭代在while里面进行），然后操作栈顶的元素（第一次的话就是最左下节点），取出来看它还有没右子节点，有的话cur指过去，然后while的时候又入栈 如此循环，直到右节点为空并且栈也为空时撒过
```c++
void inOrderIteration(TreeNode* head) {
    stack<TreeNode*> s;
    TreeNode* cur = head;
    //整个循环建立在s不为空 或者 cur 不为空
    while (!s.empty() || cur) {
        while (cur) {//只要有就一直往左边走下去并且每步都入栈
            s.push(cur);
            cur = cur->left;
        }
        TreeNode* node = s.top(); s.pop();//取栈顶第一个
        cout << node->val << " ";
        //从取出来那个节点开始找右边有没得，有就cur指到它，为了在下次循环（也就是上面第二个while）入栈
        if(node->right) cur = node->right;
    }
}
```

### 二叉树后序遍历

### 二叉树中序遍历

这里中序遍历就是一层一层访问，bfs用一个队列实现，先把根节点入队列，在迭代里头取队列第一个，如果有子节点就又压入，先左后右，直到队列为空访问结束
```c++
void layerTraversal(Node* root){
    if(!root) return;
    queue<Node*> q;
    q.push(root);//根节点加入
    while (!q.empty()) {
        auto t = q.front();q.pop();
        cout << t->val << " ";
        if (t->left) q.push(t->left);
        if (t->right) q.push(t->right);
    }
}
```


