# 指针

### 指针变量 
--------
+ 指针值所存的就是 **变量或对象** 的地址
```c++
int m_a = 10;		//m_a的地址OxAAAA AAA1
int* ptr_a = &m_a;	//“&”(取地址符) ptr_a的值就是OxAAAA AAA1
cout << *ptr_a << endl;	//10   “*”在指针前解引用

```
+ 指针类型确定**寻址空间** 
    + 不同机器所占空间不一定 [](基本数据类型) [传送门][baseType]  
    + 指针加减等于 ptr + (sizeof(type) * xx) 如 `ptr+1` 实际上做了如下操作
        + 在64位机上移动了八位`(sizeof(int)*1)` -> 8
        + 在32位机上移动了四位`(sizeof(int)*1)` -> 4

```c++
double m_arr[] = {10,20};
double* ptr_arr = m_arr;//&m_arr[0] 数组名本质是指针
cout << ptr_arr << endl;
cout << ptr_arr + 1 << endl;
//
```

![pic](https://github.com/lish44/Note/blob/master/pic/%E6%88%AA%E5%B1%8F2019-12-05%E4%B8%8A%E5%8D%8811.12.34.png)


[baseType]:https://github.com/lish44/Note/blob/master/C%2B%2B/%E5%9F%BA%E6%9C%AC%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.md
