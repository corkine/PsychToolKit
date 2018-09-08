# PsychToolKit 1.1

PsychToolKit 是一个用来简化心理学实验程序编写的类库，主要包含 Screen，Trial，Experiment以及Form类，分别对应刺激呈现、试词、实验以及GUI界面。不同于Matlab和PTB，或者Python和PyQt，在PsychToolKit中，不需要再GUI类使用逻辑判断各种不同的刺激类型并且进行不同的反应。此举措大大简化了开发以及调试的困难。

## PTK希望解决的问题

PTK使用了众多设计模式：观察者、单例、迭代器、模板方法设计模式。你只需要子类化合适的Screen，并且将其平衡的分配到Trial中（Trial有一个Screen的容器，其可以通过getScreen方法使用迭代器遍历容器，更酷的是，多次调用getScreen方法不会自动前进，你需要手动调用release方法释放它。）。Experiment类同样保存了一个Trial的容器，也有一个遍历Trial的迭代器，你可以直接对Experiment调用getScreen返回当前指针Trial的当前Screen，当这个Trial遍历完毕，返回null后自动调用下一个Trial，直到最后彻底返回null。Experiment类同样使用release方法和getScreen方法来获取下一个Screen。

## 静态界面

在PTK中，你需要做的就是为Trial实现initTrial方法，保存一组Screen到其内置容器 screens，同样为Experiment实现initExperiment方法，保存一组Trial到其内置容器trials，这样通过直接调用Experiment的getScreen方法就可以遍历两个容器的内容。你应该在Screen的initScreen中设置Screen呈现的时间，定义其GUI布局（JavaFX），分别保存在 duration 和 layout 变量中。完成这些后，复制 Form 代码，修改其默认构造器保存的 Experminet 对象，即可自动完成Screen的定时和布局展示。

## 动态行为

为了在播放Screen时对鼠标或者键盘进行反应，应该在Screen的eventHandler中进行适当的操作，在这里操纵 terminal 变量可以停止计时器的行为，你可以绘制一个界面用来响应用户的操作，也可以在这里记录需要保存的数据。提醒:数据会保存在Trial对象中，当离开程序进行文件存储。你需要实现Experiment的saveData方法来保存数据到文件中。

## 下载

下载地址 [com.mazhangjing.lab-v1.1.jar](/dist/com.mazhangjing.lab-v1.1.jar)

需要 Java 1.8 及以上版本。

## 文档

JavaDoc 文档地址 [程序文档 v1.1](/doc/index.html)

## 关于

程序遵循GPL v2协议开放源代码。

版权归 华中师范大学虚拟仿真实验室所有。©2018 Central China Normal University，PAL