## 1.内部类

### 1.3 局部内部类

- 局部内部类定义位置

  - 局部内部类是在方法中定义的类

- 局部内部类方式方式

  - 局部内部类，外界是无法直接使用，需要在方法内部创建对象并使用
  - 该类可以直接访问外部类的成员，也可以访问方法内的局部变量

### 1.4 匿名内部类

- 匿名内部类的前提：存在一个类或者接口

- 匿名内部类的格式：new 类名 ( ) {  重写方法 }    new  接口名 ( ) { 重写方法 }

  ```java
  new Inter(){
      @Override
      public void method(){}
  } 
  ```

- 匿名内部类的本质：是一个继承了该类或者实现了该接口的子类匿名对象

- 匿名内部类直接调用方法

  ```java
  interface Inter{
      void method();
  }

  class Test{
      public static void main(String[] args){
          new Inter(){//也可以通过多态的形式接收:(Inter i = new Inter(){)
              @Override
              public void method(){
                  System.out.println("我是匿名内部类");
              }
          }.method();	// 直接调用方法
      }
  }
  ```

## 2.Lambda

### 2.1表达式

​	1.Lambda使用前提:  存在函数式接口!
​		 a. 必须要有一个接口
​		 b. 接口中必须有且仅有一个抽象方法!

​	2.Lambda格式解析:(形式参数) -> {代码块}
​		(): 和接口中的抽象方法的形参保持一致!
​		-> : 固定格式,代表指向动作
​		{}: 实现类对象的重写逻辑

### 2.2省略规则
​	1.参数类型可以省略，但是有多个参数的情况下，不能只省略一个
​	2.如果参数有且仅有一个，那么小括号可以省略
​	3.如果代码块的语句只有一条，可以省略大括号和分号，甚至是return	

### 2.3和匿名内部类的区别
​	1.所需类型不同
​		匿名内部类：可以是接口，也可以是抽象类，还可以是具体类
​		Lambda表达式：只能是接口

​	2.使用限制不同
​		如果接口中有且仅有一个抽象方法，则Lambda表达式和匿名内部类都可以使用
​		如果接口中多于一个抽象方法，只能使用匿名内部类，而不能使用Lambda表达式

​	3.实现原理不同
​		匿名内部类：编译之后，产生一个单独的.class字节码文件
​		Lambda表达式：编译之后，没有一个单独的.class字节码文件。对应的字节码会
​		在运行的时候动态生成

## 3.API

### 1.Math
​	Math.abs(int a)					返回参数的绝对值
​	Math.ceil(double a)				向上取整
​	Math.floor(double a)				向下取整
​	Math.round(float a)				四舍五入
​	Math.max(int a,int b)				返回两个int值中的较大值
​	Math.min(int a,int b)				返回两个int值中的较小值
​	Math.pow(double a,double b)			返回a的b次幂的值
​	Math.random()					返回值为double的正值，[0.0,1.0)

### 2.System
​	System.exit(int status)				终止当前运行的 Java 虚拟机，非零表示异常终止
​	System.currentTimeMillis() 		返回当前时间(以毫秒为单位)
​	System.arraycopy(数据源数组, 起始索引, 目的地数组, 起始索引, 拷贝个数)		数组copy

### 3.Object

​	1.toString :	打印一个对象,其实就是在打印该对象的调用toString()的返回值.
​		重写前:在Object中返回对象的地址值;
​		重写后:返回值是属性值!

​	2.equals :	
​		重写前:在Object中默认逻辑是比较双方地址值.
​		重写后:是比较双方属性值

### 4.Objects

​	**没用的工具类,略过**

### 5.BigDecimal

​	//如果想要进行精确运算,那么请使用字符串的构造
​	public BigDecimal add(另一个BigDecimal对象) 				加法
​	public BigDecimal subtract (另一个BigDecimal对象)  			减法
​	public BigDecimal multiply (另一个BigDecimal对象)  			乘法
​	public BigDecimal divide (另一个BigDecimal对象)   			除法

​	public BigDecimal divide (另一个BigDecimal对象,精确几位,舍入模式)		除法
​	舍入模式:进一法  BigDecimal.ROUND_UP
​        		去尾法  BigDecimal.ROUND_FLOOR
​        		四舍五入 BigDecimal.ROUND_HALF_UP