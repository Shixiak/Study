# LeetCode  
## 53.最大子数组和  
###  方法一：动态规划  

```C  
//  
int maxSubArray(int* nums, int numsSize)   
{  
    int result;  
    int* f = (int*)malloc(sizeof(int) * numsSize);  
  
    f[0] = nums[0];  
  
    for (int i = 1; i < numsSize; i++) {  
        f[i] = fmax(f[i - 1] + nums[i], nums[i]);  
    }  
	//动态规划的核心思想，将问题细化为以nums[i]结尾的最大子数组  
    result = f[0];  
  
    for (int i = 1; i < numsSize; i++) {  
        result = fmax(result, f[i]);  
    }  
  
    free(f);  
    return result;  
}  
```  

* 定义状态（定义子问题）  
  

 **f [ i ]** 是以 **nums[ i ]** 结尾的最大子数组，**res = max { f [ i ] }**  

 * 状态转移方程（描述子问题之间的关系）  
  

 **f [ i ]  = max { f [ i-1 ] + nums[ i ] , nums[ i ] }**   

 * 初始化  
  

 **f [ 0 ] = nums[ 0 ]**，i > 1 是可由递推关系获得  

 * 输出  
  

 **res = max { f [ i ] }**  
  

### 方法二：分而治之  

```C  
```  

## 88.合并两个有序数组  

#### 代码  

方法一：快排函数  

```C  
int cmp(const void* _a, const void* _b)  
{  
	int a = *(int*)_a, b = *(int*)_b;  
	return a - b;  
}  
  
bool containsDuplicate(int* nums, int numsSize)   
{  
	qsort(nums, numsSize, sizeof(nums[0]), cmp);  
	for (int i=0; i<numsSize-1; i++) {  
		if (nums[i] == nums[i+1]) {  
			return true;  
	}  
}  
  
return false;  
}  
```  

方法二：双指针  
  

#### 收获  

* 本来还挺高兴能够活学活用qsort函数，结果反手看解析直接由被薄纱  



## 217.存在重复元素
### 方法一：排序  
```C  
int cmp(const void* _a, const void* _b) {  
    int a = *(int*)_a, b = *(int*)_b;  
    return a - b;  
}  
  
bool containsDuplicate(int* nums, int numsSize) {  
    qsort(nums, numsSize, sizeof(int), cmp);  
    for (int i = 0; i < numsSize - 1; i++) {  
        if (nums[i] == nums[i + 1]) {  
            return true;  
        }  
    }  
    return false;  
}  
```  
* qsort 快排函数的使用
* const void* 是可以转换为任意类型的空白指针
* 
  

### 方法二：哈希表（待补全）  

```C  
```    

### 快排函数的原理

```C  
void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void*))  
//base -- 需要排序的数组  
//nitems -- 元素的个数  
//size -- 单个元素所占的字节数  
//compar -- 比较大小的函数  
```  

```C  
//暂未搞清楚原理  
#include <stdio.h>  
  
int a[100], n, temp;  
  
void QuickSort(int h, int t)  
{  
	//h为首位置，t为末尾位置  
    if(h >= t) return; //确保h < n  
       
    int mid = (h + t) / 2, i = h, j = t, x;  
    x = a[mid];  
    while(1)  
    {  
        while(a[i] < x)  
            i++;  
        while(a[j] > x)   
            j--;  
        if(i >= j)   
             break;  
        temp = a[i];  
        a[i] = a[j];  
        a[j] = temp;  
    }  
     a[j] = x;  
     QuickSort(h, j - 1);  
     QuickSort(j + 1, t);  
     return ;  
}  
  
int main()  
{  
     int i;  
     scanf("%d", &n);  
     for(i = 0; i < n; i++)  
         scanf("%d", &a[i]);  
     QuickSort(0, n - 1);  
     for(i = 0; i < n; i++)   
         printf("%d ", a[i]);  
     return 0;  
}  
```  

* 哈希表的使用（目前还没有学这个玩意）  

## 566.重塑矩阵
### 方法一：二维数组的一维表示
```C
//int** nums表示传入的二维数组
//int numSize表示传入数组的长度
int** matrixReshape(int** nums, int numsSize, int* numsColSize, int r, int c, int* returnSize, int** returnColumnSizes) {
    int m = numsSize;
    int n = numsColSize[0];
    if (m * n != r * c) {
        *returnSize = numsSize;
        *returnColumnSizes = numsColSize;
        return nums;
    }
    *returnSize = r;
    *returnColumnSizes = malloc(sizeof(int) * r);
    int** ans = malloc(sizeof(int*) * r);

    for (int i = 0; i < r; i++) {
        (*returnColumnSizes)[i] = c;
        ans[i] = malloc(sizeof(int) * c);
    }
    for (int x = 0; x < m * n; ++x) {
        ans[x / c][x % c] = nums[x / n][x % n];
    }
    return ans;
}
```
* 二级指针

二级指针，我看你是一点都不懂啊
  
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM4NTE1NDg0NywtMjM1MDM1MzUyLDEzNT
E3NjgyODQsMzE4NTE3MTM4LDMyMjAxNTBdfQ==
-->