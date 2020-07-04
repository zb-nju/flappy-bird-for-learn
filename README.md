# Flappy Bird (For Train)

一个为Flappy bird机器学习改写的框架

## 来源

本项目在[flappy-bird-pygame](https://github.com/TimoWilken/flappy-bird-pygame)上进行修改

## 框架结构

```
+—— flappybird.py
+—— train.py
```

`flappybird.py`中实现游戏逻辑，使用MVC结构进行组织，可通过更改View类加速训练

## 如何使用

在`train.py`中实现了一些`Brain`的实例

`Brain`接口实现如下：

```python
class Brain(metaclass=ABCMeta):
    @abstractmethod
    def decideFlap(self,params):pass
```

在游戏运行时的每一帧都会调用`decideFlap`方法，并传入`params`

```json
{
	"bottomPipeHeight",    
	"topPipeHeight",
    "pipeWidth"		//水管宽度
	"distance",		
	"height",		//鸟的高度
	"velY",			//鸟的y轴速度
	"accY",			//鸟的y轴加速度
	"velX",  		//鸟的x轴速度
}
```

![QQ截图20200704165254](F:\Typora IMG\QQ截图20200704165254.png)

当你实现完`Brain`后，你可以通过`flappybird.py`中的`FlappyBirdGame`传入你的Brain

例如：

```python
brain = HappyBrain()
g = fb.FlappyBirdGame(60,1,[brain]) 
g.run()
```

第一个参数`60`表示的是帧率，但是目前修改这个参数不会有任何变化（还未实现）

第二个参数是鸟的数量，或许你想让多只鸟同时飞行（例如遗传算法）

第三个参数是Brain的`List`，每只鸟的Brain都是独立的