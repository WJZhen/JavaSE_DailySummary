# 一.HashSet

## 1.概述和特点

​	①底层数据结构是**哈希表**
​	②对集合的迭代顺序不作任何保证，存取顺序可能**不一致**
​	③**没有带索引**的方法，所以不能使用普通for循环遍历
​	④由于是Set集合，所以元素**唯一**

## 2.哈希值

**2.1概述:**

​	①JDK根据对象的**地址**或者**属性值**算出来的int类型的**十进制整数**
​	②通过Object中的hashCode方法根据对象的**地址值**得出哈希值
​	③通过子类重写hashCode方法根据对象的**属性值**得出哈希值

**2.2 特点**

​	①同一个对象多次调用hashCode()方法返回的哈希值是相同的
​	②默认情况下，不同对象的哈希值是不同的。而重写hashCode()方法，可以实现让不同对象的哈希值相同

## 3.哈希表

**3.1 JDK1.8之前:数组+链表**

​	①创建一个默认长度16,默认加载因为0.75的数组,数组名table
​	②根据元素的哈希值跟数组的长度计算出应存入的位置
​	③判断当前位置是否为null,如果是null直接存入
​	④如果位置不为null,表示有元素,则逐个比较哈希值
​		如果不同,老元素挂在新元素下面形成**哈希桶(链表)**结构
​		如果相同,产生**哈希碰撞(哈希冲突)**,触发equals比较机制
​	⑤根据equals比较返回结果
​		如果为false,则判断为非重复元素,存入哈希表
​		如果为true,则为重复元素,不存入哈希表

​	**因此,凡是重写equals(),必须重写hashCode() !!!**

**3.2 JDK1.8及之后:数组+链表+红黑树**

​	存储流程不变。
​	当数组长度>=64时,且链表长度>8的时候，自动转换为红黑树。
​	否则只会将数组扩容,分散链表压力,不会直接转红黑树

**3.3 哈希表扩容机制**

​	1.满足加载因子0.75,当数组中添加的**元素个数**>数组长度*0.75,就会触发数组扩容
​	2.当链表长度>8时,且数组长度<64时,触发扩容
​	3.当红黑树的节点被删除到<=6的时.会重新降级为链表结构
​	扩容系数: 每次数组长度*2

**3.4 数学理论支撑:泊松分布**



# 二.Map

**Map集合概述:**

​	①Interface Map K：键的数据类型；V：值的数据类型
​	②键不能重复，值可以重复(**键相同,值覆盖**)
​	③键和值是一一对应的，每一个键只能找到自己对应的值
​	④(键 + 值)称之为“键值对”或“键值对对象”,Java中叫做“Entry对象”。

**创建Map集合对象:**

​	①多态的方式
​	②具体的实现类HashMap

**Map基本功能:**

```java
V put(K key,V value)//添加元素
V remove(Object key)//根据键删除键值对元素
void clear()//移除所有的键值对元素
boolean containsKey(Object key)//判断集合是否包含指定的键
boolean containsValue(Object value)//判断集合是否包含指定的值
boolean isEmpty()//判断集合是否为空
int size()//集合的长度，也就是集合中键值对的个数
```

**三种遍历:**

```java
//第一种
//Set<K> keySet()	获取所有键的集合
//V get(Object key)	根据键获取值
Set<String> set = map.keySet();
	for (String key : set) {
    String value = map.get(key);
    System.out.println(key + "=" + value);
}
//第二种
//Set<Map.Entry<K,V>> entrySet() 获取所有键值对对象的集合
//K getKey() 获得键
//V getValue() 获得值
Set<Map.Entry<String, String>> entries = map.entrySet();
	for (Map.Entry<String, String> entry : entries) {
	String key = entry.getKey();
	String value = entry.getValue();
	System.out.println(key+"---"+value);
}
//第三种
//forEach和lambda表达式
map.forEach(
  (key,value)->System.out.println(key+"---"+value)
);
```

## 1.HashMap

​	①HashMap是Map里面的一个实现类。
​	②方法与Map相同
​	③HashMap跟HashSet一样底层是哈希表结构的
​	④依赖hashCode方法和equals方法保证**键**的唯一
​	⑤如果**键**存储自定义对象,需要重写hashCode和equals方法

## 2..TreeMap

​	①TreeMap是Map里面的一个实现类。
​	②方法与Map相同
​	③TreeMap跟TreeSet一样底层是红黑树结构的
​	④依赖自然排序或者比较器排序，对**键**进行排序
​	⑤如果**键**存储自定义对象，需要进行自然排序或比较器排序



# 三.可变参数

**可变参数：**就是形参的个数是可以变化的
​	格式：修饰符 返回值类型 方法名(数据类型… 变量名) { }
​	范例：public static int sum(int… a) { }
**可变参数注意事项:**
​	①这里的变量其实是一个数组
​	②一个方法,最多只能定义一个可变参数
​	③如果定义可变参,可变参数必须放在方法形参的末尾



# 四.不可变集合

在List、Set、Map接口中，都存在of方法，可以创建一个不可变的集合。
​	①这个集合不能添加，不能删除，不能修改。
​	②但是可以结合集合的带参构造，实现集合的批量添加。
​	③在Map接口中，还有一个ofEntries方法可以提高代码的阅读性。
​	④首先会把键值对封装成一个Entry对象，再把这个Entry对象添加到集合当中

```Java
static  List of(E…elements) //创建一个具有指定元素的List集合对象
static  Set of(E…elements) //创建一个具有指定元素的Set集合对象
static  Map of(E…elements) //创建一个具有指定元素的Map集合对象
```

