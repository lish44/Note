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
