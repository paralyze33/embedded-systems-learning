# C 语言学习记录｜2026-10-09

## 今日进度

- 视频学习至 **9.2.1 指针**部分。
- 学习重点：`const` 与指针、数组的关系。

## `const` 与指针

### 1. `const` 在 `*` 前面

```c
const int *p;
// 等价写法：int const *p;
```

- `p` 指向的 `int` 不能通过 `p` 修改。
- `p` 本身可以改变，可以再指向其他地址。

```c
int a = 10;
int b = 20;
const int *p = &a;

// *p = 30;  // 错误：不能通过 p 修改所指向的值
p = &b;      // 正确：p 本身可以改变
```

### 2. `const` 在 `*` 后面

```c
int * const p = &a;
```

- `p` 是常量指针，保存的地址不能改变。
- `p` 指向的 `int` 可以修改。

```c
int a = 10;
int b = 20;
int * const p = &a;

*p = 30;  // 正确：可以修改所指向的值
// p = &b; // 错误：p 保存的地址不能改变
```

### 3. 两边都有 `const`

```c
const int * const p = &a;
```

- 不能通过 `p` 修改所指向的值。
- `p` 本身也不能指向其他地址。

## `const` 与数组

```c
const int a[] = {1, 2, 3};
```

- 数组的每个元素都是 `const int`，因此不能执行 `a[0] = 10;`。
- 数组本身不是指针；只是在多数表达式中，数组名会转换为指向首元素的指针。
- 在函数参数中，`const int a[]` 会被调整为 `const int *a`，表示函数不能通过参数修改数组元素。

```c
void printArray(const int a[], int length)
{
    // a[0] = 10;  // 错误：不能通过 a 修改数组元素
}
```

## 记忆方法

- `const int *p`：`*p` 不能改，`p` 可以改。
- `int * const p`：`p` 不能改，`*p` 可以改。
- `const int * const p`：`p` 和 `*p` 都不能改。

## 今日练习代码

### 练习一：统计数字 `0`～`9` 的出现次数

程序不断读取整数，输入 `-1` 时结束；只有 `0`～`9` 范围内的数字会被统计。

编译与运行：

```powershell
gcc -std=c99 -Wall -Wextra main.c -o main.exe
.\main.exe
```

源码：

```c
#include <stdio.h>

int main(void) {
    const int number = 10;
    int x;
    int count[number];
    int i;

    for (i = 0; i < number; i++) {
        count[i] = 0;
    }

    scanf("%d", &x);
    while (x != -1) {
        if (x >= 0 && x <= 9) {
            count[x]++;
        }
        scanf("%d", &x);
    }

    for (i = 0; i < number; i++) {
        printf("%d:%d\n", i, count[i]);
    }

    return 0;
}
```

### 练习二：输出前 100 个素数

程序用已经找到的素数判断候选整数是否为素数，并将结果按每行 5 个输出。

编译与运行：

```powershell
gcc -std=c99 -Wall -Wextra prime100.c -o prime100.exe
.\prime100.exe
```

源码：

```c
#include <stdio.h>

int isPrime(int x, int knownPrimes[], int numberOfKnownPrimes);

int main(void)
{
    enum { number = 100 };
    int prime[number] = {2};
    int count = 1;
    int i = 3;

    while (count < number) {
        if (isPrime(i, prime, count)) {
            prime[count++] = i;
        }
        i++;
    }

    for (i = 0; i < number; i++) {
        printf("%d", prime[i]);
        if ((i + 1) % 5) {
            printf("\t");
        } else {
            printf("\n");
        }
    }

    return 0;
}

int isPrime(int x, int knownPrimes[], int numberOfKnownPrimes)
{
    int ret = 1;
    int i;

    for (i = 0; i < numberOfKnownPrimes; i++) {
        if (x % knownPrimes[i] == 0) {
            ret = 0;
            break;
        }
    }

    return ret;
}
```
