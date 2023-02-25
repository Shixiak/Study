# C语言复习
# 浙大版《C语言程序设计（第4版）》题目集
## 练习 5-3 字符金字塔
```C
#include <stdio.h>

void CharPyramid( int n, char ch );

int main()
{
    int n;
    char ch;

    scanf("%d %c", &n, &ch);
    CharPyramid(n, ch);

    return 0;
}

/* 请在这里填写答案 */
void CharPyramid( int n, char ch )
{
    for (int i=1; i <= n; i++)
    {
        for (int j=1; j <= n; j++)
        {
            if (j <= n-i)
                printf(" ");
            else
                printf("%c ",ch);
        }
        printf("\n");
    }
}
```
> 一般般，挺简单的

## 习题 5-1 使用函数求奇数和
```C
#include <stdio.h>

#define MAXN 10

int even( int n );
int OddSum( int List[], int N );

int main()
{
    int List[MAXN], N, i;

    scanf("%d", &N);
    printf("Sum of ( ");
    for ( i=0; i<N; i++ ) {
        scanf("%d", &List[i]);
        if ( even(List[i])==0 )
            printf("%d ", List[i]);
    }
    printf(" )= %d\n", OddSum(List, N));

    return 0;
}

/* 你的代码将被嵌在这里 */
int even( int n )
{
    if (n%2 == 0)
        return 1;
    else
        return 0;
}
int OddSum( int List[], int N)
{
    int result = 0;
    for ( int i=0; i < N; i++)
    {
        if ( !even(List[i]))
        {
            result += List[i];
        }
    }
    return result;
}
```
> 别问，问就是简单
## 习题5-5 使用函数统计指定数字的个数
```C
#include <stdio.h>

int CountDigit( int number, int digit );

int main()
{
    int number, digit;

    scanf("%d %d", &number, &digit);
    printf("Number of digit %d in %d: %d\n", digit, number, CountDigit(number, digit));

    return 0;
}

/* 你的代码将被嵌在这里 */
int CountDigit( int number, int digit )
{
    int temp,count = 0;
    if (number < 0)
        number = number*(-1);
    while (number)
    {
        temp  = number%10;
        if (temp == digit)
            count++;
        number /= 10;
    }
    return count;
}
```
> 没考虑到number为负数的时候，小输一波

## 习题5-7 使用函数求余弦函数的近似值
```C
#include <stdio.h>
#include <math.h>

double funcos( double e, double x );
double mypow( double x, int n);
int Fact( int n);
int main()
{
    double e, x;

    scanf("%lf %lf", &e, &x);
    printf("cos(%.2f) = %.6f\n", x, funcos(e, x));

    return 0;
}

/* 你的代码将被嵌在这里 */
double funcos( double e, double x )
{
    int f = 1,n = 0;
    double result = 0,addent = 0;
    do
    {
        addent = mypow(x,n)/Fact(n);
        result += addent*f;
        n += 2;
        f = -f;
    }while (addent > e);

    return result;
}

double mypow( double x, int n)
{
    int temp = n;
    double result = 1;
    if (n < 0) temp = -n;
    for (int i = 0;i < temp;i++)
        result *= x;
    if (n > 0)
        return result;
    else
        return 1/result;
}

int Fact( int n)
{
    int result = 1;
    for (int i = 1; i <= n; i++)
    {
        result *= i;
    }
    return result;
}
```
> 一堆小错误，真的拉跨


## 习题6-3 使用函数输出指定范围内的完数
```C
#include <stdio.h>

int factorsum( int number );
void PrintPN( int m, int n );
void PrintN( int n);

int main()
{
    int m, n;

    scanf("%d %d", &m, &n);
    if ( factorsum(m) == m ) printf("%d is a perfect number\n", m);
    if ( factorsum(n) == n ) printf("%d is a perfect number\n", n);
    PrintPN(m, n);

    return 0;
}

/* 你的代码将被嵌在这里 */
int factorsum( int number )
{
    int result = 0;
    for (int k = 1; k < number; k++)
        if ( number%k == 0)
            result += k;
    return result;
}
void PrintPN( int m, int n )
{
    int count = 0;
    for (int i=m; i <= n; i++)
    {
        if (factorsum(i) == i)
        {
            PrintN(i);
            printf("\n");
            count++;
        }
    }
    if (count == 0) printf("No perfect number\n");
}
void PrintN( int n)
{
    printf("%d = 1 ",n);
    for (int k = 2; k < n; k++)
        if (n%k == 0) printf("+ %d ",k);
}
```
## 习题8-3 数组循环右移
```C
#include <stdio.h>
#define MAXN 10

void ArrayShift( int a[], int n, int m );

int main()
{
    int a[MAXN], n, m;
    int i;

    scanf("%d %d", &n, &m);
    for ( i = 0; i < n; i++ ) scanf("%d", &a[i]);

    ArrayShift(a, n, m);

    for ( i = 0; i < n; i++ ) {
        if (i != 0) printf(" ");
        printf("%d", a[i]);
    }
    printf("\n");

    return 0;
}

/* 你的代码将被嵌在这里 */
void ArrayShift( int a[], int n, int m )
{
    int temp[10],k = 0;
    for (int i = n-m; i<n; i++)
        temp[k++] = a[i];
    for (int i = n-m-1; i >= 0; i--)
        a[i+m] = a[i];
    for (k = 0; k < m; k++)
        a[k] = temp[k];
}
```
> 这代码风格我是真的喜欢
## 习题8-4 报数（约瑟夫环）
```C
#include <stdio.h>
#include <stdlib.h>
#define MAXN 20

void CountOff( int n, int m, int out[] );

int main()
{
    int out[MAXN], n, m;
    int i;

    scanf("%d %d", &n, &m);
    CountOff( n, m, out );
    for ( i = 0; i < n; i++ )
        printf("%d ", out[i]);
    printf("\n");

    return 0;
}

/* 你的代码将被嵌在这里 */
void CountOff( int n, int m, int out[] )
{
    int count = n, k = 0, order = 0;
    int *person = (int*)malloc(sizeof(int)*n);
    //k为数组下标，order为每个人报的序号

    for (int i=0;i<n;i++)
        person[i] = i+1;
    while (count != 0)
    {
        if (person[k] != 0) order++;
        if (order == m)
        {
		    count--;
            order = 0;
            out[person[k]-1] =n - count;
            person[k] = 0;
        }
        k++;
        if (k == n) k = 0;
    }
}
```
> 挺有意思一道题，约瑟夫环

## 习题9-2 计算两个复数之积
```C
#include <stdio.h>

struct complex{
    int real;
    int imag;
};

struct complex multiply(struct complex x, struct complex y);

int main()
{
    struct complex product, x, y;

    scanf("%d%d%d%d", &x.real, &x.imag, &y.real, &y.imag);
    product = multiply(x, y);
    printf("(%d+%di) * (%d+%di) = %d + %di\n",
            x.real, x.imag, y.real, y.imag, product.real, product.imag);

    return 0;
}

/* 你的代码将被嵌在这里 */
struct complex multiply(struct complex x, struct complex y)
{
    struct complex result;
    result.real = x.real * y.real - x.imag * y.imag;
    result.imag = x.imag * y.real + x.real * y.imag;
    return result;
}
```
> 轻松拿捏
## 习题9-6 按等级统计学生成绩
```C
#include <stdio.h>
#define MAXN 10

struct student{
    int num;
    char name[20];
    int score;
    char grade;
};

int set_grade( struct student *p, int n );

int main()
{   struct student stu[MAXN], *ptr;
    int n, i, count;

    ptr = stu;
    scanf("%d\n", &n);
    for(i = 0; i < n; i++){
       scanf("%d%s%d", &stu[i].num, stu[i].name, &stu[i].score);
    }
   count = set_grade(ptr, n);
   printf("The count for failed (<60): %d\n", count);
   printf("The grades:\n");
   for(i = 0; i < n; i++)
       printf("%d %s %c\n", stu[i].num, stu[i].name, stu[i].grade);
    return 0;
}

/* 你的代码将被嵌在这里 */
int set_grade( struct student *p, int n )
{
    int x,p_num = 0;
    for (int i = 0; i < n; i++)
    {
        x = p[i].score;
        if (85 <= x && x <= 100)
            p[i].grade = 'A';
        else if (70 <= x && x <= 84)
            p[i].grade = 'B';
        else if (60 <= x && x <= 69)
            p[i].grade = 'C';
        else
        {
            p[i].grade = 'D';
            p_num++;
        }
    }
    return p_num;
}
```
> 只有一个疑惑，就是为什么p[i].gtade只能用'.'而不能用"->"
## 练习10-1 使用递归函数计算1到n之和
```C
#include <stdio.h>

int sum( int n );

int main()
{
    int n;

    scanf("%d", &n);
    printf ("%d\n", sum(n));

    return 0;
}

/* 你的代码将被嵌在这里 */
int sum(int n)
{
    if (n == 0)
        return 0;
    else
        return n + sum(n-1);
}
```
> 这题没必要刷的

## 习题10-2 递归求阶乘和
```C
#include <stdio.h>

double fact( int n );
double factsum( int n );

int main()
{
    int n;

    scanf("%d",&n);
    printf("fact(%d) = %.0f\n", n, fact(n));
    printf("sum = %.0f\n", factsum(n));

    return 0;
}

/* 你的代码将被嵌在这里 */
double fact (int n)
{
    if (n == 1)
        return 1;
    else
        return n * fact(n-1);
}

double factsum (int n)
{
    if (n == 1)
        return 1;
    else
        return fact(n) + factsum(n-1);
}
```
> 感觉刷起来没多大的必要，，，

## 习题10-4 递归求简单交错幂级数的部分和
```C
#include <stdio.h>

double fn( double x, int n );

int main()
{
    double x;
    int n;

    scanf("%lf %d", &x, &n);
    printf("%.2f\n", fn(x,n));

    return 0;
}

/* 你的代码将被嵌在这里 */

double fn( double x, int n )
{
    if (n == 1)
        return x;
    else if (n == 2)
        return x * (1-x);
    else
        return x * (1 - fn(x,n-1));
}
```
> 我喜欢这道题
## 习题10-5 递归计算Ackermenn函数
```C
#include <stdio.h>

int Ack( int m, int n );

int main()
{
    int m, n;

    scanf("%d %d", &m, &n);
    printf("%d\n", Ack(m, n));

    return 0;
}

/* 你的代码将被嵌在这里 */
int Ack( int m, int n )
{
    if (m == 0)
        return n+1;
    else if (n == 0 && m > 0)
        return Ack(m-1, 1);
    else
        return Ack(m-1,Ack(m,n-1));
}
```
> 我相当喜欢这道题，又简单，但又很深刻
## 习题10-6 递归求Fabonacci数列
```C
#include <stdio.h>

int f( int n );

int main()
{
    int n;

    scanf("%d", &n);
    printf("%d\n", f(n));

    return 0;
}

/* 你的代码将被嵌在这里 */

int f( int n )
{
    if (n == 0)
        return 0;
    else if (n == 1)
        return 1;
    else
        return f(n-1) + f(n-2);
}

```
> 递归好像也挺好用的
## 习题10-7 十进制转换二进制
```C
#include <stdio.h>

void dectobin( int n );

int main()
{
    int n;

    scanf("%d", &n);
    dectobin(n);

    return 0;
}

/* 你的代码将被嵌在这里 */
void dectobin( int n )
{
    if (n/2 == 0)
        printf("%d",n%2);
    else
    {
        dectobin(n/2);
        printf("%d",n%2);
    }
}
```
> 不懂，感觉应该有更简单的

## 习题10-8 递归实现顺序输出整数
```C
#include <stdio.h>

void printdigits( int n );

int main()
{
    int n;

    scanf("%d", &n);
    printdigits(n);

    return 0;
}

/* 你的代码将被嵌在这里 */
void printdigits(int n)
{
    if (n/10 != 0)
    {
        printdigits(n/10);
        printf("%d\n",n%10);
    }
    else
        printf("%d\n",n%10);
}
```
> 三天不练手生
## 习题10-11 有序表的增删改查操作
```C
/* 有序表的增删改查操作 */
#include<stdio.h>
#define MAXN 10000    /* 定义符号常量表示数组a的长度 */

int Count = 0;        /* 用全局变量Count表示数组a中待处理的元素个数 */
void select(int a[], int option, int value); /* 决定对有序数组a进行何种操作的控制函数 */
int input_array(int a[ ]);    /* 输入有序数组a的函数 */
void print_array(int a[ ]);    /* 输出有序数组a的函数 */
int insert(int a[ ], int value);    /* 在有序数组a中插入一个值为value的元素的函数 */
int del(int a[ ], int value);    /* 删除有序数组a中等于value的元素的函数 */
int modify(int a[ ], int value1, int value2); /* 将有序数组a中等于value1的元素，替换为value2 */
int query(int a[ ], int value);     /* 用二分法在有序数组a中查找元素value的函数 */

int main(void)
{
    int option, value, a[MAXN];

    if(input_array(a) == -1){     /* 调用函数输入有序数组 a */
         printf("Error");        /* a不是有序数组，则输出相应的信息 */
         return 0;
    }

    printf("[1] Insert\n");    /* 以下4行显示菜单*/
    printf("[2] Delete\n");
    printf("[3] Update\n");
    printf("[4] Query\n");
    printf("[Other option] End\n");
    while (1) /* 循环 */
    {
        scanf("%d", &option);         /* 接受用户输入的编号 */
        if (option < 1 || option > 4) {    /* 如果输入1、2、3、4以外的编号，结束循环 */
            break;
        }
        scanf("%d", &value);         /* 接受用户输入的参数value */
        select(a, option, value);         /* 调用控制函数 */
        printf("\n");
    }
    printf("Thanks.");            /* 结束操作 */

    return 0;
}

/* 控制函数 */
void select(int a[ ], int option, int value)
{
    int index, value2;

    switch (option) {
        case 1:
            index = insert(a, value);      /* 调用插入函数在有序数组 a 中插入元素value */
            if(index == -1){        /* 插入数据已存在，则输出相应的信息 */
                printf("Error");
            }else{
                print_array(a);        /* 调用输出函数，输出插入后的有序数组a */
            }
            break;
        case 2:
            index = del(a, value);      /* 调用删除函数在有序数组 a 中删除元素value */
            if(index == -1){        /* 没找到value，则输出相应的信息 */
                printf("Deletion failed.");
        }else{
            print_array(a);         /* 调用输出函数，输出删除后的有序数组a */
        }
            break;
        case 3:
            scanf("%d", &value2);         /* 接受用户输入的参数value2 */
            index = modify(a, value, value2);      /* 调用修改函数在有序数组 a 中修改元素value的值为value2 */
            if(index == -1){            /* 没找到value或者vaule2已存在，则输出相应的信息 */
                printf("Update failed.");
            }else{
            print_array(a);         /* 调用输出函数，输出修改后的有序数组a */
            }
            break;
        case 4:
            index = query(a, value);     /* 调用查询函数在有序数组 a 中查找元素value */
            if(index == -1){        /* 没找到value，则输出相应的信息 */
                printf( "Not found.");
            }else{            /* 找到，则输出对应的下标 */
            printf("%d", index);
            }
            break;
    }
}

/* 有序表输入函数 */
int input_array(int a[ ])
{
    scanf("%d", &Count);
    for (int i = 0; i < Count; i ++) {
        scanf("%d", &a[i]);
        if(i > 0 && a[i] <= a[i-1]){    /* a不是有序数组 */
            return -1;
        }
    }

    return 0;
}

/* 有序表输出函数 */
void print_array(int a[ ])
{
    for (int i = 0; i < Count; i ++) { /* 输出时相邻数字间用一个空格分开，行末无空格 */
        if(i == 0){
           printf("%d", a[i]);
        }else{
           printf(" %d", a[i]);
        }
    }
}

/* 请在这里填写答案 */
int insert(int a[ ], int value)
{
    for (int i = 0; i < Count-1; i++)
    {
        if (a[i] < value)
        {
            if (value < a[i+1])
            {
                for (int j = Count; j > i+1; j--)
                    a[j] = a[j-1];
                a[i+1] = value;
                Count++;
                return 1;
            }
            else if (value == a[i+1])
                return -1;
            else if (i == Count-1)
            {
                a[Count] = value;
                Count++;
                return 1;
            }
        }
    }
}
int del(int a[ ], int value)
{
    int pos;
    pos = query(a,value);
    if (pos == -1)
        return -1;
    else
    {
        for (int i = pos; i < Count-1; i++)
            a[i] = a[i+1];
        Count -= 1;
        return 1;
    }
}
int modify(int a[ ], int value1, int value2)
{
    int f;
    f = del(a,value1);
    if (f == -1)
        return -1;
    else
    {
        f = insert(a,value2);
        if (f == -1)
            return -1;
        return 1;
    }
}
int query(int a[ ], int value)
{
    int m,n,i;
    m = 0;n = Count;
    while (m+1 < n)
    {
        if (value > a[(m+n)/2])
            m = (m+n)/2;
        else
            n = (m+n)/2;
    }
    if (value == a[n])
        return n;
    else if (value == a[m])
        return m;
    else
        return -1;
}
// a[i] < value <a[i+1]
//1 2 3 4 5 6 8
//0 1 2 3 4 5 6
//value = 7:m = 3 -> m = 4 -> m = 5
```
> 还费了我好一会儿
## 习题11-4 字符串的连接
```C
#include <stdio.h>
#include <string.h>

#define MAXS 10

char *str_cat( char *s, char *t );

int main()
{
    char *p;
    char str1[MAXS+MAXS] = {'\0'}, str2[MAXS] = {'\0'};

    scanf("%s%s", str1, str2);
    p = str_cat(str1, str2);
    printf("%s\n%s\n", p, str1);

    return 0;
}

/* 你的代码将被嵌在这里 */
char *str_cat( char *s, char *t )
{
    char *p;
    p = strcat(s,t);
    return p;
}
```
> 本来是不想用strcat，但是你头函数带了string.h那就不好意思了
## 习题11-6 查找子串
```C
#include <stdio.h>
#define MAXS 30

char *search(char *s, char *t);

int main()
{
    char s[MAXS], t[MAXS], *pos;

    gets(s);
    gets(t);
    pos = search(s, t);
    if ( pos != NULL )
        printf("%d\n", pos - s);
    else
        printf("-1\n");

    return 0;
}

/* 你的代码将被嵌在这里 */
char* search( char *s, char *t )
{
    char *result;
    int l_t, i, count = 0, pos2=0;

    for ( l_t = 0; t[l_t] != '\0'; l_t++ );
    for ( i=0; s[i] != '\0';)
    {
        while ( s[i++] == t[pos2++] && s[i-1] != '\0')
            count++;

        if ( count == l_t)
            return s+i-l_t-1;
        else
        {
            count = 0;
            pos2 = 0;
        }
    }
    return NULL;
}
/* 你的代码将被嵌在这里 */
char* search( char *s, char *t )
{
    char *result;
    int l_t, i, count = 0, pos2=0;

    for (l_t = 0; t[l_t] != '\0'; l_t++);
    for (i=0; s[i] != '\0';)
    {
        while (s[i++] == t[pos2++] && s[i-1] != '\0')
            count++;

        if (count == l_t)
            return s+i-l_t-1;
        else
        {
            count = 0;
            pos2 = 0;
        }
    }
    return NULL;
}
```
> 没救了，没救了，debug用了好久
## 习题11-8 单链表结点删除
```C
#include <stdio.h>
#include <stdlib.h>

struct ListNode {
    int data;
    struct ListNode *next;
};

struct ListNode *readlist();
struct ListNode *deletem( struct ListNode *L, int m );
void printlist( struct ListNode *L )
{
     struct ListNode *p = L;
     while (p) {
           printf("%d ", p->data);
           p = p->next;
     }
     printf("\n");
}

int main()
{
    int m;
    struct ListNode *L = readlist();
    scanf("%d", &m);
    L = deletem(L, m);
    printlist(L);

    return 0;
}

/* 你的代码将被嵌在这里 */
struct ListNode *readlist()
{
    struct ListNode *head,*Pt,*prePt;


    Pt = (struct ListNode*)malloc(sizeof(struct ListNode));
    if (Pt == NULL) exit(-1);
    scanf("%d", &Pt->data);
    if (Pt->data == -1){
        free(Pt);
        Pt = NULL;
    }
    head = Pt;
    prePt = head;
    while (prePt) {
        Pt = (struct ListNode*)malloc(sizeof(struct ListNode));
        if (Pt == NULL) exit(-1);
        scanf("%d", &Pt->data);
        if (Pt->data == -1) {
            free(Pt);
            Pt = NULL;
        }
        prePt->next = Pt;
        prePt = Pt;
    }
    return head;
}

struct ListNode *deletem( struct ListNode *L, int m )
{
    struct ListNode *Pt,*prePt,*head;

    head = L;
    while (1) {
        if (head->data == m) {
            Pt = head;
            head = Pt->next;
            free(Pt);
        }
        else break;
    }
    prePt = head;
    Pt = head->next;
    while (Pt) {
        if ( Pt->data == m) {
            prePt->next = Pt->next;
            free(Pt);
            Pt = prePt->next;
            continue;
        }
        prePt = prePt->next;
        Pt = prePt->next;
    }
    return head;
}
```
> C语言基本复习完了吧

Practice/review.md
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA3NTE4NTM5NF19
-->