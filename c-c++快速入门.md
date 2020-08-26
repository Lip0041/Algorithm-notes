# C/C++快速入门

## 基本数据类型

 - 位运算符

| 运算符 | 含义 | 语法 | 效果|
| :-: | :-: | :-: | :-: |
| << | 左移 | a << x | 整数 a 按二进制位左移x位|
| >> | 右移 | a >> x | 整数 a 按二进制位右移x位|
| & | 位与| a & b| 整数 a 和 b 按二进制对齐，按位进行与运算（除了11得1，其他均为0）|
| \| | 位或| a \| b|整数 a 和 b 按二进制对齐，按位进行或运算（除了00得0，其他均为1）|
|^| 位异或| a ^ b| 整数 a 和 b 按二进制对齐，按位进行异或运算（相同为0，不同为1）|
| ~| 位取反| ~ a| 整数 a 的二进制的每一位进行0变1，1变0的操作|
## 数组

1. 如果数组大小约10^6^级别，则需要定义在主函数外面——栈大小限制

2. 对数组每一个元素赋相同的值

   ```c
   memset(数组名, 值, sizeof(数组名));  
   //值可使用0，-1，该函数在头文件 string.h 中
   ```

3. `sscanf` 与 `sprintf` ： 在 `stdio.h` 中

   ```c
   int n;
   double db;
   char str[100];
   sscanf(str, "%d%lf", &n, &db);//将字符数组中str中的内容以"%d%lf"的形式写到n和db中，从左至右
   sprintf(str, "%d", n);//把n以"%d"的形式写到str字符数组中，从右至左
   ```

## 补充

1. 浮点数比较

   引入一个极小数 `eps = 1e-8` 来进行比较

   ```c++
   const double eps = 1e-8;
   # define Equ(a, b) ((fabs((a) - (b))) < (eps)) //比较是否相等
   # define More(a, b) (((a) - (b)) > (eps)) //比较是否a > b, 即 a > b + eps
   # define Less(a, b) (((a) - (b)) < (-eps)) //比较是否a < b, 即 a < b - eps
   ```

2. 圆周率π 

   ```c++
   const double Pi = acos(-1.0);
   ```

3. C语言为二维数组分配连续内存 [参考链接](https://geek-docs.com/cprogramming/c-pointer/c-allocates-contiguous-memory-to-two-dimensional-arrays.html)——思路：**先分配外层数组**

   ```c
   // 分配行数rows个整数指针数组，每个元素存储一行的指针
   int **matrix = (int **) malloc(rows * sizeof(int *));
   // 在二维数组首地址处为所有元素(rows * columns)分配内存
   matrix[0] = (int *) malloc(rows * columns * sizeof(int));
   // 整个指针数组的每个指针相应的已经分配的内存
   for (int i = 1; i < rows; i++)
       matrix[i] = matrix[0] + i * columns;
   ```

   