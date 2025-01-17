#设计模式

《Head First 设计模式》读书笔记。

## 观察者模式

**定义:**
观察者模式定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新


观察者模式提供了一种对象设计，让主题和观察者之间松耦合

对于观察者的一切，主题只知道观察者实现了某个接口

松耦合的设计之所以能让我们建立有弹性的OO系统，能够应对变化，是因为对象之间的互相依赖降到了最低

使用观察者模式时，可以从被观察者处push或pull数据

observable有多个观察者时，不可以依赖特定的通知顺序，observable实现采用的是继承，存在一些问题



## 装饰者模式

**定义：**

装饰者模式动态地将责任附加到对象上。若要扩展此功能，装饰者提供了比继承更有弹性的代替方案。

在程序设计中，应该允许行代码可以被扩展，而无需修改现有的代码

组合和委托可在允许时动态地加上新的行为

装饰者模式意味着一群装饰者类，这些类用来包装具体的组件

装饰者反映出被装饰的组件类型（事实上，他们具有相同的类型，都经过接口或继承实现）。

装饰者可以在被装饰者的行为前面或后面加上自己的行为，甚至将被装饰者行为整个取代掉，而达到特定的目的

可以用无数个装饰者包装一个组件

装饰者一般对组件的客户是透明的，除非客户程序依赖与组件的具体类型

装饰者会导致设计中出现许多小对象，过度使用，会让程序变的很复杂



## 工厂模式

分为：简单工厂模式，工厂模式和抽象工厂模式

简单工厂模式其实不是一种设计模式，反而比较像是一种编程习惯，但仍可以将客户程序从具体实现解耦

工厂方法用来处理对象的创建，并将这样的行为封装在子类，客户程序中关于超类的代码就和子类对象创建代码解耦类

所有工厂模式都是用来封装对象的创建，都通过减少应用程序和具体类之间的依赖促进松耦合

工厂模式方法通过让子类决定该创建的对象是什么，来达到将对象创建的过程封装的目的

工厂方法使用继承：把对象的创建委托给子类，子类实现工厂方法来创建对象

**工厂方法模式**：定义了一个创建对象的接口，但由于子类决定要实例化的类是哪一个。工厂方法让类把实例化到子类。

依赖倒置原则：要依赖抽象，不要依赖具体的类

避免OO设计中违反依赖倒置原则的指导方针：

- 变量不可以持有具体的引用
- 不要让类派生自具体类
- 不要覆盖基类中以实现的方法

**抽象工厂模式**：提供了一个接口，用于创建相关或依赖对象的家族，而不需要明确制定具体类

抽象工厂使用对象耦合：对象的创建被实现在工厂接口所暴露出来的方法中



## 单例模式

单例模式：确保一个类只有一个实例，并提供一个全局访问点

多线程下的单例模式：

- 如果`getInstance()`的性能对应用不是很关键，就什么也别做
- 使用“饿汉式”创建实例，而不用“懒汉式”实例化的做法
- 用“双重检查锁”，在`getInstance()`中减少使用同步

```java
public class Singleton {
	private volatile static Singleton uniqueInstance;
 
	private Singleton() {}
 
	public static Singleton getInstance() {
		if (uniqueInstance == null) {
			synchronized (Singleton.class) {
				if (uniqueInstance == null) {
					uniqueInstance = new Singleton();
				}
			}
		}
		return uniqueInstance;
	}
}

```

## 命令模式

封装调用

定义：将请求封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式也支持可撤销的操作。

空对象：当不想返回一个有意义的对象，可以使用空对象，将处理null的责任转移给空对象。

当命令支持撤销时，该命令必须提供和execute()方法相反的方法undo() 方法

宏命令：在命令中添加命令的集合，是命令的一种简单延伸，允许调用多个命令。支持注销

命令模式将发出请求的对象和执行请求的对象接偶，在被解耦的两者之间时通过命令对象进行沟通的，命令对象封装了接收者和一个或一组动作

调用者通过调用命令对象的execute（）发出请求，这会使接收者的动作被调用

调用者可以接受命令当做参数，甚至可以在运行时动态进行

实际操作时，直接实现请求，而非将工作直接委托给接收者



## 适配器模式与外观模式

适配器模式将一个类的接口，转化成客户期望的另一个接口。适配器让原本接口不兼容的类可以合作无间。

外观模式提供了一个统一的接口，用来访问子系统中的一群接口。外观定义了一个高层接口，让子系统更容易使用。

意图：

装饰者模式：不改变接口，但加入责任。

适配器模式：将一个接口转换成为另一个接口。

外观模式：让接口更接单。

适配器模式和外观模式的主要差异在意图上。而不在包装类的数量上，适配器是转化接口，外观模式是提供子系统的更简单的接口，从复杂的子系统中解耦。

最少知识原则：只和你的“密友”谈话。设计一个系统，不管是任何对象，都需要注意交互的类有哪些，是如何交互的，不要让太多的类耦合在一起，减少对象之间的交互。

适配器模式有两种形态：对象适配器和类适配器。类适配器用到多重继承（不适用于Java）。



##模版方法模式

模版方法定义了一个算法的步骤，并允许字类为一个或多个步骤提供实现。

模版方法模式在一个方法中定义了一个算法的骨架，而将一些步骤延迟到子类中。模版方法使得字类可以在不改变算法结构的情况下，重信定义算法中的某些步骤。

钩子（hook）是一种被声明在抽象类中的方法，但只有控的或者默认的实现。可以让子类有能力对算法的不同点进行挂钩。

好莱坞原则：别调用我们，我们会调用你。允许低层组件将自己挂钩到系统上，但是高层组件会决定when和how使用这些低层组件。

模版方法为我们提供一种代码复用的重要技巧。

模版方法的抽象类可以定义具体方法，抽象方法和钩子。

为了防止子类改变模版方法中的算法，可以将模版发放声明final。

策略模式和模版方法模式都封装算法，一个用组合，一个基础。

工厂方法是版模版方法的一种特殊版本。



## 迭代器与组合模式

迭代器模式：提供类一种方法访问一个聚合对象中的各个元素，而又不暴露其内部的表示。

迭代器将遍历聚合的工作封装到一个对象中。

当使用迭代器的时候，我们依赖聚合提供遍历。

设计原则：一个类应该只有一个引起变化的原因。

当一个模块或一个类被设计成只支持一组相关功能时，具有高内聚；反之，被设计成支持一组不想管功能时，具有低内聚。

组合模式：允许你将对象组合成树形结构来表现“整体/部分”层次结构。组合能让客户以一致的方式处理个别对象以及对象组合。

组合模式以单一设计原则获取透明性。

组合结构内的任意对象成为组件，组件可以时组合也可以时叶节点。





























