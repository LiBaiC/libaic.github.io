---
title: 关于设计模式
date: 2017-03-14 18:18:42
---

# 设计模式笔记
---


## 1. 策略模式
策略模式定义了算法族,分别封装起来,让他们之间可以互相替换,此模式让算法的变化独立于使用算法的客户

### 设计原则

1. 找出应用中可能需要变化之处,把它们独立出来,不要和那些不需要的变化的代码混在一起
2. 针对接口编程,而不是针对实现编程
3. 多用组合,少用继承

#### 例子

```java

	import java.io.*;
	class test  
	{
		public static void main (String[] args) throws java.lang.Exception
		{
			MallarDuck md = new  MallarDuck();
			md.PerformFly();
			md.SettingFly(new FlyNoWay());
			md.PerformFly();
			md.Display();
		}
	}
	
	interface FlyBehavior
	{
	    public void Fly();
	}
	
	class FlyWithWings implements FlyBehavior
	{
	    public void Fly()
	    {
	        System.out.println("FlyWithWings");
	    }
	}
	
	class FlyNoWay implements FlyBehavior
	{
	    public void Fly()
	    {
	        System.out.println("FlyNoWay");
	    }
	}
	
	
	class Duck
	{
	    FlyBehavior myFlyBehavior;
	    
	    public void PerformFly()
	    {
	        myFlyBehavior.Fly();
	    }
	    
	    public void SettingFly(FlyBehavior fb)
	    {
	        myFlyBehavior = fb;
	    }
	}
	
	class MallarDuck extends Duck
	{
	    public MallarDuck()
	    {
	        myFlyBehavior = new FlyWithWings();
	    }
	    
	    public void Display()
	    {
	        System.out.println("I'm real mallarDuck!");    
	    }
	}
```

