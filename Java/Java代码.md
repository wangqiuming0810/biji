```java
import java.math.BigInteger;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        BigInteger a,b;
        int t;
        t=sc.nextInt();
        for(int i=1;i<=t;i++){
            if(i!=1) System.out.println();
            a=sc.nextBigInteger();
            b=sc.nextBigInteger();
            System.out.println("Case "+i+":");
            System.out.println(a+" + "+b+ " = "+a.add(b));
        }
    }
}

```



Java的输入输出必须要先定义一个输入的类，

```java
Scanner sc = new Scanner(System.in);//遇到空格结束
//输入int型
int t = sc.nextInt();
//输入大整数
BigInteger a=sc.nextBigInteger();
//输入string类型，java的字符串类型S要大写。
String str=sc.next();//遇到空格结束
String str=sc.nextLine();//整行读入，类似于c++，getline(cin,str);
```



大数加法

```java
import java.math.BigInteger;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        BigInteger a=sc.nextBigInteger();
        BigInteger b=sc.nextBigInteger();
        BigInteger c=sc.nextBigInteger();
        System.out.println(a.add(b.add(c)));
    }
}

```

