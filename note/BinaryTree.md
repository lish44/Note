# 二叉树
--------

## 定义

## 节点实现
```csharp
public class TreeNode {
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}
```

## 一些遍历

### 前序遍历

根 -> 左 -> 右

Recursive
```csharp
IList<int> l = new List<int> ();
public IList<int> Preorder (TreeNode root) {
    if (root != null) {
        l.Add (root.val);
        Preorder (root.left);
        Preorder (root.right);
    }
    return l;
}
```

Iteration
```csharp
public void PreorderRecursive (TreeNode root) {
    IList<int> l = new List<int> ();
    Stack<TreeNode> s = new Stack<TreeNode> ();
    s.Push (root);// 头先入栈
    while (s.Count > 0) {// 只要栈里还有东西就继续
        TreeNode curNode = s.Pop ();
        l.Add (curNode.val);
        if (curNode.right != null) s.Push (curNode.right);
        if (curNode.left != null) s.Push (curNode.left);
    }
}
```

+ 迭代用栈模拟
+ 因为先进后出特性 加上前序遍历是先 __根__ 后 __左__ 再 __右__ 所以在while循环中 就要 __右__ 先进 __左__ 后进 最后出来的结果就是 先左后右符合前序遍历特点 根的话一开始进去就出来了

### 中序遍历
左 -> 根 -> 右

Recursive
```csharp
public void InorderRecursive (TreeNode root) {
    IList<int> l = new List<int> ();
    Stack<TreeNode> s = new Stack<TreeNode> ();
    TreeNode curNode = root;// 当前节点为已搜索节点 就是存在的节点
    while (s.Count > 0 || curNode != null) {// 只要curNode和s不是空 就继续
        while (curNode != null) {// 一直往左边迭代下去 直到cur为空 只要为空了就说明走到了数的最左下角节点
            s.Push (curNode);// 每次压进去为了回溯
            curNode = curNode.left;
        }
        TreeNode tmpNode = s.Pop ();// while出来了就说明 s里面的栈顶的节点没得左子树了 s里面的栈顶的节点就是要找的点
        l.Add (tmpNode.val);
        if (tmpNode.right != null) curNode = tmpNode.right;// 这里就是看 弹出来这个点 右边还有没子树 有的话就给cur 然后以cur为基准进行新的一轮while（里面的while）直到cur为空 s也为空
    }
}
```

+ 总的来说就是用一个栈来模拟，创建一个cur指针，一直往左边的节点迭代下去，每次迭代都入栈，当走到最后一个（也就是最左边那个节点）就停止（整个迭代在while里面进行），然后操作栈顶的元素（第一次的话就是最左下节点），取出来看它还有没右子节点，有的话cur指过去，然后while的时候又入栈 也就是说在子while中每都次以cur为路线找左节点 如此循环，再利用了栈的特性 直到右节点为空并且栈也为空时撒过

标准简化模板
```c++
void InorderIterator(TreeNode* root) {
    if (!root) return NULL;
    stack<TreeNode*> s;
    while (root || !s.empty()) {
        while (root) { // 一直往左走
            s.push(root);
            root = root->left;
        }
        root = s.top(); s.pop();// 走到底就弹出来
        // root就是操作空间
        root = root->right;// 看弹出来的node右边还有没有，没有的话root就是NULL，子while也不会继续走 
    }
}
```

### 二叉树构建
#### 构建方式
[×] 只有前序 5种状态
[×] 前后序 2种状态
[√] 前中序
[√] 中后序


#### 通过前序中序构建

前序遍历在数组中的第一位就是根节点root 但是无法确定左右子树

![Rehma-BuildTree-1.jpg](../pic/Rehma-BuildTree-1.jpg)

--------

通过中序遍历的结果关系可已确定左右子树

![Rehma-BuildTree-2.jpg](../pic/Rehma-BuildTree-2.jpg) 
--------

进而在前序遍历中确定 左右子树

![Rehma-BuildTree-3.jpg](../pic/Rehma-BuildTree-3.jpg) 
--------

通过递归以相同的方法继续构建左右子树 此时左子树只有一个不用管了 右边有三个大于一个 递归继续

![Rehma-BuildTree-4.jpg](../pic/Rehma-BuildTree-4.jpg) 
--------

确定子树位置

![Rehma-BuildTree-5.jpg](../pic/Rehma-BuildTree-5.jpg) 
--------

完成构建

![Rehma-BuildTree-6.jpg](../pic/Rehma-BuildTree-6.jpg) 
--------

#### 计算边界和递归范围

首先确定pre数组左右边界 __[rpeL,preR]__ （闭区间）in数组同理

![Rehma-BuildTree-7.jpg](../pic/Rehma-BuildTree-7.jpg) 

+ `preL + 1` 就是在前序遍历中的 <font color=#ffbc32>left左子树</font> __左边界__
+ `pIdx - inL + preL` 就是在前序遍历中的 <font color=#ffbc32>left左子树</font> __右边界__
    + 咋个理解? `pIdx - inL + preL` 其实就是<font color=#ffbc32>left黄色</font> 块块的宽度，是通过inorder 算的。
    + 然后实际上 [<font color=#ffbc32>left</font> 的 __右边界__ : `pIdx - 1 - inL`] + [<font color=#ffbc32>left</font>的 __左边界__ : `preL + 1`] = `pIdx - inL + preL`
+ `pIdx` 就是中序遍历中<font color=#0aa858>root</font> 的下标
+ 其他位置如图同理计算

#### 实现步骤

1. 首先记录两个数组的长度
```Csharp
int preLen = preorder.Length;
int inLen = inorder.Length;
```

2. 特判一下
```Csharp
if (preLen != inLen) return new TreeNode();
```

3. 用字典存一下中序遍历的下标与与值
```Csharp
Dictionary<int, int> dic = new Dictionary<int, int> ();
for (int i = 0; i < inLen; ++i) {
    dic.Add (inorder[i], i);
}
```

4. 编写递归函数参数条件
```Csharp
return RecBuildTree (preorder, 0, preLen - 1, dic, 0, inLen - 1);
```

5. 递归实现
```Csharp
private TreeNode RecBuildTree (int[] preorder, int preL, int preR, Dictionary<int, int> inorderdic, int inL, int inR) {
    if (preL > preR || inL > inR) return null;

    int rootVal = preorder[preL]; // 找到根节点值
    TreeNode root = new TreeNode (rootVal); //创建
    // 找到前序遍历的root节点 在中序遍历中的位置 通过dic获取 
    int pIdx = inorderdic[rootVal];
    //然后构建 模糊的话更上面的图来结合其看
    root.left = RecBuildTree (preorder, preL + 1, pIdx - inL + preL, inorderdic, inL, pIdx - 1);

    root.right = RecBuildTree (preorder, pIdx - inL + preL + 1, preR, inorderdic, pIdx + 1, inR);

    return root;
}
```

#### 精选代码
```Csharp
public TreeNode BuildTree (int[] preorder, int[] inorder) {
    return helper (0, 0, inorder.Length - 1, preorder, inorder);
}

private TreeNode helper (int preStart, int inStart, int inEnd, int[] preorder, int[] inorder) {
    // 递归终止条件 
    if (preStart > preorder.Length - 1 || inStart > inEnd) return null;

    // 构建root
    TreeNode root = new TreeNode (preorder[preStart]);

    // Index of current root in inorder
    int inIdex = 0;
    // 在 inorder 里面找 root 
    for (int i = inStart; i <= inEnd; ++i)
        if (inorder[i] == root.val)
            inIdex = i;
    // 递归构建 rec
    root.left = helper (preStart + 1, inStart, inIdex - 1, preorder, inorder);

    root.right = helper (preStart + inIdex - inStart + 1, inIdex + 1, inEnd, preorder, inorder);

    return root;
}
```

#### 通过中序后序构建

原理和前中一样 只不过 <font color=#0aa858>root</font> 的确定不一样 __前序__ 是以 __第一个__ 为准, 而 __后序__ 是以 __最后一个__ 为准 然后都是通过 __中序__ 确定<font color=#ffbc32>左</font><font color=#4285f4>右</font>子树位置

![Rehma-BuildTree-8.jpg](../pic/Rehma-BuildTree-8.jpg) 

### 位置边界的计算

![Rehma-BuildTree-9.jpg](../pic/Rehma-BuildTree-9.jpg) 

+ `poL + pIdx - inL - 1` 是 <font color=#ffbc32>left左子树</font> 的 __右边界__
    + 咋个理解？`pIdx - inL - 1` 就是 <font color=#ffbc32>left黄色</font> 块块的宽度因为在inorder中 <font color=#ffbc32>left</font> 的 __右边界__ 正好在 `pIdx` 的左边 所以就是 `[pIdx - 1] - [inL]` 最后加上`poL` 
+ 其他同理理解

源代码
```Csharp
Dictionary<int, int> postDic = new Dictionary<int, int> (); // 做缓存
int[] post;
public TreeNode BuildTree1 (int[] inorder, int[] postorder) {
    if (inorder.Length != postorder.Length) return new TreeNode (); // 特判
    int len = inorder.Length;
    for (int i = 0; i < len; ++i)
        postDic.Add (inorder[i], i); // 缓存 值和对应下标 方便递归查找

    post = postorder; // 为了让递归跟清晰明了

    return PostorderHelper (0, len - 1, 0, len - 1);
}

private TreeNode PostorderHelper (int poL, int poR, int inL, int inR) {
    int rootVal = post[poR];// 后序的最后一个就是root节点的val
    int pIdx = postDic[rootVal];// 取到root在中序中的下标位置
    TreeNode root = new TreeNode (rootVal);
    // 计算边界 参考图
    root.left = PostorderHelper (poL, poL + pIdx - inL - 1, inL, pIdx - 1);
    root.right = PostorderHelper (poL + pIdx - inL, poR - 1, pIdx + 1, inR);
    return root;
}
```
### 总结范围

__在前中序里头__ 

前序 left的右边界就是 `pIdx - inL + preL` 

__在后中序里头__ 

中序 left的右边界就是 `pIdx - inL + poL - 1`


### ssssssssssss
--------

### 基本定义
**度** 

一个节点有几个娃儿就有几个度，二叉树的度 **0 <= 度 <= 2** <++>
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/BinaryTree1.png)

**层** 

![pic](https://raw.githubusercontent.com/lish44/pic/main/res/BinaryTree2.png)

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

![pic](https://raw.githubusercontent.com/lish44/pic/main/res/BinaryTree3.png)
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

