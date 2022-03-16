# 一.Stream流

## 1.获取Stream流

创建一条流水线，并把数据放到流水线上准备进行操作

**1.1单列集合*:**

​	直接使用Collection接口中的默认方法stream()生成流

**1.2双列集合*:**

​	**间接**的生成流,可以先通过keySet或者entrySet获取一个Set集合，再调用stream()方法

**1.3数组:**

​	Arrays中的静态方法stream(数组名)生成流

**1.4同种数据类型的多个数据:**

​	1，2，3，4，5….		“aaa”,“bbb”,“ccc”….
​	使用Stream.of(T…values)生成流

## 2.中间方法

流水线上的操作。一次操作完毕之后，还可以**继续**进行其他操作，但不能再**重新**操作.

**常用方法:**

```java
Stream filter(Predicate predicate)：对流中的数据进行过滤
//Predicate:接口中的方法 boolean test(T t)：对给定的参数进行判断，返回一个布尔值，保留符合条件的
Stream limit(long maxSize)：截取指定参数个数的数据
Stream skip(long n)：跳过指定参数个数的数据
static Stream concat(Stream a, Stream b)：合并a和b两个流为一个流
Stream distinct()：去除流中重复的元素。依赖(hashCode和equals方法)
```

## 3.终结方法

一个Stream流只能有一个终结方法,是流水线上的最后一个操作

**常用方法:**

```java
void forEach(Consumer action)：对此流的每个元素执行操作
//Consumer接口中的方法 void accept(T t)：对给定的参数执行此操作
long count()：返回此流中的元素数
```

## 4.收集操作

在Stream流中无法直接修改集合,数组等数据源中的数据

**常用方法:**

```java
//Stream流的收集方法
R collect(Collector collector)
//工具类Collectors提供了具体的收集方式
public static <T> Collector toList()//把元素收集到List集合中
public static <T> Collector toSet()//把元素收集到Set集合中
public static Collector toMap(Function keyMapper,Function valueMapper)//把元素收集到Map集合中
```



# 二.File

## 1.File类是什么

1.1在读写数据时告诉虚拟机要操作的（文件/文件夹）在哪
1.2对（文件/文件夹）本身进行操作。包括创建，删除等。

## 2.概述和构造方法

File：它是文件和目录路径名的抽象表示
2.1文件和目录可以通过File封装成对象
2.2File封装的对象仅仅是一个路径名。它可以是存在的，也可以是不存在的。

```java
File(String pathname)//通过将给定的路径名字符串转换为抽象路径名来创建新的File实例
File(String parent, String child)//从父路径名字符串和子路径名字符串创建新的File实例
File(File parent, String child)//从父抽象路径名和子路径名字符串创建新的File实例
```

**2.3绝对路径和相对路径**

```java
//绝对路径：从盘符开始
File file1 = new File(“D:\\itheima\\a.txt”);
//相对路径：相对当前项目下的路径 
File file2 = new File(“a.txt”);//项目中
File file3 = new File(“模块名\\a.txt”);//模块中 
```

## 3.功能

**3.1创建**

```java
public boolean createNewFile()//创建一个新的空的文件
public boolean mkdir()//创建一个单级文件夹
public boolean mkdirs()//创建一个多级文件夹
```

注意事项:
​	①createNewFile不管有没有后缀名,只能创建文件;如果文件存在,那么创建失败返回false,不存在则创建成功返回true.文件所在的文件夹也必须要存在,否则会创建失败
​	②mkdir不管有没有后缀名,只能创建单级文件夹
​	③mkdirs可以创建单级或多级文件夹(用这个就**不用mkdir**了)

**3.2删除**

```java
public boolean delete()//删除由此抽象路径名表示的文件或目录
```

注意事项:
​	①delete方法直接删除不走回收站。
​	②如果删除的是一个文件，直接删除。
​	③如果删除的是一个文件夹，需要先删除文件夹中的内容，最后才能删除文件夹。

**3.3判断和获取**

```java
public boolean isDirectory()//测试此抽象路径名表示的File是否为目录(文件夹)
public boolean isFile()//测试此抽象路径名表示的File是否为文件
public boolean exists()//测试此抽象路径名表示的File是否存在
public String getAbsolutePath()//返回此抽象路径名的绝对路径名字符串
public String getPath()//将此抽象路径名转换为路径名字符串
public String getName()//返回由此抽象路径名表示的文件或目录的名称
```

**3.4高级获取**

```java
public File[] listFiles()//返回此抽象路径名表示的目录中的文件和文件夹的File对象数组(包括隐藏的)
```

listFiles方法注意事项：
​	①当调用者不存在时，返回null
​	②当调用者是一个文件时，返回null
​	③当调用者是一个空文件夹时，返回一个长度为0的数组
​	④ 当调用者是一个有内容的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回
​	⑤当调用者是一个有隐藏文件的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回，包含隐藏内容
​	⑥当调用者是一个需要权限才能进入的文件夹时，返回null