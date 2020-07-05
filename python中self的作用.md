#python中self的作用
在类中定义__init__然后后面有很多self.xxx什么的，其实就是把从外部接受到的数据转换成类内部的属性  
在类里面定义方法为什么要加入self呢？  
  其实就是相当于self等于类实例化的名字，举个例子

	class Preson:
	    def sayhi(self):
	        print('hello world')
	p = Preson()
	p.sayhi()
	Preson.sayhi(p)

在代码最后一行中，我们直接使用类Person，然后调用它的sayhi方法，再在里面把实例化的p放进去，代码成功执行，这里的p就等于方法里面的self