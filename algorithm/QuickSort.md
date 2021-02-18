# 快速排序
--------

### 基本思想

+ 选择基准：按某种标准随便选一个元素作为**基准**
+ 分割操作：以基准为目标（中心）比基准小的元素在基准左边，大的在基准右边，分成左部分和右部分（左子序列 右子序列）
+ 递归操作：把左右子序列当进行同样的操作（递归）直到子序列为空或者只有一个元素

### 代码实现
```c++
void Quicksort (vector<int> &arr, int left, int right){
    if (left < right){
        
        int key = arr[left];
        int low = left;
        int high = right;
        
        while (low < high) {//如果相等本轮左右筛选完成
            while (low < high && arr[high] >= key) {//以key为基准 从后向前比较 比基准大就往前-- 否则 交换
                high--;
            }
            swap(arr[low], arr[high]);
            
            while (low < high && arr[low] <= key) {//以key为基准 从前向后比较 比基准小就往后-- 否则 交换
                low++;
            }
            swap(arr[low], arr[high]);
        }
        
        Quicksort(arr, left, low - 1);//先递归左边部分
        Quicksort(arr, low + 1, right);
    }
}
```
