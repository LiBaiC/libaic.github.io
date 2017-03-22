---
title: Unreal Message Bus
date: 2017-03-22 14:18:12
---

# Unreal Message Bus,消息与消息处理
---
在UE4C++开发过程中，我们可以方便的使用unreal自带的消息处理机制，来达到各个模块之间解耦的通信模式。下面我们来看一个通过UMB改变一个游戏各状态的例子。

## 使用方式
各个模块之间的通信队列
![消息队列](https://cl.ly/0B0t3N3t1J2K/MessageQueue.png)
### 1. 添加消息头文件
添加一个单独的SGameMessage头文件，方便我们管理。在头文件中我们定义一个用来传送消息的结构体和一个代表游戏状态的枚举类。

``` C++
#pragma once

#include "SGameMessages.generated.h"   //添加Unreal代码的元数据信息，必须放在所有include的底部

/** Defines the game state */
UENUM()
enum class ESGGameStatus : uint8
{
	EGS_Init,					// Initial value
	EGS_GameStart,				// Game start
	EGS_RondBegin,				// New round begin
	EGS_PlayerTurnBegin,		// Player turn begin
	EGS_PlayerRegengerate,		// Player regenerate
	EGS_PlayerSkillCD,			// Player skill CD
	EGS_PlayerBeginInput,		// Player begin input, can link line or use the skill
	EGS_PlayerEndBuildPath,		// Player end build the path, but he can still use skill or buy some thing
	EGS_PlayerEndInput,			// Player end input, his turn end
	EGS_EnemyAttack,			// Enemy attack player
	EGS_RoundEnd,				// End of the round
	EGS_GameOver,				// Game over
};


/**
* Game status update messages
*/
USTRUCT()
struct FMessage_Gameplay_GameStatusUpdate
{
	GENERATED_USTRUCT_BODY()

	/** The new game status */
	UPROPERTY()
	ESGGameStatus NewGameStatus;
};
```
### 2. 为需要通信的模块添加私有的MessageEndPoint

``` C++
private:
	FMessageEndpointPtr MessageEndpoint;
```

### 3. 初始化MessageEndPoint

``` C++
MessageEndpoint = FMessageEndpoint::Builder("CheatManagerMessageEP"); 
```

### 4. 发送一个消息至消息队列中
在使用MessageEndPoint前需要用check对象的合法性,这是一个好习惯
``` C++
//发送一个消息到消息总线上
	check(MessageEndpoint.IsValid());
	FMessage_Gameplay_GameStatusUpdate* Message = new FMessage_Gameplay_GameStatusUpdate();  //new一个对象在堆中，不在栈上，在离开函数之后生命周期不会消失。 你负责创建，Unreal Message Bus 负责回收内存
	Message->NewGameStatus = ESGGameStatus::EGS_RondBegin;
	MessageEndpoint->Publish(Message, EMessageScope::Process);
```

### 5. 监听消息队列上需要接受的信息

``` C++
    //初始化并订阅消息 
	MessageEndpoint = FMessageEndpoint::Builder("Gameplay_GameMode") 
		.Handling<FMessage_Gameplay_GameStatusUpdate>(this, &ASGameGameMode::HandleGameStatusUpdate);  //模板函数
	check(MessageEndpoint.IsValid());
	MessageEndpoint->Subscribe<FMessage_Gameplay_GameStatusUpdate>();
```

### 6. 监听类中添加实现

``` C++
void ASGameGameMode::HandleGameStatusUpdate(const FMessage_Gameplay_GameStatusUpdate& Message, const IMessageContextRef& Context)
{
	//添加需要处理的代码
}
```