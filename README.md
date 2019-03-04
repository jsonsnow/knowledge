### iOS事件传递及响应
#### iOS中的事件分类
* 触屏事件（列如点击按钮、手势缩放）
* 传感器事件（例如摇一摇）
* 远程控制事件（列如耳机的线控、外接手柄、遥控器）

响应链的顺序是：自身 -> superView -> controller -> window -> uiapplication   
总的来说传递是自上而下，响应自下而上

注意：控件不能响应的情况有（事件不能专递）   

* 1.userInteractionEabled = NO
* 2.hidden = YES
* 3.透明度alpha小于等于0.01
* 4.子视图超出父视图区域


### runtime
* issue0:  
不能像编译后得到的类中增加实例变量；  
能向运行时创建的类中添加实例变量；    
原因如下：  
因为编译后的类以及注册在runtime中，类结构体中的objc_ivar_list实例变量的列表和instance_size实例变量的内存大小以及确定，同时runtime会调用class_setIvarLayout或class_setWeakIvarLayout来处理strong weak引用。所以不能向存在的类中添加实例变量。  

运行时创建的类是可以添加实例变量，调用class_addivar函数。但是得在调用objc_allocateClassPair之后，objc_registerClassPair之前 。


  
那为什么可以添加方法呢，需要研究一下 ,因为一个类分为存储区和方法区，方法区是通过一个指针指向并没有破坏类的内存布局。在运行期，对象的内存布局已经确定，如果添加实例变量就会破坏类的内部布局，这对编译型语言来说是灾难的。

分类的方法是在运行时候添加的，在调用load方法时方法已经attach到主类中，期添加顺序由其在source文件顺序决定，这个顺序决定期编译顺序和load加载顺序


* issue1:


### TCP/IP
#### TIME_WAIT
通信双方建立TCP连接后，主动关闭连接的一方会进入TIME_WAIT状态。  
客户端主动关闭连接时，会发送最后一个ack后，然后进入TIME_WAIT状态，再停留2个MSL时间进入CLOSED状态。 

客户端主动断开连接如下图   
![avatar](http://dl.iteye.com/upload/attachment/0077/3159/734c7efd-3d62-3946-a234-acdddff3b507.jpg)

### 算法与数据结构
#### hashMap
hashMap：hashMap是数组加链表来实现的  
key进行has运算再求余得到具体在数组的位置，位置一般通过一个链来解决冲突的，链节点保存了key和value

### C++  
指针和引用
指针方法属性或者方法的时候通过箭头->  
引用是别名可以是指针的引用也可以是具体类型

### iOS如何实现charles类似应用
主要难点在于

* 如何代理系统的请求，
* 适配https实现中间人攻击功能

#### 代理系统的请求
方案1：用一台服务器，系统的代理地址指向改服务器，charles应用与服务器通信,不过改成本太大

方案2：iPhone 实现web service功能，系统代理指向该web servcie的地址，转发请求，以及中间人攻击适配https

