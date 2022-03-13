# 1.API

## 1.包装类

### 1.包装类

​	将java中8种基本数据类型进行包装,包装成对应的引用数据类型.

### 2.类型

​            byte -- Byte
​            short -- Short
​            int -- Integer
​            long -- Long
​            float -- Float
​            double -- Double
​            char -- Character
​            boolean -- Boolean

### 3.基本类型和字符串的转换

​    方案一:
​        int ---> String :   利用字符串的拼接: 10 + ""
​        String ---> int :   Integer.parseInt()

​    方案二:
​        int ---> String :   利用String.valueOF(int)
​        String ---> int :   利用Integer.valueOF(String)

```java
int str = Integer.parseInt("123");
int num = Integer.valueOf("123");
		 Integer num = Integer.valueOf("123")
          int num = num.intValue();
String num = 123 + "" ;
String num = String.valueOf(123);
```

​	1.装箱:将基本数据类型变成对应的包装类类型
​	2.自动装箱:底层JVM会自动调用包装类的valueOF操作进行数据封装.
​	3.拆箱:将包装类类型转为对应的基本类型
​	4.自动拆箱:底层JVM会自动调用包装类的intValue操作,进行数据还原基本类型的操作
​	注意事项:包装类属于引用数据类型,是可以记录null值得

## 2.二分查找

数组的二分查找步骤:

​	1，定义两个变量，表示要查找的范围。默认min = 0 ， max = 最大索引 (arr.length-1)
​	2，循环查找，条件是min <= max
​	3，计算出mid的值为(min+max)/2
​	4，判断mid位置的元素是否为要查找的元素，如果是直接返回对应索引
​	5，如果要查找的值在mid的左半边，那么min值不变，max = mid -1.继续下次循环查找
​	6，如果要查找的值在mid的右半边，那么max值不变，min = mid + 1.继续下次循环查找
​	7，当 min > max 时，表示要查找的元素在数组中不存在，返回-1.

二分查找核心:

​	1.被查找的数据一定要排好序
​	2.查找过程中每次都会删除一半的可能

## 3.冒泡排序

将一组数据按照固定的规则进行排列
相邻的数据两两比较，小的放前面，大的放后面。
如果有n个数据进行排序，总共需要比较n-1次
每一次比较完毕,都会将最大值排到最后一个索引,下一次的比较就会少一个数据参与

```java
for (int i = 0; i < arr.length - 1; i++) { //比较的轮数
    for (int j = 0; j < arr.length - 1 - i; j++) { //每轮比较的次数
        if (arr[j] < arr[j + 1]) { // >:从小到大   <:从大到小
            int temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
```

## 4.Arrays

**1.public static String toString (int[] arr)**

 	Arrays.toString (arr): 返回指定数组的内容的字符串表现形式

**2.public static void sort (int[] arr)**

 	Arrays.sort (arr): 按照数字排序排列指定的数组

**3.public static int binarySearch (int[] arr,int key)**

​	Arrays.binarySearch (arr,key): 利用二分查找返回指定元素的索引
​	如果key在arr中存在,返回key在arr中的索引
​	如果key在arr中不存在,返回负的插入索引-1

# 2.异常

## 1.异常发生的本质

​	哪里发生了异常,底层其实就是在哪里创建了异常对象
​	异常对象创建后会扫描当前语法是否有对其处理的逻辑
​	如果我们开发者没有对其处理,异常就会交给方法的调用者处理
​	main方法的调用者是JVM

## 2.JVM是怎么处理异常的?

​	a: 将异常对象的详细信息打印到控制台   -- 通报批评
​	b: 哪里发生异常,程序就在哪里停止!     -- 罢工

## 3.处理异常

​    a:抛出异常
​        注意:抛出异常本质上并没有真正解决问题,只是声明问题跟我当前方法无关,谁调用我,谁负责								处理该问题
​        作用:能够让编译时异常快速通过语法编译,继而运行程序

​    b:正常处理
​        try{}:大括号写有可能出现异常的代码
​        catch():小括号中定义异常变量
​        catch{}:大括号中写的就是捕获到异常后的处理逻辑

```java
1.抛出异常
	public static void method() throws ParseException {}
2.try catch处理
	try{
		有可能出现异常的代码
	}catch(异常变量 a){
		捕获到异常后的处理逻辑
		a.printStackTrace(); //打印异常类和异常位置
	}
```

1.如果 try 中没有遇到问题，怎么执行？
​	会把try中所有的代码全部执行完毕,不会执行catch里面的代码
2.如果 try 中遇到了问题，那么 try 下面的代码还会执行吗？
​	那么直接跳转到对应的catch语句中,try下面的代码就不会再执行了
​	当catch里面的语句全部执行完毕,表示整个体系全部执行完全,继续执行下面的代码
3.如果出现的问题没有被捕获，那么程序如何运行？
​	那么try...catch就相当于没有写.那么也就是自己没有处理,默认交给虚拟机处理
4.同时有可能出现多个异常怎么处理？
​	出现多个异常,那么就写多个catch就可以了.
​	注意点:如果多个异常之间存在子父类关系.那么父类一定要写在下面
5.打印异常信息到控制台的方式:
​	public String getMessage ()   	 	返回此 throwable 的详细消息字符串
​	public String toString ()     	 		返回此可抛出的简短描述
​	public void printStackTrace ()	 	 把异常的错误信息输出在控制台(字体为红色的)

## 4.自定义异常

自定义异常存在的意义：就是为了让控制台的报错信息更加的见名之意。

用法:声明一个类继承RuntimeException或Exception,写出空参无参构造

```java
public class AgeOutOfBoundsException extends RuntimeException{ 
	public AgeOutOfBoundsException() { 
	} 
	public AgeOutOfBoundsException(String message) { 
		super(message); 
	} 
}
```

# 3.递归

​	1.概述:指方法定义中调用方法本身的现象

​	2.思路:把一个 复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解,只需少量的程序就可描述出解题过程所需要的多次重复计算

​	3.要求:需要**递归的出口**和**递归的规律**

