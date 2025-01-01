# C 程序示例 - 张浩

> Author: 张浩
>
> Date: 2023-12

浩哥写的是真的很不错，作为优秀作品来给大家打个样。

希望后来者努力学习，更进一步。

下面是示例代码。

```c
#include<stdio.h>
#include <assert.h>
#include <stdlib.h>
#include <string.h>
#include<stdarg.h>

int main(int argc,char *argv[])
{
    // 15. 指针
    char *name = "jim";
    printf("name自身%p,name指向%s\n", &name,name);

    int ages[] = {12, 22, 34, 44, 53};
    printf("ages[0]:%d\nages[3]:%d\n", (*ages), (*(ages+3)));
    printf("ages:%p", ages);

    int ages_2[2][2] = { {1,2},{4,5} };
    int *p_2 = ages_2[0];
    printf("ages_2[0][1]:%d\n(ages_2[1][0]):%d\n", ((*p_2)+1), (*(p_2+2)));

    // 16. 结构体和指向他们的指针
    struct Person {
        char *name;
        int age;
        int height;
        int weight;
    };

    struct Person joe = {"Joe Alex", 32, 64, 140};

    printf("Name: %s\n", joe.name);
        printf("\tAge: %d\n", joe.age);
        printf("\tHeight: %d\n", joe.height);
        printf("\tWeight: %d\n", joe.weight);

    // 17. 堆和栈
    int *arr;
    int n = 5;
    
    arr = (int*) malloc(n * sizeof(int));
    if (arr == NULL) {
        fprintf(stderr, "内存错误!\n");
        return -1;
    }
    // 初始化并打印数组
    for (int i = 0; i < n; i++) {
        arr[i] = i * i;
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    free(arr);

    // 18. 函数指针
    //回调函数
    int max(int a, int b) {
        return a > b ? a : b;
    }    
    int min(int a, int b)
    {
        return a < b ? a : b;
    }

    int (*p1)(int, int);
    p1 = max;
    printf("结果:%d\n",p1(45,76));

    printf("\n调用函数max\n");
    int more(int a, int b, int (*p)(int ,int))
    {
        printf("结果%d\n", max(a,b));
        return 0;
    }

    printf("\n调用函数min\n");
    int less(int a, int b, int(*p)(int,int))
    {
        printf("结果%d\n", min(a,b));
    }

    more(12, 23, max);
    less(12, 23, min);

    //指针函数
    int *app1(int a ){
        return 0;
    }

    printf("指针函数%p", app1(10));
    free(app1(10));

    // 24. IO函数
    int a = 0;
    printf("\n用fscanf输入一个整数\n");
    fscanf(stdin, "%d", &a);
    fprintf(stdout, "%d", a);

    // fgets()
    char str[20];  
        printf("请输入一个字符串:\n");
        fgets(str, 10, stdin);  
        printf("%s\n", str);

    // fopen()
    FILE *p222 = fopen("./123.c", "r");
        if(p222 == NULL)
        {
            printf("文件打开失败 !\n");
        }else
        {
            printf("文件打开成功 !\n");

            // 如果打开成功 , 则需要关闭文件
            fclose(p222);
        }

    printf("fopen结束\n\n");

    // 25. 变参函数
    int sum(int numa, ...)
    {
        int suma = 0;
        va_list ap;
        int i;

        va_start(ap, numa);
        for(i = 0; i < numa; i++)
        {
            suma += va_arg(ap, int);
        }
        va_end(ap);
        
        return suma;
    }
    int sum_1 = sum(3, 4, 5, 6);
    printf("sum_1:%d\n", sum_1);

    // main 结束
    printf("\nmain结束\n");
    return 0;
}
```