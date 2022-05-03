# Compiler-Notes

Record Notes When Learning Compiler



## CH 7 语义分析和中间代码生成

### 中间语言

语法分析器 -> 静态语义检查器 -> 中间代码生成器 -> 优化器

静态语义检查：类型、控制流、一致性、相关名字、名字作用域check

**很多编译程序采用独立于机器的、复杂性介于源语言和机器语言之间的中间语言**

![image-20220503093904311](https://vvtorres.oss-cn-beijing.aliyuncs.com/image-20220503093904311.png)

#### 后缀式

运算量在前、算符在后。

**运算优先级**由高到低：

#### 图表示法

抽象语法树

DAG图：可以识别公共子表达式，在代码优化部分介绍

#### 三地址代码

三地址语句的种类

1. x = y op z ，op 为二元算法算符

2. x = op y，op 为一元算符

3. x = y，赋值

4. goto L    无条件转移

5. if x relop y goto L 或 if a goto L，条件转移，relop： <= < = > >=

6. 过程调用param x和 call p,n以及返回return y

   p(x1,x2,x3…xn)

   param x1

   param x2

   …

   param xn

   call p,n

7. x = y[i]   x[i] = y
8. x = &y     x = *y     *x = y

##### 四元式

**(op,arg1,arg2,result)**

op 代表运算符的内部码，arg1,arg2为两个运算数，result为结果域

---

**[例7.5]** a = b * -c + b * -c 的四元式

**[解析]**	T1 = -c

​				T2 = b * T1

​				T3 = -c

​				T4 = b* T3

​				T5 = T2 + T4

**[解答]** 	(uminus,c,-,T1)

​				(*,b,T1,T2)

​				(uminus,c,-T3)

​				(*,b,T3,T4)

​				(+,T2,T4,T5)

​				(=,T5,-,a)   // 等于就是这么写的  arg2 = -           a = T5 

---

#### 三元式

为了避免把临时变量填入到符号表，可以通过**计算这个临时变量的语句位置**来引用这个临时变量，这样只需要三个域**(op,arg1,arg2),此时的result 就是 编号**

​				(0) (uminus,c,-)

​				(1) (*,b,(0))

​				(2) (uminus,c,-T3)

​				(3) (*,b,(2))

​				(4) (+,(1),(3))

​				(5) (=,a,(4))  





​			







