#  编译原理-语法分析-自顶向下-LL

## 什么是语法分析？

一个编程语言可以由上下文无关文法生成，如下面的例子：

```
S -> AB
A -> CD
C -> int|void
D -> name
B -> {E}
E -> FE|ε
F -> sentence
```

便是一个可以描述函数的文法（仅举例，不保证严谨性）

```c
int main{
    int a;
}
// S -> AB,A -> CD,C -> int,D -> main,B -> {E},E -> FE,F -> int a;,E -> ε
```

现在我们要根据一个文法来判定所写代码是否符合编程语言定义的语法

## 自顶向下

给定文法（G1.1）:

```
E -> TE'
E' -> +TE'|ε
T -> FT'
T' -> *FT'|ε
F -> (E)|i
```

其中 i 为语法分析得到的id

使用自顶向下方法意味着我们要从初始符E开始，选择合适的产生式最终获得给出的语句

如果说每一次我们都有唯一的选择，那么这个工作将会很好做，但事实上存在很多问题：

* 左递归

如果程序中存在左递归，很有可能会导致我们的分析程序陷入死循环，下面可以使用一种简单的方案去除直接左递归：

```
设 存在 E -> E + T| T
存在直接左递归，则其与以下产生式等价:

E -> T{+T}


```

