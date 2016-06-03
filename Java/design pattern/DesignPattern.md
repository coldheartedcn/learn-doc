# 一、概况

设计模式分为三大类：

**创建型模式**：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式

**结构型模式**：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式

**行为型模式**：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式

# 二、设计模式的六大原则

1. 开闭原则（Open Close Principle）
    > 对扩展开放，对修改关闭
2. 里氏代换原则（Liskov Substitution Principle）
    > * 子类的能力大于等于父类，父类的方法子类都有
    > * 子类返回值的能力小于等于父类，子类的返回值是父类的自身或子类
    > * 子类抛出异常时父类的自身或子类
3. 依赖倒转原则（Dependence Inversion Principle）
    > 面向接口编程，依赖于抽象而不依赖于具体
4. 接口隔离原则（Interface Segregation Principle）
    > 使用多个隔离的接口，比使用单个接口要好
5. 迪米特法则（最少知道原则）（Demeter Principle）
    > 一个实体应当尽量少的与其他实体之间发生相互作用，使得系统功能模块相对独立
6. 合成复用原则（Composite Reuse Principle）
    > 尽量使用合成/聚合的方式，而不是使用继承

# 三、创建型模式

## 3.1、工厂方法模式

工厂方法模式分为三种：普通工厂模式、多个工厂方法模式和静态工厂方法模式。

### 3.1.1、普通工厂模式

普通工厂模式就是建立一个工厂类，对实现了同一接口的一些类进行实例的创建。

```
package com.mode.create;

public interface MyInterface {
    public void print();
}
```
```
package com.mode.create;

public class MyClassOne implements MyInterface {
    @Override
    public void print() {
        System.out.println("MyClassOne");
    }
}
```
```
package com.mode.create;

public class MyClassTwo implements MyInterface {
    @Override
    public void print() {
        System.out.println("MyClassTwo");
    }
}
```
```
package com.mode.create;

public class MyFactory {
    public MyInterface produce(String type) {
        if ("One".equals(type)) {
            return new MyClassOne();
        } else if ("Two".equals(type)) {
            return new MyClassTwo();
        } else {
            System.out.println("没有要找的类型");
            return null;
        }
    }
}
```
```
package com.mode.create;

public class FactoryTest {
    public static void main(String[] args){
        MyFactory factory = new MyFactory();
        MyInterface myi = factory.produce("One");
        myi.print();
    }
}
```

### 3.1.2、 多个工厂方法模式

多个工厂方法模式，是对普通工厂方法模式的改进，多个工厂方法模式就是提供多个工厂方法，分别创建对象。

直接看代码吧，我们修改MyFactory和FactoryTest如下：

```
package com.mode.create;

public class MyFactory {
    public MyInterface produceOne() {
        return new MyClassOne();
    }

    public MyInterface produceTwo() {
        return new MyClassTwo();
    }
}
```
```
package com.mode.create;

public class FactoryTest {
    public static void main(String[] args){
        MyFactory factory = new MyFactory();
        MyInterface myi = factory.produceOne();
        myi.print();
    }
}
```

### 3.1.3、 静态工厂方法模式

静态工厂方法模式，将上面的多个工厂方法模式里的方法置为静态的，不需要创建实例，直接调用即可。

直接看代码，我们修改MyFactory和FactoryTest如下：
```
package com.mode.create;

public class MyFactory {
    public static MyInterface produceOne() {
        return new MyClassOne();
    }

    public static MyInterface produceTwo() {
        return new MyClassTwo();
    }
}
```
```
package com.mode.create;

public class MyFactory {
    public static MyInterface produceOne() {
        return new MyClassOne();
    }

    public static MyInterface produceTwo() {
        return new MyClassTwo();
    }
}
```