# LeetCode  
## ！1.两数之和
### 方法一：双重循环
```C
int* twoSum(int* nums, int numsSize, int target, int* returnSize)
{
    for (int i = 0; i < numsSize; ++i) {
        for (int j = i + 1; j < numsSize; ++j) {
            if (nums[i] + nums[j] == target) {
                int* ret = malloc(sizeof(int) * 2);
                ret[0] = i, ret[1] = j;
                *returnSize = 2;
                return ret;
            }
        }
    }
    *returnSize = 0;
    return NULL;
}
```
* 二分查找 ==target - nums[i]==
其实也可以优化一下，如果第一个数确定了就能锁定出第二个数的值，然后利用二分查找在数组里面查找是否存在这个数。当然这需要传入数组是一个有序的数组，但是考虑到这种算法的时间复杂度为O(nlogn)，所以可以利用快排函数qsort先进行排序，再进行二分查找。
### ！方法二：哈希表
## ！53.最大子数组和  
###  方法一：动态规划  

```C
int maxArray(int* nums,int numsSize)
{
	int ans = nums[0],sumi = nums[0];
	
	for (int i =; i < numsSize; i++) {
		sumi = fmax(sumi + nums[i], nums[i]);
		ans = fmax(sum,ans);
	}
	
	return ans;
}
```
* ==sumi==是以第i个元素结尾的最大子数列和
* ==ans==就应该是数组==sumi==中最大的一个
### ！方法二：分而治之  

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


## ！118.杨辉三角
### 方法一
```C
int** generate(int numRows, int* returnSize, int** returnColumnSizes) {
	//numRows和returnSize中存储的是杨辉三角的行数
	//*returnColumnSizes存储的是列数的数组的首地址,(*returnColumnSizes)[0]表示的是第0行的列数
	//returnColumnSizes是int**型变量，则*reuturnColumnSizes是int*型变量，指向int,可以理解为数组的首地址
	
    int** ret = malloc(sizeof(int*) * numRows);
    
    *returnSize = numRows;
    *returnColumnSizes = malloc(sizeof(int) * numRows);
    for (int i = 0; i < numRows; ++i) {
        ret[i] = malloc(sizeof(int) * (i + 1));
        //ret[i]表示的是第i行数组的首地址
        (*returnColumnSizes)[i] = i + 1;
        ret[i][0] = ret[i][i] = 1;
        for (int j = 1; j < i; ++j) {
            ret[i][j] = ret[i - 1][j] + ret[i - 1][j - 1];
        }
    }
    
    return ret;
}
```
* 二级指针真的。。。
* 反复抄了几遍代码，感觉对二级指针有些理解了
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
 ### ！快排函数的原理

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


### ！方法二：哈希表

```C  
```    



* 哈希表的使用（目前还没有学这个玩意）  

## 566.重塑矩阵
### ！方法一：二维数组的一维表示
```C
//int** nums表示传入的二维数组
//int numSize表示传入数组的长度
//int r,c,分别表示需转换矩阵行数和列数
int** matrixReshape(int** nums, int numsSize, int* numsColSize, int r, int c, int* returnSize, int** returnColumnSizes) {
    //第一步判断两个矩阵元素数量是否相同
    int m = numsSize;
    int n = numsColSize[0];
    //numsColSize[0]存的是数组nums的列数
    if (m * n != r * c) {
        *returnSize = numsSize;
        *returnColumnSizes = numsColSize;
        return nums;
    }
    *returnSize = r;
    *returnColumnSizes = malloc(sizeof(int) * r);
    //每行都应该有一个ColumnSize吧，所以应该 *r
    int** ans = malloc(sizeof(int*) * r);

    for (int i = 0; i < r; i++) {
        (*returnColumnSizes)[i] = c;
        //每一行的列数都是c
        ans[i] = malloc(sizeof(int) * c);
        //ans[i]是第i行数组的首地址
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
eyJoaXN0b3J5IjpbLTQwMjY0NTk1MywxOTk3ODc4NjU1LC02Nz
E3Mjk2MjgsMjE4MjcxMjc4LC0xMzgyMzQzOTMyLDQ0OTQ1OTQ2
LC0xNzAxNTY1MzM4LDEyMTc2MDU2MzgsOTE3MDQ4MDIxLC0xND
U5MDgyNjk1LC0xMTQ5NjAzNDMxLC0xNDU2MDA4NTQ1LDE4NjE0
OTc2NjIsMTYzOTEyNzI2MiwyMDI2MzY5MjEzLDEzODY4NzY1NT
AsLTIzNTAzNTM1MiwxMzUxNzY4Mjg0LDMxODUxNzEzOCwzMjIw
MTUwXX0=
-->