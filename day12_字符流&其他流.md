# 一.字符流

> 因为字节流一次读一个字节，而不管GBK还是UTF-8一个中文都是多个字节，用字节流每次只能读其中的一部分，所以就会出现乱码问题。

## **1.读取中文的过程**

1.1 想要进行拷贝，一律使用字节流或者字节缓冲流
1.2 想要把文件中的数据读到内存中打印或者读到内存中运算，请使用字符输入流。想要把集合，数组，键盘录入等数据写到文件中，请使用字符输出流
1.3 GBK码表一个中文两个字节，UTF-8编码格式一个中文3个字节。

## **2.字符流写数据**

2.1 创建字符输出流对象。

```Java
new FileWrite(new File());
new FileWrite(String filePath);  ★★★
```

​	如果文件不存在，就创建。但是要保证父级路径存在。如果文件存在就清空。

2.2 写数据

```Java
void write(int c)//写一个字符
void write(char[] cbuf)//写入一个字符数组
void write(char[] cbuf, int off, int len)//写入字符数组的一部分 
void write(String str)//写一个字符串  ★★★
void write(String str, int off, int len)//写一个字符串的一部分
```

​	①写出int类型的整数，实际写出的是整数在码表上对应的字母。
​	②写出字符串数据，是把字符串本身原样写出。

2.3 释放资源

​	每次使用完流必须要释放资源(close)

```Java
flush() //刷新流，还可以继续写数据
close() //关闭流，释放资源，但是在关闭之前会先刷新流。一旦关闭，就不能再写数据
```

## **3.字符流读数据**

3.1创建字符输入流对象

```java
new FileReader(File file);
new FileReader(String filePath); ★
```

3.2读数据

```java
int read() //一次读一个字符数据
int read(char[] cbuf) //一次读一个字符数组数据
```

3.3释放资源

​	每次使用完流必须要释放资源(close)

## **4.字符缓冲流**

4.1字符缓冲流
​	BufferedWriter：缓冲输出流
​	BufferedReader：缓冲输入流
4.2构造方法：
​	BufferedWriter(Writer out):字符缓冲输出流
​	BufferedReader(Reader in):字符缓冲输入流
4.3成员方法:
​	BufferedWriter：
​	void newLine()：写一行行分隔符，行分隔符字符串由系统属性定义
​	BufferedReader：
​	public String readLine() ：读一行文字。 结果包含行的内容的字符串，不包括任何行终止字符，如果流
的结尾已经到达，则为null 

# 二.转换流

> 转换流就是来进行字节流和字符流之间转换的,InputStreamReader是从字节流到字符流的桥梁,OutputStreamWriter是从字符流到字节流的桥梁

**创建转换流对象**

```java
InputStreamReader(InputStream in,String charset)
InputStreamWriter(OutStream in,String charset)
//使用指定编码创建对象,不写charset则为默认编码
```

# 三.对象操作流

> 可以把对象以字节的形式写到本地文件，直接打开文件是读不懂的，需要再次用对象操作流读到内存中

**1.应用:**

​	①对象网络传输
​	②保存对象到文件/读取文件

**2.分类:**

```java
ObjectOutputStream(OutputStream out)// 对象输出流, 将对象写到本地文件中, 或者在网络中传输对象
ObjectInputStream(InputStream int)// 对象输入流, 从本地文件读取对象, 或者接收网络中传输的对象
```

**3.使用对象转换流写数据**

​	①创建User对象
​	②创建对象转换流
​	③写出数据  void writeObject(Object obj);
​	④释放资源
 	注意: 对象要保存到文件中, 需要实现Serializable接口

**4.使用对象转换流读数据**

​	①创建对象转换流
​	③读取数据  Object readObject();
​	③释放资源

**5.注意事项:**

​	5.1 用对象序列化流序列化一个对象后,修改了对象所属的类文件, 读取数据会抛出InvalidClassException异常
​	5.2 如果出现问题了,如何解决问题?
​		①重新序列化
​		②给对象所属的类, 添加一个 serialVersionUID private static final long serialVersionUID = 42L;
​	5.2 如果对象中的某个成员变量不想被序列化, 给该成员变量加transient关键字修饰，该关键字标记的成员变量不参与序列化过程
