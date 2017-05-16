####  类与实例的关系，为什么要有类，有没有什么例子能显示出类这个概念确实是有用处的？

1. 类与实例的关系，本身没有什么好说的，就是抽象和具体，但是放到代码里一开始难以理解。
类与实例，就好比人与某个有名字的具体的人，车与一辆买了10年、跑了10万公里的奇瑞qq。
脱离实例，类没有什么用处。如果没有实例，就没有办法用类（一般情况），只能停留在抽象的层次。
拿 java 说，要删除操作D盘里的 test.txt ，简单的代码，要这样搞：

```java
File file = new File("D/test.txt"); // File 是 java 里面的文件类，file 就是 File 的一个实例
file.getParent(); // 拿到实例后，就可以调用封装到类里面的方法，获取父目录
file.delete(); // 或者删除
```
类本身也有一些方法，可以直接调用，所以刚才说是一般情况，比如
```java
File[] files = File.listRoots();// listRoots() 就是类的静态方法，可以直接调用
for(File file:files){
    System.out.println(file.getAbsolutePath());
}
```

2. 为什么要有类。没有类，就没有对象。面向对象要有对象，就要求有类。你要是搞出一个对象，但是不知道是什么类型，根本没法用。比如
```java
file = "D:/test.txt"; // 这是个字符串，还是个文件？
```

3. 类没有用处，有用处的是面向对象，面向对象必须要有类。但是面向对象本身并不是必须的，所有面向对象的代码，都可以改写成面向过程。但是有些场合就是适合用面向对象，比如你写游戏，游戏里面你要做物理效果，一个物体撞到另一个物体，它会弹。那你可以定义一个 object 类，这个 object 有个方法就是 bounce()，那你所有的游戏物体比如人物，球，车，继承 object 类之后，撞到东西都会弹了，就不要重新写逻辑。

####  面向对象

至于面向对象的好处，无非就是封装、继承、多态
我用通俗的话说下我自己的理解：

1. 封装：既封装数据，又封装方法。
   1. 封装数据，你可以把它看成是一个包裹，里面装了很多东西，传递来传递去，前台后台数据库到处传，就要封装，不然一堆数据看着很难看。
   2. 封装方法，你可以把它看成是一个工具，比如汽车，它能干很多事情，但不需要管怎么做到的。

File 里有很多属性，比如名字，父目录，你都看不到，但是你用适当方法就能获取到。
设想下你写个移动文件的方法 move(源文件，目标位置)，那这个源文件，不就是起到个包裹的作用吗？

2. 继承：刚才游戏的例子已经说过了。
3. 多态：一个司机，他会 drive(Car c)，这个时候你给他个 Porsche BMW Bench，他都能开：

```java
class Driver{
    void drive(Car c){ // 方法定义的时候，参数只写了 Car，但是传入的时候，宝马奔驰都能传进去
        c.run();
    }
}
abstract class Car{
    void run();
}
class BMW extends Car{ // 用 implements Runnable 更贴合场景，不过 Runnable 被占用了
    void run(){
        // 宝马这样跑
    }
}
class Bench extends Car{
    void run(){
        // 奔驰那样跑
    }
}

Driver jack = new Driver();
Car bmw = new BMW();
Car bench = new Bench();
jack.drive(bmw); // 
jack.drive(bench);
```
