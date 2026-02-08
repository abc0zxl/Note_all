# 注意

1.目前HBuilerX还不支持typeScript的语法报错，VsCode可以

# TypeScript

他是一款解决javascript缺点的编程语言

**特点**：

1.包含javascript的特性

2.**静态类型检查**：一个变量定义时，必须要提前好声明他的数据类型

* 动态类型语言，允许在打代码时，不明确他的数据类型，如，let num;
* 动态类型的闭端是在打代码时遇到类型混乱的错误，他不会报错，运行时才会报错
* TypeScript他能解决这个问题，可以检查这种错误。

3.**代码补全**：

4.**重构**：

5.**简写符号**：提高编码效率

## 大概使用过程

**总的来说**：TypeScript像是JavaScript的补全，先用TypeScript编写代码，然后再转换成JavaScript用来运行。

1.**编码**：

因为再打代码中javascript的错误无法自动检查出来，只有在代码运行时才会出来。

**所以先用TypeScript来写代码，让代码更健壮。**

2.**转换语言**：因为TypeScript不能再浏览器运行，所以要先把它转换为JavaScript

3.**运行**

## 实现步骤

1.**安装TypeScript**：去官网下载

**![image.png](/assets/8ba75908-0826-4752-a93c-db69985bf5d4.png)**

---

## 细节报错

if里的参数上的？导致这个参数可能不存在，下面的方法逻辑上就会，可能导致一个参数为空，所以ts会报错

，这时就要在if中加上return来返回


![image.png](/assets/e0b0012d-a807-4e1c-a6f9-971ae6c9663b.png)
