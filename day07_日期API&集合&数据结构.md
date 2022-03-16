# 1.API

## 1.1 Date

​	 **1.1 Date介绍:**
​		1.Date是Java提供的用来描述日期时间的一个类
​		2.在程序的世界中,时间原点:1970年1月1日 0点0分0秒
​		3.中国所在地理位置:东八区  ---和世界标准时间有8个小时时差

​	**1.2 构造方法:**

​		无参: 创建一个日期对象,表示当前系统时间 
```
		Date d1 = new Date();
		System.out.println("d1 = " + d1);
```
​		 带参: 创建一个日期对象,表示在时间原点基础上加上给定的毫秒值,表示一个指定时间
```java
		Date d2 = new Date(0L);
		System.out.println("d2 = " + d2);
```

​	**1.3 成员方法:**

​		1.getTime():获取当前日期对象所对应的毫秒值
​		2.setTime():设置当前日期对象所对应的毫秒值

```java
		Date d1 = new Date();
		long time1 = d1.getTime();
		System.out.println("time1 = " + time1);

		long time2 = System.currentTimeMillis();
		System.out.println("time2 = " + time2);
    
		d1.setTime(0L);//重置当前时间到时间原点
		System.out.println("d1 = " + d1);
```

## 1.2 SimpleDateFormat

​	**2.1 构造方法:**

​		无参: 创建一个默认的日期格式

```java
	SimpleDateFormat sdf = new SimpleDateFormat();
```

​		带参:创建一个指定的日期格式

```java
	SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒");
```

​	**2.2 成员方法:**    

​		1.将日期对象格式化成指定的日期字符串  --format()  

```java
	Date d1 = new Date();
	SimpleDateFormat sdf = new SimpleDateFormat();
	String format = sdf.format(d1);
	System.out.println("format = " + format);
	SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss");
	String format = sdf.format(d1);
	System.out.println("时间: " + format);
```

​	2.将日期字符串解析为对应的日期对象  --parse()

```java
	String birthday = "1999-11-11";
	//注意: 解析必须保证模板和被解析的字符串格式严格匹配
	SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
	Date date = sdf.parse(birthday);//这里需要抛出异常
	System.out.println("date = " + date);
```

## 1.3.Calendar

​	**3.1 用途:** 主要提供关于日期的精确运算

```java
	//抽象类多态, 默认创建的日历指向当前系统时间
	Calendar c = Calendar.getInstance();
```

​	**3.2 注意:**
​		1.在Calendar中月份从0开始,范围是**[0,11]**
​		2.在Calendar中星期从星期日(1)开始,周六(7)是一周的结束

​	**3.3 常用方法:**
​		**1.get();** 获取指定的日历字段信息

```java
    //获取当前日历中的年份
    int year = c.get(Calendar.YEAR);
    System.out.println("year = " + year);
    //获取月份
    int month = c.get(Calendar.MONTH);
    System.out.println("month = " + (month+1));
    //获取日
    int day = c.get(Calendar.DATE);
    System.out.println("day = " + day);
    //获取今天是一年中的第几天
    int dayOfYear = c.get(Calendar.DAY_OF_YEAR);
    System.out.println("dayOfYear = " + dayOfYear);
    //获取今天是星期几
    int week = c.get(Calendar.DAY_OF_WEEK);
    System.out.println("week = " + (week-1));
```

​		**2.set();** 设置日历

```java
	//将日历快速定位到2008年8月8日
	c.set(2008, 7, 8);
    System.out.println("year = " + c.get(Calendar.YEAR));
    System.out.println("month = " + (c.get(Calendar.MONTH)+1));
    System.out.println("day = " +c.get(Calendar.DATE));
```

​		**3.add();** 实现日历的动态计算

```java
	//注意:add方法将指定日历字段进行精确运算
	//正数:时间往后移  负数:时间往前移
	//需求:将当前的时间往前推56天,并计算得到一个新的日历
	Calendar c1 = Calendar.getInstance();
	c1.add(Calendar.DATE, - 56);
	System.out.println("year = " + c1.get(Calendar.YEAR));
	System.out.println("month = " + (c1.get(Calendar.MONTH)+1));
	System.out.println("day = " +c1.get(Calendar.DATE));
```



# 2.集合

## 2.1 Collection接口

​	**1.1 注意事项:** 

​		1.接口不能直接new,需要new接口的实现类,如Arraylist

​		2.Collection没有索引,索引是list的特有属性

​	**1.2 常用方法:**

```java
    boolean add (E e) : 添加元素。
    boolean contains (Object o): 如果此集合包含指定的元素，则返回 true 。
    boolean isEmpty () : 判断集合是否为空，为空则返回 true 。
    boolean remove (Object o) : 根据元素本身删除集合中对应的内容。
    int size (): 返回此集合中的元素个数。
    boolean removeIf(Object o): 根据条件删除集合中的元素//可以用Lambda表达式
    void clear(): 清空集合中的元素
```

## 2.2 Iterator迭代器

​	**2.1 创建方法:**

​		Iterator<E> iterator()：创建迭代器对象，默认指向当前集合的0索引。

```java
		Collection<String> list = new ArrayList<>();
		Iterator<String> it = list.iterator();
```

​	**2.2 成员方法:**

​		1.boolean hasNext()：判断当前位置是否有元素可以被取出

​		2.E next()：获取当前位置的元素,将迭代器对象移向下一个索引位置

​		3.E remove()：删除此迭代器返回的最后一个元素

```java
		while (it.hasNext()) {//判断是否有元素
          System.out.println(it.next());//打印当前位置元素
          it.remove();//删除上面next取出的元素
        }
```

## 2.3 增强for循环

​	**3.1 概述**：

​		1.简化数组和Collection集合的遍历
​		2.它是JDK5之后出现的，其内部原理是一个Iterator迭代器
​		3.实现Iterable接口的类才可以使用迭代器和增强for

​	**3.2 格式：**	

```java
		for(String s : list) {//元素数据类型 变量名 : 数组或者Collection集合
			System.out.println(s)//在此处使用变量即可，该变量就是元素
		}
```

​		idea快捷键:	iter		list.for		list.iter

​	**3.3 四种循环的使用场景：**
​		1.如果需要操作索引，使用普通for循环
​		2.如果在遍历的过程中需要删除元素，请使用迭代器
​		3.如果仅仅想遍历，那么使用增强for
​		4.forEach可以使用lambda表达式



# 3.数据结构

​	**概述：**数据结构是计算机存储、组织数据的方式。是指相互之间存在一种或多种特定关系的数据元素的集合通常情况下，精心选择的数据结构可以带来更高的运行或者存储效率

## 3.1 栈

​	数据进入栈模型的过程为：压/进栈
​	数据离开栈模型的过程称为：弹/出栈
​	栈是一种数据**先进后出**的模型

## 3.2 队列

​	数据从**后端**进入队列模型的过程称为：入队列
​	数据从**前端**离开队列模型的过程称为：出队列
​	队列是一种数据**先进先出**的模型

## 3.3 数组

​	数组是一种**查询快，增删慢**的模型
​	查询数据通过地址值和索引定位，查询任意数据耗时相同，查询速度快
​	删除数据时，要将原始数据删除，同时后面每个数据前移，删除效率低
​	添加数据时，添加位置后的每个数据后移，再添加元素，添加效率极低

## 3.4 链表

​	链表是一种**增删快，查询慢**的模型(对比数组）
​	添加B数据时，将A对应的下一个数据地址指向B，将B对应的下一个数据地址指向C，添加速度快
​	删除数据时，将A对应的下一个数据地址指向C，然后删除B，删除速度快
​	查询数据D是否存在，必须从头(head)开始查询，查询速度慢
​	***java中都是双向链表,可以双向查询**



# 4.List

​	**1. 概述:**	

​		1.有序集合，这里的有序指的是存取顺序
​		2.用户可以精确控制列表中每个元素的插入位置。
​		3.用户可以通过整数索引访问元素，并搜索列表中的元素

​	**2. 特点:**	

​		1.**允许重复：**Set集合不同，列表通常允许重复的元素
​		2.**存取有序**：存储和取出的元素顺序一致
​		3.**有索引**：可以通过索引操作元素
​		4.**可重复**：存储的元素可以重复

​	**3. 成员方法:**		

```java
		void add(int index,E element)// 在此集合中的指定位置插入指定的元素
		E remove(int index)// 删除指定索引处的元素，返回被删除的元素
		E remove(E element)// 删除指定元素,返回boolean类型的结果 
		E set(int index,E element)// 修改指定索引处的元素，返回被修改的元素
		E get(int index)// 返回指定索引处的元素
```

​	**4. List集合常用实现类:**
​		List集合常用子类：ArrayList，LinkedList
​		ArrayList：底层数据结构是数组，查询快，增删慢
​		LinkedList：底层数据结构是链表，查询慢，增删快

## 4.1 LinkedList

​	**特有方法:**

```java
	public void addFirst(E e)// 在该列表开头插入指定的元素
	public void addLast(E e)// 将指定的元素追加到此列表的末尾
	public E getFirst()// 返回此列表中的第一个元素
	public E getLast()// 返回此列表中的最后一个元素
	public E removeFirst()// 从此列表中删除并返回第一个元素
	public E removeLast()// 从此列表中删除并返回最后一个元素	
```

## 4.2 ArrayList

​	**底层源码总结:**

​		1.通过无参构造创建的ArrayList集合容器,初始容量是0

​		2.当第一次添加元素后, 集合容器会自动扩容到10

​		3.ArrayList集合底层的扩容,每次都是将集合容量 * 1.5倍