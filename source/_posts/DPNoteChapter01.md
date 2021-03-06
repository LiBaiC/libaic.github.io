---
title: 关于设计模式
date: 2017-03-14 18:18:42
---

# 设计模式笔记
---
下面列子出于 HeadFrist 设计模式一书，算是一点总结。

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
---
## 2. 观察者模式
定义了对象之间的一对多依赖,这样一来,当一个对象改变状态时,他的所有依赖者都会收到通知并自动更新

### 设计原则

1. 为了交互对象之间的松耦合设计而努力

#### 例子
```java

import java.util.*;
 interface Observer {
	public void update(float temp, float humidity, float pressure);
}

interface DisplayElement {
	public void display();
}

interface Subject {
	public void registerObserver(Observer o);
	public void removeObserver(Observer o);
	public void notifyObservers();
}

class WeatherData implements Subject {
	private ArrayList<Observer> observers;
	private float temperature;
	private float humidity;
	private float pressure;
	
	public WeatherData() {
		observers = new ArrayList<Observer>();
	}
	
	public void registerObserver(Observer o) {
		observers.add(o);
	}
	
	public void removeObserver(Observer o) {
		int i = observers.indexOf(o);
		if (i >= 0) {
			observers.remove(i);
		}
	}
	
	public void notifyObservers() {
		for (Observer observer : observers) {
			observer.update(temperature, humidity, pressure);
		}
	}
	
	public void measurementsChanged() {
		notifyObservers();
	}
	
	public void setMeasurements(float temperature, float humidity, float pressure) {
		this.temperature = temperature;
		this.humidity = humidity;
		this.pressure = pressure;
		measurementsChanged();
	}

}



class CurrentConditionsDisplay implements Observer, DisplayElement {
	private float temperature;
	private float humidity;
	private Subject weatherData;
	
	public CurrentConditionsDisplay(Subject weatherData) {
		this.weatherData = weatherData;
		weatherData.registerObserver(this);
	}
	
	public void update(float temperature, float humidity, float pressure) {
		this.temperature = temperature;
		this.humidity = humidity;
		display();
	}
	
	public void display() {
		System.out.println("Current conditions: " + temperature 
			+ "F degrees and " + humidity + "% humidity");
	}
}


class WeatherStation {

	public static void main(String[] args) {
		WeatherData weatherData = new WeatherData();
	
		CurrentConditionsDisplay currentDisplay = 
			new CurrentConditionsDisplay(weatherData);

		weatherData.setMeasurements(80, 65, 30.4f);
		weatherData.setMeasurements(82, 70, 29.2f);
		weatherData.setMeasurements(78, 90, 29.2f);
	}
}

```

## 装饰模式
动态地将责任附加到对象上。若要扩展功能，装饰着提供了比继承更有弹性的替代方案。

### 设计原则
1. 类对扩张开放,对修改关闭

####例子
``` java
import java.io.*;
import java.util.*;

//超类饮料
 abstract class Beverage
{
    String description = "UnKnow Beverage";
    
    public String GetDescription()
    {
        return description;
    }
    
    public abstract double cost();
    
}

//装饰着类 对饮料类进行装饰
 abstract class CondimentDecorator extends Beverage
{
    public abstract String GetDescription();
}


//具体为某一种饮料
 class Espresso extends Beverage
{
    public Espresso()
    {
        description = "Espresso Coffee";    
     
    }
    
    public double cost()
    {
        return 1.99;
    }
}

 class HouseBlend extends Beverage
{
    public HouseBlend()
    {
        description = "HouseBlend Coffee";    
     
    }
    
    public double cost()
    {
        return 0.99;
    }
}

//添加摩卡装饰
 class Mocha extends CondimentDecorator
{
    Beverage beverage;
    
    public Mocha(Beverage beverage)
    {
        this.beverage = beverage;
    }
    
    public String GetDescription()
    {
        return beverage.GetDescription() + ", Mocha";
    }
    
    public double cost()
    {
        return .20 + beverage.cost();
    }
}

 class Soy extends CondimentDecorator
{
    Beverage beverage;
    
    public Soy(Beverage beverage)
    {
        this.beverage = beverage;
    }
    
    public String GetDescription()
    {
        return beverage.GetDescription() + ", Mocha";
    }
    
    public double cost()
    {
        return .15 + beverage.cost();
    }
}

 class Whip extends CondimentDecorator
{
    Beverage beverage;
    
    public Whip(Beverage beverage)
    {
        this.beverage = beverage;
    }
    
    public String GetDescription()
    {
        return beverage.GetDescription() + ", Mocha";
    }
    
    public double cost()
    {
        return .10 + beverage.cost();
    }
}

 class StarbuzzCoffee
{
    public static void main(String args[])
    {
        Beverage beverage = new Espresso();
        System.out.println(beverage.GetDescription() + '$'+beverage.cost());
        
        //制造一个Espresso对象
        Beverage beverage2 = new Espresso();
        beverage2 = new Mocha(beverage2);
        beverage2 = new Mocha(beverage2);
        beverage2 = new Whip(beverage2);
        System.out.println(beverage2.GetDescription()+'$'+beverage2.cost());
        
        //制造一个HouseBlend对象
        Beverage beverage3 = new HouseBlend();
        beverage3 = new Mocha(beverage3);
        beverage3 = new Mocha(beverage3);
        beverage3 = new Whip(beverage3);
        System.out.println(beverage3.GetDescription()+'$'+beverage3.cost());
        
    }
}

```

下面为运行结果
``` java
Espresso Coffee$1.99
Espresso Coffee, Mocha, Mocha, Mocha$2.49
HouseBlend Coffee, Mocha, Mocha, Mocha$1.49
```