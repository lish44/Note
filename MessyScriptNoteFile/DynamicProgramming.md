### 动态规划
--------

**爬楼梯**
自顶向下 递归思路f(n)：爬上n阶楼梯方法数 可以得出f(n) = f(n -1) + f(n-2)
```c++
int climbStairs(int n) {
    if (n == 1)
        return 1;
    if (n == 2)
        return 2;
    return climbStairs(n - 1) + climbStairs(n - 2);
}
```
基于上面的递归思路加入记忆化搜索

```c++
vector<int> memo;
int climbStairs(int n) {
    memo = vector<int>(n + 1, -1);
    return stairsClimb(n);
}
int stairsClimb(int n) {
    assert(n >= 1);
    if (n == 1)
        return 1;
    if (n == 2)
        return 2;
    if (memo[n] != -1)
        return memo[n];
    return memo[n] = stairsClimb(n - 1) + stairsClimb(n - 2);
}
```

自底向上 dp
```c++
int climbStairs(int n) {
    vector<int> memo(n + 1, -1);
    memo[0] = 1;
    memo[1] = 1;
    for (int i = 2; i <= n; ++i) {
        memo[i] = memo[i - 1] + memo[i - 2];
    }
    return memo[n];
}
```

优化dp
```c++
int climbStairs(int n) {
    if (n <= 2)
        return n;
    int i1 = 1;
    int i2 = 2;
    for (int i = 3; i <= n; ++i) {
        int temp = i1 + i2;
        i1 = i2;
        i2 = temp;
    }
    return i2;
}
```
--------


