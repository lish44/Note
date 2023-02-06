# 冒泡

## 思想 

+ 相邻两元素比较
+ 前数比后数大 交换

### 从前往后
```c++
void Bybubble(vector<int>& arr){
    for (size_t i = 0; i < arr.size(); ++i)
        for (size_t j = 0; j < arr.size() - i -1; ++j)
            if (arr[j] > arr[j+1]) swap(arr[j], arr[j+1]);
}
```

### 从后往前
```c++
void Bybubble (vector<int>& arr){
    for (size_t i = arr.size() - 1; i > 0; --i)
        for (size_t j = i; j > 0; --j)
            if (arr[j] < arr[j-1]) swap(arr[j], arr[j-1]);
}
```
### do_while实现
```c++
void Bybubble(vector<int> &arr){
    bool isTrue;
    do {
        isTrue = false;
        for (size_t i = 0; i < arr.size()-1; i++) {
            if (arr[i] > arr[i+1]){
                swap(arr[i], arr[i+1]);
                isTrue = true;
            }
        }
    } while (isTrue);
}
```



