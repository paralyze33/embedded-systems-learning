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

