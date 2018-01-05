# 高（gao）级（ji）计算器使用说明

## 一般计算的语法说明：

1,加减乘除分别为+-*/

2,支持`sin,cos,tan,atan,acos,asin`,这些三角函数输入的时候必须带括号

例如sin(3*6+5),使用的并非角度制而是弧度制，转换成角度时候在后面加上*180/p(p为预设的π值，约为3.14159265358979323846)，比如：
`sin((3*6+5)*180/3)`

3,支持abs(),用法同sin(),意思是求绝对值

4,log的语法为log(n,表达式),例如：`log(2,1024/2*4)`不支持ln，但是预存了e，使用`log(e,e^2)`即可计算ln(e^2)，结果为2.

5,!为阶乘，^为幂次方，因为输入限制，不支持根号，根号2可输入2^0.5,三次根号8可以输入为8^(1/3)

## 高级计算语法说明：
### (1)积分语法说明

使用的变量为小写的x，不要书成X。

大致语法为`intg(a:deepth:b,exp)`

a,b为初值与终值，输反了没关系。

deepth是精度的二次深度，

如果精度深度为7,则其会将a~b这个区间均匀划分为2^7=128份

一般结果要求5位有效精度的话，需要划分256~512个区间，即深度为8或9

例如，求x^2从-2到3上的积分（实际结果大约为11又三分之二）

`intg(-2:9:3,x^2)`

暂时不支持多重积分和曲线积分

### (2)微分语法说明

`difx(x0,f(x))`即可求f(x)在x0处的导数

例如:`difx(-2,x^2)`

### (3)线性方程求零点语法说明

`cqux(a,b,c,exp)`

将解出exp=0的所有根中间离a最近的一个根

b是搜索步长，不影响最终精度，但是太大可能漏解

c是精度等级，实际上δx是0.5的c次方

例子：`cqux(1:0.1,18,x^2-5)`

由于精度提高引起运算量的变化很小，一般22以上无压力，可以适当取大一些。

### (4)一阶常微分方程数值解语法说明

`dqux(x0,y0,x1,dx,exp)`

y的一阶导数输入y'即可

y0=y(x0),是微分方程的初始条件，否则有无穷个解

x1是所求的y(x1)的参数

dx是精度，同样是0.5^dx的表达方式。

这个精度对计算量影响很大，建议少一点取10~12，多的取16~18，否则就得等好一会儿了。

例如y'=y-x y(0)=2

(表达式等价于y'-y+x=0或者y-y'-x=0)

两端做拉普拉斯变换以后再做逆变换，得到y=e^x+x+1

y(2)=e^2+3

机解法输入：

`dqux(0,2,2,12,y'-y+x)`

即可

## 测试函数样例
```
difx(-2,x^2)

difx(2,x^3)

difx(1,x^0.5)

difx(0,sin(x))

difx(0,cos(x))

difx(2,e^x)

intg(-3:9:3,x^2)

cqux(1:0.1,4,x^2-5)

cqux(1:0.1,6,x^2-5)

cqux(1:0.1,8,x^2-5)

cqux(1:0.1,10,x^2-5)

cqux(1:0.1,12,x^2-5)

cqux(1:0.1,14,x^2-5)

cqux(1:0.1,16,x^2-5)

cqux(1:0.1,18,x^2-5)

cqux(1:0.1,20,x^2-5)

cqux(1:0.1,22,x^2-5)
```
