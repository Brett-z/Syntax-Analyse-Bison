# 语法分析_自动完成语法检测并生成AST

## 介绍&使用说明

**概述：**

​		本次实验在已有基础上，修改了 .l 文件来完成文件的读取，参照 SysY 语言的语法规则并利用Flex-Bison工具链自动完成对SysY语言的语法检测，且生成AST打印在终端。参照如下语法规则：

![sysy语法](https://images.gitee.com/uploads/images/2021/1117/165328_aa4cae8e_9865699.png "RW]X@(~OTOF}4JZOZ9EJGY2.png")

**主要文件介绍：**

1. ast.c & ast.h：主要包含树结构的定义、节点创建函数、树输出函数等；
2. flex 的输入文件 lrlex.l： 主要包含标识符、关键字、数字、符号的读取；
3. bison 的输入文件 lrparser.y：主要包含各种语法的节点创建规则等；
4. main.c 为主函数，调用 yyparser() 来生成树；
5. expr.txt 为测试用例；

**文件关系介绍：**

1. lrparser.y 文件中定义有联合体来存放 lrlex.l 文件识别到的每一个标识符、关键字、数字、符号；
2. lrparser.y 文件中根据文法创建节点时，需要用到 ast.c 中的节点创建函数；
3. main.c 需要用到的 yyparser() 函数由 lrparser.y 生成。

**使用步骤 & 要点说明：**

1. 本次实验均在 linux 环境下测试运行，作者使用的虚拟机镜像为 ubuntu；
2. 若 linux 环境下未安装 flex 与 bison 需要安装，可输入 --version 查看是否安装，若未安装请按照终端提示命令行进行安装！
3. 首先将 lrlex.l 作为 flex 的输入文件，生成 lex.yy.c（词法分析器） ，需要用到以下语句：

~~~ 
flex lrlex.l
~~~

3. 经步骤2后会发现终端提示有warning，但已正确生成 lex.yy.c ，因此可忽略；
4. 将 lrparser.y 作为 bison 的输入文件，生成 lrparser.tab.c 与 lrparser.tab.h，需要用到以下语句：

~~~ 
bison -d lrparser.y
~~~

5. 经步骤4后会发现终端提示有一个移进/规约冲突，但已正确生成目标文件 ，因此可忽略；
6. 最后，利用命令行编译 lrparser.tab.c  、lex.yy.c 、ast.c 、main.c 生成可执行文件，需要用到以下语句：

~~~ 
gcc -o test.exe lrparser.tab.c lex.yy.c ast.c main.c
~~~

7. 生成的 test.exe 可执行文件即可以对 SysY 语言进行语法分析并且生成AST。
8. 步骤图如下：

![输入图片说明](graph/%E6%AD%A5%E9%AA%A4.png)

 **注意：在进行案例的测试时：**

1. 检查文件时，需要在命令行输入文件名；如：./test.exe  expr.txt；
2. 终端只能输入一个参数（文件名），否则无法完成相应功能。

## 运行结果展示

1. 若前文所述步骤均成功完成，即可完成以下测试：


2. 测试用例为：

```c
int a,b;
int main(){
    a=10;
    b=5;
    int c=a*2+b+3;
    return c;
}
```
3. 测试结果为：

![输入图片说明](graph/%E8%BF%90%E8%A1%8C%E7%BB%93%E6%9E%9C.png)

## 作者
曾彬芮 2021/11/30 于四川成都

( 对代码有疑问可联系： e-mail： brettemail@163.com || 392184316@qq.com )