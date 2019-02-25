### iOS事件传递及响应
#### iOS中的事件分类
* 触屏事件（列如点击按钮、手势缩放）
* 传感器事件（例如摇一摇）
* 远程控制事件（列如耳机的线控、外接手柄、遥控器）

响应链的顺序是：自身 -> superView -> controller -> window -> uiapplication（有可能没有）   
总的来说传递是自上而下，响应自下而上

注意：控件不能响应的情况有    

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

分类的方法添加顺序尤其在source文件顺序决定
  
那为什么可以添加方法呢，需要研究一下  


* issue1:


### TCP/IP