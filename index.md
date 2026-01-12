# GDScript教程

`GDScript`是`Godot`引擎的专用脚本语言，具有简单易学、开发便捷的特点。本教程将带你从基础代码框架入门，逐步掌握`GDScript`语法，学习面向对象编程和设计模式，并提供了丰富的代码示例。

::: tip 卷首词
你说的对，但是《Godot》是一款由社区自主研发的全新开源游戏引擎。引擎使用了一个被称作「GDScript」的简单脚本。在这里，将Godot选中的人将自主学习「编程技巧」，导引代码之力。你将扮演一位名为「独游开发者」的神秘角色，在自由的旅行中邂逅性格各异、能力独特的伙伴们，和他们一起制作游戏，挣回Steam上架费————同时，逐步发掘「发售即扑街」的真相。
:::

---

- ## 基础概念
  - [预测试](1.pre-test.html)
  - [初识代码结构](2.introduction-to-code-structure.html)

- ## [变量与基本数据类型](3.variables-and-basic-data-types/)
  - [变量](3.variables-and-basic-data-types/3.1.variables.html)
  - [基本数据类型](3.variables-and-basic-data-types/3.2.basic-data-types.html)
  - [类型转换](3.variables-and-basic-data-types/3.3.type-conversion.html)
  - [算术和位运算符](3.variables-and-basic-data-types/3.4.arithmetic-and-bitwise-operators.html)

- ## [分支语句和常量](4.branch-statements-and-constants/)
  - [条件表达式](4.branch-statements-and-constants/4.1.conditional-expressions.html)
  - [if-else-elif语句](4.branch-statements-and-constants/4.2.if-else-elif.html)
  - [常量和枚举](4.branch-statements-and-constants/4.3.constants-and-enums.html)
  - [match语句](4.branch-statements-and-constants/4.4.match-statement.html)

- ## [循环语句](5.loop-statements/)
  - [while循环](5.loop-statements/5.1.while-loop.html)
  - [for循环](5.loop-statements/5.2.for-loop.html)
  - [跳转语句](5.loop-statements/5.3.jump-statements.html)

- ## [函数](6.functions.html)

- ## [集合](7.collections/)
  - [数组](7.collections/7.1.array.html)
    - [API文档摘要](7.collections/api-docs-summary/array.html)
  - [紧缩数组](7.collections/7.2.packed-array.html)
    - [API文档摘要](7.collections/api-docs-summary/packed-array.html)
  - [字典](7.collections/7.3.dictionary.html)
    - [API文档摘要](7.collections/api-docs-summary/dictionary.html)

- ## [可调用体](8.callable.html)

- ## [信号](9.signals.html)

- ## [面向对象入门](10.object-oriented-intro/)
  - [类](10.object-oriented-intro/10.1.class.html)
  - [对象](10.object-oriented-intro/10.2.object.html)
  - [静态成员](10.object-oriented-intro/10.3.static-members.html)
  - [继承](10.object-oriented-intro/10.4.inheritance.html)
  - [多态](10.object-oriented-intro/10.5.polymorphism.html)
  - ## [设计原则](10.object-oriented-intro/10.6.design-principles/)
    - [单一职责原则](10.object-oriented-intro/10.6.design-principles/10.6.1.single-responsibility-principle.html)
    - [开闭原则](10.object-oriented-intro/10.6.design-principles/10.6.2.open-closed-principle.html)
    - [里氏替换原则](10.object-oriented-intro/10.6.design-principles/10.6.3.liskov-substitution-principle.html)
    - [接口隔离原则](10.object-oriented-intro/10.6.design-principles/10.6.4.interface-segregation-principle.html)
    - [依赖倒置原则](10.object-oriented-intro/10.6.design-principles/10.6.5.dependency-inversion-principle.html)
    - [迪米特法则](10.object-oriented-intro/10.6.design-principles/10.6.6.law-of-demeter.html)
    - [组合优于继承](10.object-oriented-intro/10.6.design-principles/10.6.7.composition-over-inheritance.html)

  - ### [设计模式](10.object-oriented-intro/10.7.design-patterns/)
  
    - #### [创建型模式](10.object-oriented-intro/10.7.design-patterns/10.7.1.creational-patterns/)
      - [单例模式](10.object-oriented-intro/10.7.design-patterns/10.7.1.creational-patterns/10.7.1.1.singleton-pattern.html)
      - [工厂方法](10.object-oriented-intro/10.7.design-patterns/10.7.1.creational-patterns/10.7.1.2.factory-method.html)
      - [抽象工厂](10.object-oriented-intro/10.7.design-patterns/10.7.1.creational-patterns/10.7.1.3.abstract-factory.html)
      - [建造者模式](10.object-oriented-intro/10.7.design-patterns/10.7.1.creational-patterns/10.7.1.4.builder-pattern.html)
      - [原型模式](10.object-oriented-intro/10.7.design-patterns/10.7.1.creational-patterns/10.7.1.5.prototype-pattern.html)

    - #### [结构型模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/)
      - [适配器模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/10.7.2.1.adapter-pattern.html)
      - [桥接模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/10.7.2.2.bridge-pattern.html)
      - [装饰器模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/10.7.2.3.decorator-pattern.html)
      - [代理模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/10.7.2.4.proxy-pattern.html)
      - [外观模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/10.7.2.5.facade-pattern.html)
      - [享元模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/10.7.2.6.flyweight-pattern.html)
      - [组合模式](10.object-oriented-intro/10.7.design-patterns/10.7.2.structural-patterns/10.7.2.7.composite-pattern.html)

    - #### [行为型模式](/10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/)
      - [责任链模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.1.chain-of-responsibility.html)
      - [命令模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.2.command-pattern.html)
      - [解释器模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.3.interpreter-pattern.html)
      - [迭代器模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.4.iterator-pattern.html)
      - [中介者模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.5.mediator-pattern.html)
      - [备忘录模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.6.memento-pattern.html)
      - [观察者模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.7.observer-pattern.html)      
      - [策略模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.8.strategy-pattern.html)
      - [状态模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.9.state-pattern.html)
      - [模板方法模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.10.template-method-pattern.html)
      - [访问者模式](10.object-oriented-intro/10.7.design-patterns/10.7.3.behavioral-patterns/10.7.3.11.visitor-pattern.html)

- ## [注解](11.annotation.html)

- ## [文档注释](12.doc-comments.html) 

---

## 使用须知

* 教程中的`GDScript`代码以`MIT`协议开源
* 教程里的文字内容非商用时**请注明出处**，商用请联系我们
