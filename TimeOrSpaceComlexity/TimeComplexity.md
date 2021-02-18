### 时间复杂度
--------

**Big O notatione**

O(1) : Constant Complexity 常数复杂度

O(log n): Logarithmic Complexity对数复杂度

O(n): Linear Complexity线性时间复杂度

O(n2): N square Complexity平方

O(n~3): N square Complexity立方

O(2^n): Exponential Growth指数

O(n): Factorial p阶乘
### 对数
㏒<sub>10</sub>100 = 2 理解成:多少个10相乘得到100 答案是10*10 $\color{#4285f4}2个$

㏒<sub>2</sub>8 = 3 `==` 2<sup>3</sup> = 8 理解成:多少个2相乘等于8 答案是2 * 2 * 2 $\color{#4285f4}3个$

通常省略2 写成log n
### 对于递归的时间复杂
斐波拉西数列
```c++
int fib (int n) {
    if (n <= 1) return n;
    return fib (n-1) + fib (n-2);
}
```
展开树（递归树）

![RecursionTree](../pic/RecursionTree.png) 

### 主定理
解决所有递归函数的时间复杂度问题

![RecursionTree2](../pic/RecursionTree2.png) 

基本二叉树的遍历 前 中 后 时间复杂度是 O(n): 因为可以看成每个节点都要访问一次所以是O(n)

图的遍历也是 O(n) 

DFS、BfS 也是 O(n)

二分查找是 O(log n) : 因为每次砍一半，搜索规模也小一半
