---
title: UE4的一些笔记
date: 2017-03-10 17:45:42
---
#UE4的一些笔记
---
##Git Repo
- GitHub    私有库收费，速度可以
- BitBucket 私有库免费，速度一般

##Game Framework
![概图](https://cl.ly/1a2T2O1A3w1U/1.png)

1. Actor

2. Components          
	A.提供给Actor重复使用。								
	B.列如 Scene Component(变换矩阵等),粒子组件
	C.以及一系列事件 exp:Hit/Begin Overlap etc..
												
3. Pawn  玩家   				
	没有movement和input code

4. Controller           
	Pawn的灵魂..负责控制Player或者AI等

5. Character            
	特殊的Pawn,Pawn添加了一系列component 可以移动等			

6. HUD									
	游戏内的UI

7. GameMode              
	A. 游戏的核心                   						
	B. 包含Pawn,Controller,HUD,etc.. 
	c. 可以在任何地方访问通过GetGameMode   		
									
8. Other Important Concepts
	A. Input
	B. Collision
	C. Replication												