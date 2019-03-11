# java基础
## 1.String的常见方法:
  * （1）length()、charAt()、substring()、equals()、compareTo、indexOf()、toLowerCase()、toUpperCase()、replace()
  * （2）+ 、concat()、apend()都可用来拼接字符串

## 2.java中String、StringBuffer、StringBuilder的区别
  * （1）String的值是不可变得。
    原因：String类中使用字符数组保存字符串，因为有“final”修饰符，所以可以知道string对象是不可变的。private final char value[];
  * （2）StringBuffer、StringBuilder的值是可变的
    原因：StringBuilder与StringBuffer都继承自AbstractStringBuilder类，在AbstractStringBuilder中也是使用字符数组保存字符串。char[] value;
    这样会导致每次对String的操作都会生成新对象，效率低下，浪费内存。包括String类的字符串拼接也是创造新对象。
  * （3）String因为不可变，所以线程安全。
    StringBuffer对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。
    StringBuilder并没有对方法进行加同步锁，所以是非线程安全的。
  * （4）StringBuilder与StringBuffer共同点
    StringBuilder与StringBuffer有公共父类AbstractStringBuilder(抽象类)。
  * （5）初始值时，String可以赋空值，其余两者不可
	 小结：（1）如果要操作少量的数据用 String；
               （2）多线程操作字符串缓冲区下操作大量数据 StringBuffer；
               （3）单线程操作字符串缓冲区下操作大量数据 StringBuilder（推荐使用）。
		
## 3.接口和抽象类的区别
  * 相同点：（1）二者都是抽象类，都不能实例化。
	   （2）接口的实现类和抽象类的子类都必须要实现已经声明的抽象方法。
  * 不同点：（1）接口被实现，抽象类被继承
           （2）一个类可以实现多个接口，但一个类只能继承一个抽象类
	   （3）interface实现类及abstrct class的子类都必须要实现相应的抽象方法，但实现的形式不同。
                interface中的每一个方法都是抽象方法，都只是声明的(declaration,没有方法体)，实现类必须要实
                 现。而abstractclass的子类可以有选择地实现。

## 4.多线程的实现方式、同步的实现方式
  * 多线程的实现方式：（1）继承Thread类（2）实现Runnable接口
  * 同步的实现方式:（1）在返回类型上加synchronized（2）使用wait()、notify();
				   
## 5.==和equals的区别
  * （1）== 作用于基本数据类型变量，比较值，
        作用于引用类型变量，比较对象的内存地址
  * （2）equals() 若重写了equals()方法，比较的是引用类型的变量所指向的对象的地址;
                 没重写，则比较的是值
				 
## 6.页面跳转方式（（转发）forward与（重定向）redirect的区别）
 * （1）forward   URL不变  redirect改变
 * （2）forward转发页面和转发到的页面可以共享request里面的数据。redirect不能共享数据。
 * （3）forward只能在同一个Web应用程序内的资源之间转发请求。redirect可以重定向到同一站点的不同程序上，甚至重定向到其他站点。
   
## 7.八大基本类型
     short,long,flaot,double,byte,char,int,boolean
	 
## 8.基本类型和包装类型的区别
  * （1）基本类型只有值，而引用类型不止有值，还有同一性，同一性指两个引用是否指向同一个对象，也就是两个值的地址是否相同。
	      也就是说基本类型是值传递，包装类型是引用传递。
		  
  * （2）声明方式不同，基本类型不需要new关键字，包装类型需要在堆内存中用new来分配内存空间
	 
  * （3）存储位置不同，基本类型存储在栈中，包装类型存储在堆中，通过对象引用
	 
  * （4）初始值不同，基本类型初始值如int是0，boolean是false。而包装类型的初始值时null。
	 
  * （5）使用方式不同，基本类型直接赋值使用，包装类型一般在集合如List Map时会使用

  * （6）包装类型是对象，拥有方法和字段，对象的调用是引用对象的地址。
	 
  * （7）基本数据类型传值，对形参的修改不会影响实参；引用类型传引用，形参和实参指向同一个内存地址（同一个对象），所以对参数的修改会影响到实际的对象；
	 
## 8.java是引用传递和值传递？
     java是值传递，然而我们经常看到对于对象（数组，类，接口）的传递似乎有点像引用传递，可以改变对象中某个属性的值。但是不要被这个假象所蒙蔽，
	 实际上这个传入函数的值是对象引用的拷贝，即传递的是引用的地址值，所以还是按值传递。
	 
	 Java中只有按值传递。不管是基本类型还是引用类型，形参都是实参的一个拷贝。对形参的修改不会影响到实参。形参只是实参的一个拷贝，是两个不同的东西。
	 但是因为形参和实参的值相同，都指向同一个对象，所以对形参所指向的对象的修改会影响到实参所指向的对象。
