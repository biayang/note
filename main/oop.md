# oop 面向对象

## 设计思想: 高内聚, 低耦合

### 内聚: 内聚标志一个模块内各个元素彼此结合的紧密程度

#### 分类（内聚由低到高）

- 偶然内聚: 指一个模块内的各处理元素之间没有任何联系。
- 逻辑内聚: 指模块内执行几个逻辑上相似的功能，通过参数确定该模块完成哪一个功能。
- 时间内聚: 把需要同时执行的动作组合在一起形成的模块为时间内聚模块。
- 通信内聚: 指模块内所有处理元素都在同一个数据结构上操作（有时称之为信息内聚），或者指各处理使用相同的输入数据或者产生相同的输出数据。
- 顺序内聚: 指一个模块中各个处理元素都密切相关于同一功能且必须顺序执行，前一功能元素输出就是下一功能元素的输入。
- 功能内聚: 这是最强的内聚，指模块内所有元素共同完成一个功能，缺一不可。与其他模块的耦合是最弱的。

### 耦合: 软件工程中对象之间的耦合度就是对象之间的依赖性

#### 分类 (耦合由弱到强)

- 非直接耦合：两模块间没有直接关系，之间的联系完全是通过主模块的控制和调用来实现的 　
- 数据耦合：指两个模块之间有调用关系，传递的是简单的数据值，相当于高级语言的值传递;　 
- 标记耦合：指两个模块之间传递的是数据结构，如高级语言中的数组名、记录名、文件名等这些名字即标记，其实传递的是这个数据结构的地址　 
- 控制耦合：指一个模块调用另一个模块时，传递的是控制变量（如开关、标志等），被调模块通过该控制变量的值有选择地执行块内某一功能;　 
- 外部耦合：一组模块都访问同一全局简单变量而不是同一全局数据结构，而且不是通过参数传递该全局变量的信息 　
- 公共耦合：一组模块都访问同一个公共数据环境。该公共数据环境可以是全局数据结构、共享的通信区、内存的公共覆盖区等。　 
- 内容耦合：这是最高程度的耦合，也是最差的耦合。当一个模块直接使用另一个模块的内部数据，或通过非正常入口而转入另一个模块内部。

#### 解耦

- 少使用类的继承，多用接口隐藏实现的细节。 Java面向对象编程引入接口除了支持多态外， 隐藏实现细节也是其中一个目的。
- 模块的功能化分尽可能的单一，道理也很简单，功能单一的模块供其它模块调用的机会就少。（其实这是高内聚的一种说法，高内聚低耦合一般同时出现，为了限制篇幅，我们将在以后的版期中讨论）。
- 遵循一个定义只在一个地方出现。
- 少使用全局变量。
- 类属性和方法的声明少用public，多用private关键字，
- 多用设计模式，比如采用MVC的设计模式就可以降低界面与业务逻辑的耦合度。
- 尽量不用“硬编码”的方式写程序，同时也尽量避免直接用SQL语句操作数据库。
- 最后当然就是避免直接操作或调用其它模块或类（内容耦合）；如果模块间必须存在耦合，原则上尽量使用数据耦合，少用控制耦合。  
- 限制公共耦合的范围，避免使用内容耦合。

---

## 设计原则: (SOLID)

### 单一职责原则SRP(Single Responsibility Principle)

- 核心思想：应该有且仅有一个原因引起类的变更
- 问题描述：假如有类Class1完成职责T1，T2，当职责T1或T2有变更需要修改时，有可能影响到该类的另外一个职责正常工作。
- 好处：类的复杂度降低、可读性提高、可维护性提高、扩展性提高、降低了变更引起的风险。
- 需注意：单一职责原则提出了一个编写程序的标准，用“职责”或“变化原因”来衡量接口或类设计得是否优良，但是“职责”和“变化原因”都是不可以度量的，因项目和环境而异。
- 场景: 用于类的设计
  - 当我们想出一个类，或者设计出一个类的原型后，使用SRP原则核对一下类的设计是否符合SRP要求。

### 开放封闭原则OCP(Open－Close Principle)

- 核心思想：尽量通过扩展软件实体来解决需求变化，而不是通过修改已有的代码来完成变化
- 通俗来讲： 一个软件产品在生命周期内，都会发生变化，既然变化是一个既定的事实，我们就应该在设计的时候尽量适应这些变化，以提高项目的稳定性和灵活性。
- 场景: 总的指导思想
  - OCP原则是一个总的指导思想，在面向对象的设计中，如果能够符合LSP/ISP/DIP原则，一般情况下就能够符合OCP原则了。 除了在面向对象的软件设计中外，OCP也可以用于指导系统架构设计，例如常见的CORBA、COM协议，其实都可以认为是OCP原则的具体应用和实现。

### 里氏替换原则LSP(the Liskov Substitution Principle LSP)

- 核心思想：在使用基类的的地方可以任意使用其子类，能保证子类完美替换基类。
- 通俗来讲：只要父类能出现的地方子类就能出现。反之，父类则未必能胜任。
- 好处：增强程序的健壮性，即使增加了子类，原有的子类还可以继续运行。
- 需注意：如果子类不能完整地实现父类的方法，或者父类的某些方法在子类中已经发生“畸变”，则建议断开父子继承关系 采用依赖、聚合、组合等关系代替继承。
- 场景: 用于指导类继承的设计
  - 当我们设计类之间的继承关系时，使用LSP原则来判断这种继承关系是否符合LSP要求。

### 接口隔离原则ISP(the Interface Segregation Principle ISP)

- 核心思想：类间的依赖关系应该建立在最小的接口上
- 通俗来讲：建立单一接口，不要建立庞大臃肿的接口，尽量细化接口，接口中的方法尽量少。也就是说，我们要为各个类建立专用的接口，而不要试图去建立一个很庞大的接口供所有依赖它的类去调用。
- 问题描述：类A通过接口interface依赖类B，类C通过接口interface依赖类D，如果接口interface对于类A和类B来说不是最小接口，则类B和类D必须去实现他们不需要的方法。
- 需注意：
  - 接口尽量小，但是要有限度。对接口进行细化可以提高程序设计灵活性，但是如果过小，则会造成接口数量过多，使设计复杂化。所以一定要适度
    - 提高内聚，减少对外交互。使接口用最少的方法去完成最多的事情
    - 为依赖接口的类定制服务。只暴露给调用的类它需要的方法，它不需要的方法则隐藏起来。只有专注地为一个模块提供定制服务，才能建立最小的依赖关系。
- 场景: 用于指导接口的设计
  - ISP原则可以认为是SRP原则的一个变种，本质上和SRP的思想是一样。SRP用于指导类的设计，而ISP用于指导接口的设计。

### 依赖倒置原则DIP(the Dependency Inversion Principle DIP)

- 核心思想：高层模块不应该依赖底层模块，二者都该依赖其抽象；抽象不应该依赖细节；细节应该依赖抽象；
- 说明：高层模块就是调用端，低层模块就是具体实现类。抽象就是指接口或抽象类。细节就是实现类。
- 通俗来讲：依赖倒置原则的本质就是通过抽象（接口或抽象类）使个各类或模块的实现彼此独立，互不影响，实现模块间的松耦合。
- 问题描述：类A直接依赖类B，假如要将类A改为依赖类C，则必须通过修改类A的代码来达成。这种场景下，类A一般是高层模块，负责复杂的业务逻辑；类B和类C是低层模块，负责基本的原子操作；假如修改类A，会给程序带来不必要的风险。
- 解决方案：将类A修改为依赖接口interface，类B和类C各自实现接口interface，类A通过接口interface间接与类B或者类C发生联系，则会大大降低修改类A的几率。
- 好处：依赖倒置的好处在小型项目中很难体现出来。但在大中型项目中可以减少需求变化引起的工作量。使并行开发更友好。
- 场景: 用于指导类依赖的设计
  - 当我们设计类之间的依赖关系时，可以使用DIP原则来判断这种依赖是否符合DIP原则。 DIP原则和LSP原则相辅相成：DIP原则用于指导抽象出接口或者抽象类，而LSP原则指导从接口或者抽象类派生出新的子类。

```bash
一句话概括:
    - 单一职责原则: 实现类要职责单一；
    - 里氏替换原则: 不要破坏继承体系；
    - 依赖倒置原则: 要面向接口编程；
    - 接口隔离原则: 在设计接口的时候要精简单一；
    - 而开闭原则他: 要对扩展开放，对修改关闭。
```

## 设计模式:(23种)

### 创建型模式

- [简单工厂simple_factory](src/php_design_patterns/simple_factory/simple_factory.php) 一个工厂类根据传入参数决定创建哪一种产品实例
- [工厂方法模式factory_method](src/php_design_patterns/factory_method/factory_method.php) 定义一个用于创建对象的接口，让子类决定实例化那个类
- [抽象工厂模式abstract_factory](src/php_design_patterns/abstract_factory/abstract_factory.php) 创建相关依赖对象家族，而无须指定具体类
- [单例模式singleton](src/php_design_patterns/singleton/mysql_singleton.php) 确保一个类只有一个实例，提供一个全局访问点
- [建造者模式builder](src/php_design_patterns/builder/builder.php) 封装一个复杂对象过程，按照步骤构建对象
- [原型模式prototype](src/php_design_patterns/prototype/prototype.php) 通过复制现有实例创建新实例

### 结构型模式

- [适配器模式adapter](src/php_design_patterns/adapter/adapter.php) 将一个类的方法或者接口转换成客户希望另一个接口
- [桥接模式bridge](src/php_design_patterns/bridge/bridge.php) 将抽象部分与实现部分分离，使他们都可以独立进行变化
- [合成模式composite1](src/php_design_patterns/composite/composite.php) 将对象组成成树形结构以表示“整体-部分”的层次结构
- [装饰器模式decorator](src/php_design_patterns/decorator/decorator.php) 动态的给对象添加新的功能
- [门面模式facade](src/php_design_patterns/facade/facade.php) 对外提供一个统一方法，用来访问子系统中一群接口
- [代理模式proxy](src/php_design_patterns/proxy/proxy.php) 为其他对象提供一种代理以控制对这个对象的访问
- [享元模式flyweight](src/php_design_patterns/flyweight/flyweight.php) 通过共享技术来有效支持大量细粒度的对象

### 行为型模式

- [策略模式strategy](src/php_design_patterns/strategy/strategy.php) 定义一系列算法，把它们封装起来，并且使它们可以互相替换
- [模板方法模式template_method](src/php_design_patterns/template_method/template_method.php) 定义一个算法结构，而将一些步骤延迟到子类实现
- [观察者模式observer](src/php_design_patterns/observer/observer.php) 对象间一对多依赖关系，一个对象改变，依赖于它对象得到通知并更新
- [迭代器模式decorator](src/php_design_patterns/decorator/decorator.php) 一种遍历访问容器对象中各个元素的方法，不暴露该对象内部结构
- [责任链模式responsibility_chain](src/php_design_patterns/responsibility_chain/responsibility_chain.php) 将请求的发送者和接受者解耦，使得多个对象都有处理这个请求的机会
- [命令模式command](src/php_design_patterns/command/command.php) 将命令请求封装成一个对象，可以将不同请求来进行参数化
- [备忘录模式memento](src/php_design_patterns/memento/memento.php) 在不破坏封装前提下，保存对象内部状态
- [状态模式state](src/php_design_patterns/state/state.php) 允许一个对象在其内部状态改变时改变它的行为
- [访问者模式visitor](src/php_design_patterns/visitor/visitor.php) 在不改变数据结构的前提下，增加作用于一组元素对象新功能
- [中介者模式mediator](src/php_design_patterns/mediator/mediator.php) 用一个中介对象来封装一系列对象交互
- [解释器模式interpreter](src/php_design_patterns/interpreter/interpreter.php) 定义一个语言，定义它的文法的一种表示，并定义一个解释器

## ref

- [如何通俗理解设计模式及其思想](https://blog.csdn.net/mq2553299/article/details/80962335)
- [Java设计模式：23种设计模式全面解析（超级详细）](http://c.biancheng.net/design_pattern/)
- [23种设计模式简单定义](https://www.jianshu.com/p/a7e5226d3f46)
- [S.O.L.I.D: The First 5 Principles of Object Oriented Design](https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)
