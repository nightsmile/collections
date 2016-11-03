# collections

1.category重写系统方法的调用顺序
根据runtime的消息传递机制中的核心函数void objc_msgSend(id self,SEL cmd,...)来发送消息，先从当前类中查找调用的方法，若没有找到则继续从其父类中一层层往上找，那么对于category重写同一个方法，则在消息传递的过程中，会最先找到category中的方法并执行该方法。对于多个分类调用同一个方法，Xcode在运行时是根据buildPhases->Compile Sources里面的从上至下顺序编译的，编译时通过压栈的方式将多个分类压栈，根据后进先出的原则，后编译的会被先调用，当objc_msgSend找到方法并调用之后，就不再继续传递消息，所以形成所谓上的覆盖。并不是后面创建的就一定被调用，得看创建之后其在buildPhases->Compile Sources里面的位置。
关于category,这篇文章讲解的比较详细 <font color=#00ffff>http://tech.meituan.com/DiveIntoCategory.html</font>
