## 1.包的语法

包的定义:package com.itheima.包的语法.test1;

1.同一个包下,两个类之间访问:

​                    直接通过类名访问即可,无需导包.

2.不同包下,两个类之间访问:

​          1.导包访问 import
​           2.通过全类名访问 全类名: 包名+类名
​           应用场景:用于区分多个包下同名类的访问.

## 2.static:静态修饰符

1.被static修饰的成员属于类,被该类所有对象共享使用
​    结论:1.先加载静态区,再加载非静态区.
​             2.非静态区的成员由堆内存分配默认值 

2.被static修饰的成员可以直接通过类名调用(类名.静态成员)

3.静态方法只能访问类的静态成员,不能直接访问类的非静态成员.

​   非静态方法既可以访问类的静态成员,也可以访问非静态成员.
​    (注意:如果要在静态方法中访问非静态成员,必须创建对象,通过对象访问)

​ 4.静态方法中,不允许出现:this,super这两种关键字.