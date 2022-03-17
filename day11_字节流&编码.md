# 一.IO流

**概述:**
​	I表示intput，是数据从硬盘进内存的过程，称之为读。
​	O表示output，是数据从内存到硬盘的过程。称之为写。
**分类:**
​	①按流向分输入流和输出流
​	②按数据类型分字符流和字节流
​		字节流操作所有类型的文件
​		字符流只能操作纯文本文件
​	 一般来说，IO流的分类是按照**数据类型**来分的

## 1.字节流

**1.1写数据的步骤：**

① 创建字节输出流对象
```java
new FileOutputStream(String filePath); ★★★
new FileOutputStream(File file);
//如果文件不存在，就创建。如果文件存在就清空。
```
② 写数据
​	写出的整数，实际写出的是整数在码表上对应的字母。
③ 释放资源
​	每次使用完流必须要释放资源(close)。

**1.2写数据的方式：**

```java
void write(int b)//一次写一个字节数据
void write(byte[] b)//一次写一个字节数组数据
void write(byte[] b, int off, int len)//一次写一个字节数组的部分数据
```

①写完数据后加换行符:
​	windows:\r\n		linux:\n			mac:\r
②写完数据后追加写入:

```java
new FileOutputStream(String filePath，boolean 参数); ★★★
new FileOutputStream(File file boolean 参数);
//创建文件输出流写入文件。如果参数为true，不会清空文件里面的内容   
```

**1.3异常处理**

**finally**：在异常处理时提供finally块来执行所有清除操作。比如说IO流中的释放资源
特点：被finally控制的语句一定会执行，除非JVM退出
异常处理标准格式：**try….catch…finally**

**1.4读数据的步骤**

① 创建字节输入流对象。

```Java
new FileInputStream(String filePath); ★★★
new FileInputStream(File file boolean 参数);
//如果文件不存在，就直接报错。
```

② 读数据

```java
int b = read();
//读出来的是文件中数据的码表值。b=-1表示没有数据
int read(byte[] b);
//返回读入缓冲区的字节总数，如果因为已经到达文件末尾而没有更多的数据，则返回 -1。  
```

③ 释放资源
​	每次使用完流必须要释放资源(close)。

**1.5文件复制**

把文件的内容从一个文件中**读取**出来(数据源)，然后**写入**到另一个文件中(目的地)
​	数据源 --- 读数据 --- FileInputStream
​	目的地 --- 写数据 --- FileOutputStream
​	***后开启的流先释放**

第三方工具类:
(common-io)	**IOUtils.copy**(数据,目的地)

## 2.字节流缓冲流

2.1字节缓冲流：
​	BufferOutputStream：缓冲输出流
​	BufferedInputStream：缓冲输入流
2.2构造方法：
​	字节缓冲输出流：			
​	BufferedOutputStream(OutputStream out)
​	字节缓冲输入流：
​	BufferedInputStream(InputStream in)
​	字节缓冲流仅仅提供缓冲区，而真正的读写数据还得依靠基本的字节流对象进行操作

## 3.字符流

**3.1编码表：**
①计算机中储存的信息都是用二进制数表示的；我们在屏幕上看到的英文、汉字等字符是二进制数转换之后的结果
②按照某种规则，将字符存储到计算机中，称为编码。
③按照同样的规则，将存储在计算机中的二进制数解析显示出来，称为解码 。
④编码和解码的方式必须一致，否则会导致乱码。
ASCII(无中文),GBK(中文两个字节),Unicode(UTF-8中文三个字节)...

**3.2解决编码问题**

```java
//编码：
byte[] getBytes()//使用平台的默认字符集将该 String编码为一系列字节，将结果存储到新的字节数组中
byte[] getBytes(String charsetName)//使用指定的字符集将该String编码为一系列字节，将结果存储到新的字节数组中
//解码：
String(byte[] bytes)//通过使用平台的默认字符集解码指定的字节数组来构造新的 String
String(byte[] bytes, String charsetName)//通过指定的字符集解码指定的字节数组来构造新的 String
```

