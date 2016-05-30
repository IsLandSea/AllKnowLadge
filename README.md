# AllKnowLadge
---socket
Socket又称"套接字"，应用程序通常通过"套接字"向网络发出请求或者应答网络请求。
根据连接启动的方式以及本地套接字要连接的目标，套接字之间的连接过程可以分为三个步骤：服务器监听，客户端请求，连接确认。
（1）服务器监听：是服务器端套接字并不定位具体的客户端套接字，而是处于等待连接的状态，实时监控网络状态。
（2）客户端请求：是指由客户端的套接字提出连接请求，要连接的目标是服务器端的套接字。为此，客户端的套接字必须首先描述它要连接的服务器的套接字，指出服务器端套接字的地址和端口号，然后就向服务器端套接字提出连接请求。
（3）连接确认：是指当服务器端套接字监听到或者说接收到客户端套接字的连接请求，它就响应客户端套接字的请求，建立一个新的线程，把服务器端套接字的描述发给客户端，一旦客户端确认了此描述，连接就建立好了。而服务器端套接字继续处于监听状态，继续接收其他客户端套接字的连接请求。
---TCP
TCP是面向连接的通信协议，通过三次握手建立连接，通讯完成时要拆除连接，由于TCP是面向连接的所以只能用于端到端的通讯。
---UDP
UDP是面向无连接的通讯协议，UDP数据包括目的端口号和源端口号信息，由于通讯不需要连接，所以可以实现广播发送。

-----什么情况使用 weak 关键字？

在 ARC 中,在有可能出现循环引用的时候,往往要通过让其中一端使用 weak 来解决,比如: delegate 代理属性

自身已经对它进行一次强引用,没有必要再强引用一次,此时也会使用 weak,自定义 IBOutlet 控件属性一般也使用 weak；当然，也可以使用strong。在下文也有论述：《IBOutlet连出来的视图属性为什么可以被设置成weak?》

不同点：

weak 此特质表明该属性定义了一种“非拥有关系” (nonowning relationship)。为这种属性设置新值时，设置方法既不保留新值，也不释放旧值。此特质同assign类似， 然而在属性所指的对象遭到摧毁时，属性值也会清空(nil out)。 而 assign 的“设置方法”只会执行针对“纯量类型” (scalar type，例如 CGFloat 或 NSlnteger 等)的简单赋值操作。

assigin 可以用非 OC 对象,而 weak 必须用于 OC 对像

---- objc中的类方法和实例方法有什么本质区别和联系？
类方法：

1.类方法是属于类对象的
2.类方法只能通过类对象调用
3.类方法中的self是类对象
4.类方法可以调用其他的类方法
5.类方法中不能访问成员变量
6.类方法中不定直接调用对象方法

实例方法：
1.实例方法是属于实例对象的
2.实例方法只能通过实例对象调用
3.实例方法中的self是实例对象
4.实例方法中可以访问成员变量
5.实例方法中直接调用实例方法
6.实例方法中也可以调用类方法(通过类名)

---- runloop和线程有什么关系？
总的说来，Run loop，正如其名，loop表示某种循环，和run放在一起就表示一直在运行着的循环。
实际上，run loop和线程是紧密相连的，可以这样说run loop是为了线程而生，没有线程，它就没有存在的必要。
Run loops是线程的基础架构部分， Cocoa 和 CoreFundation 都提供了 run loop 对象方便配置和管理线程的 run loop （以下都以 Cocoa 为例）
。每个线程，包括程序的主线程（ main thread ）都有与之相应的 run loop 对象。


----runloop的mode作用是什么？
model 主要是用来指定事件在运行循环中的优先级的，分为：
NSDefaultRunLoopMode（kCFRunLoopDefaultMode）：默认，空闲状态
UITrackingRunLoopMode：ScrollView滑动时
UIInitializationRunLoopMode：启动时
NSRunLoopCommonModes（kCFRunLoopCommonModes）：Mode集合

-----使用block时什么情况会发生引用循环，如何解决？

一个对象中强引用了block，在block中又使用了该对象，就会发射循环引用。 解决方法是将该对象使用__weak或者__block修饰符修饰之后再在block中使用。

id weak weakSelf = self; 或者 weak __typeof(&*self)weakSelf = self该方法可以设置宏
id __block weakSelf = self;

-----在block内如何修改block外部变量？

默认情况下，在block中访问的外部变量是复制过去的，即：写操作不对原变量生效。但是你可以加上__block来让其写操作生效，示例代码如下:

------dispatch_barrier_async的作用是什么？

在并行队列中，为了保持某些任务的顺序，需要等待一些任务完成后才能继续进行，使用 barrier 来等待之前任务完成，避免数据竞争等问题。 dispatch_barrier_async 函数会等待追加到Concurrent Dispatch Queue并行队列中的操作全部执行完之后
，然后再执行 dispatch_barrier_async 函数追加的处理，等 dispatch_barrier_async 追加的处理执行结束之后，Concurrent Dispatch Queue才恢复之前的动作继续执行。

![Mou icon](http://25.io/mou/Mou_128.png)
















