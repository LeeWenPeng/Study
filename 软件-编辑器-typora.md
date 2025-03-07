1. **快捷键**

## 1. 数学公式

   + 大括号

	 ```markdown
     $$
     \begin{cases}
     第一行 \\
     第二行
     \end{cases}
     $$
     ```

	 > `	\\`：用于换行

   + 对齐符号：`&`

	 ```markdown
     $$
     f(x) = \begin{cases}
     1 &x=1,2 \\
     f(x-1) + f(x-2)  &x>2
     \end{cases}
     $$
     ```

	 从`&`在的位置对齐

	 效果图：

	 ![image-20230510094207785](typora的使用/img/image-20230510094207785.png)

   + 空格

	 ```markdown
     $$
     \space
     \quad
     \qquad
     $$
     ```

   + 矩阵

	 ```markdown
     $$
     {\left[ \begin{matrix}
     f(n) &f(n-1) \\
     f(n-1) &f(n-2)
     \end{matrix} \right]} =
     
     {\left[ \begin{matrix}
     1 &1 \\
     1 &0
     \end{matrix} \right]}^{n-1}
     $$
     ```

	 > 左右符号： `\left[` 和 `\right]`
	 >
	 > + 行列式可以换成 `\left|` 和 `\right|`

   + 分数

	   语法: `\frac{<分子>}{<分母>}`

	   ```markdown
       $$
       T(n) = aT(\frac{n}{b})+f(n)
       $$
       ```

3. **希腊数字**

   [希腊字母Typora格式 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/165369211)

## 2. 内联代码中的反引号

使用两个反引号包裹

`` `asdasd`dasdad` ``

其中的反引号，需要与包裹的反引号之间有空格
