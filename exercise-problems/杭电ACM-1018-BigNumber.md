##Problem Description

> In many applications very large integers numbers are required. Some of these applications are using keys for secure transmission of data, encryption, etc. In this problem you are given a number, you have to determine the number of digits in the factorial of the number.

####Input

> Input consists of several lines of integer numbers. The first line contains an integer n, which is the number of cases to be tested, followed by n lines, one integer 1 ≤ n ≤ 107 on each line.

####Output

> The output contains the number of digits in the factorial of the integers appearing in the input.

####Sample Input
````
2

10

20
````
####Sample Output
````
7

19
````
>首先分析一下这个题目的具体内容，输入一个数N，接着输入N个数，求出它们的阶乘并输出。
实例 输入2 ，然后输入两个数10、20，输入为7、19，分别为10的阶乘结果的位数和20的阶乘结果的位数。
由于阶乘的结果是一个大数，Int类型无法解决，生活中大数的应用有很多，Java中有一个类BigIntegera表示大整数类。理论上可以表示无限大的数，用这个解决十分方便。

###以下是关于BigIntegera的用法：

####Ⅰ基本函数：
````
1.valueOf(parament); 将参数转换为制定的类型
   比如 int a=3;
   BigInteger b=BigInteger.valueOf(a);
   则b=3;
   String s=”12345”;
   BigInteger c=BigInteger.valueOf(s);
   则c=12345；
 2.add(); 大整数相加
   BigInteger a=new BigInteger(“23”);
   BigInteger b=new BigInteger(“34”);
   a. add(b);
 3.subtract(); 相减
 4.multiply(); 相乘
 5.divide();    相除取整 
 6.remainder(); 取余
 7.pow();   a.pow(b)=a^b 
 8.gcd();   最大公约数
 9.abs(); 绝对值
 10.negate(); 取反数
 11.mod(); a.mod(b)=a%b=a.remainder(b);
 12.max(); min();
 13.punlic int comareTo();
 14.boolean equals(); 是否相等
 15.BigInteger构造函数：
   一般用到以下两种：
   BigInteger(String val);
   将指定字符串转换为十进制表示形式；
   BigInteger(String val,int radix);
   将指定基数的 BigInteger 的字符串表示形式转换为 BigInteger
````
####Ⅱ.基本常量：
````
A=BigInteger.ONE    1
B=BigInteger.TEN    10
C=BigInteger.ZERO   0
````
####Ⅲ.基本操作
 读入：
用Scanner类定义对象进行控制台读入,Scanner类在java.util.*包中
````
Scanner cin=new Scanner(System.in);// 读入
while(cin.hasNext())   //等同于!=EOF
{
   int n;
   BigInteger m;
   n=cin.nextInt(); //读入一个int;
   m=cin.BigInteger();//读入一个BigInteger;
System.out.print(m.toString());
}
````
下面是我用java写的解决方法，主要是通过for循环求出某个数的阶乘，

注意大数中的 1 的定义为     BigInteger a=BigInteger.ONE;       

Int 类型通过String.valueOf()转化再定义为BigInteger类型的数才可以与BigInteger类型的数进行运算。
````
public class Bigdata {    
public static void main(String[] args){        
    Scanner in = new Scanner(System.in);       
    int num = in.nextInt();        
    for(int i=0;i<num;i++ ){            
        int text = in.nextInt();            
        BigInteger a=BigInteger.ONE;           
        for(int j=1;j<=text;j++){                
            BigInteger c = new BigInteger(String.valueOf(j));                
            a = a.multiply(c);            
    }            
    System.out.println(String.valueOf(a).length());        
}    
}}

````
