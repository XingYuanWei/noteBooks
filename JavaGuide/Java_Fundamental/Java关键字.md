# Java关键字

## 访问控制
```java
		 private
		 protected
		 public
```
>	类、接口、抽象类实现接口
>```java
>		class
>		abstract  
>		extends 
>		implements
>		interface 
>		new 
>```		
##### abstract：
>    声明一个抽象方法，该方法只是一个声明而没有设计方法体，那么该方法没有任何功能，不需要大括号，括号后直接分号结束。如果一个非抽象子类继承了这个抽象方法，那么则必须出现这个abstract方法。当然如果继续把这子类设为抽象类，那么则不用实现这个abstract方法。  
>	abstract**不能**与 synchronized，strictfp，native，private，final，static组合。前三个是描述关于方法设计方面的修饰符，**private和final不允许子类继承，不允许被复写**，所以必然是不能同时使用的。不能修饰成员变量。**抽象类不能有实例对象。**


## 修饰方法、类、属性和变量

 ```java
    native 
	final 
	static 
	strictfp
    synchronized 
	transient 
```
	
##### volatile:
>    只能应用于实例变量，其他详见章节目录volatile关键字

##### static:
>**能用static修饰的有：**
     *类中方法，变量，顶级嵌套类*

>**不能用static修饰的有：**
				*构造函数，类，接口，内部类，内部类方法和内部类实例变量，局部变量*

##### final:
> final关键字声明变量将使该变量一旦被一个显式值初始化之后就不可能再重新初始化，对于原始类型，一旦变量赋值之后，该值就不能修改。如果对于对象引用用final修饰，那么表示该引用不能指向其他对象，但是可以更改这个对象引用里实例变量的值。
		
##### strictfp:
>strictfp 关键字可应用于类、接口或方法。使用 strictfp 关键字声明一个方法时，该方法中所有的float和double表达式都严格遵守FP-strict的限制,符合IEEE-754规范。当对一个类或接口使用 strictfp 关键字时，该类中的所有代码，包括嵌套类型中的初始设定值和代码，都将严格地进行计算。严格约束意味着所有表达式的结果都必须是 IEEE 754 算法对操作数预期的结果，以单精度和双精度格式表示。另外即使strictfp不用作类修饰符也能把方法用strictfp修饰。**不能修饰成员变量。**

##### transient:
>串行化某个对象时，如果该对象的某个变量是transient，那么这个变量不会被串行化进去。如果一个变量被transient所修饰，那么当该变量被ObjectOutputStream把这个类的某个实例保存在磁盘的时候被transient修饰的变量是不会被保存的。当从磁盘中读出某个类的实例时，实际上并不会执行这个类的构造函数，而是读取这个类的实例的状态，并且把这个状态付给这个类的对象。**可以修饰成员变量。不能修饰方法。**




