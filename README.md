# Game-Audio-Design
2025-2026学年春季学期《游戏音频设计》期末作品说明
由于我先前没有什么Wwise和UE软件开发操作的经验，所以我选择了相对简单的第二个项目，根据视频的步骤进行操作实践。具体过程如下：

首先创建Wwise及UE项目，我所下载使用的Wwise版本为2024.1.5，UE版本为5.3.2。

<img width="415" height="224" alt="image" src="https://github.com/user-attachments/assets/e2f6ac12-17f5-40d8-8ea5-3f9069602805" />

<img width="415" height="224" alt="image" src="https://github.com/user-attachments/assets/93df5749-f780-44ed-96cd-84ebdddb93f9" />


将Wwise和UE的两个项目相关联，使Wwise中所制作的素材资产能够被UE接收并运用。

首先制作篝火的交互声音设计，根据视频中的教程将篝火的声音素材导入Wwise，将sizzle和crack素材分类分别装入随机播放Random Container中，修改变量使篝火的声音素材能够不断循环随机播放，模拟真实篝火音效。

<img width="415" height="224" alt="image" src="https://github.com/user-attachments/assets/ad51a06b-3ca4-4e6a-b808-6c2cc8172f78" />


之后在UE中创建物体并将Wwise中制作好的声音添加到物体上，使用蓝图实现物体声音的播放。由于我的建模功底不是很好，所以就没有细致地为篝火建模，直接用方块代替。




对于空间立体声的实现，并没有使用UE中自带的插件，而是在Wwise中使用Positioning设置实现，通过调节音量的距离衰减、高切以及声像宽度等曲线，实现篝火的声音在玩家靠近时逐渐增大，远离时逐渐衰弱最终消失，模拟现实听感。

https://media/image5.png


接下来是环境声的制作，与篝火相似，在Wwise中导入环境声素材后，在UE中创建一大一小两个AK Spatial Audio Volume，并用一个AK Acoustic Portal将它们连接，大的作为整个场地的环境声，小的作为室内的环境声。通过修改优先级，使人物在进入室内时场地的环境声会衰减。

https://media/image6.png

之后也是在Wwise中通过调整音量的距离衰减、高切以及声像宽度等曲线，让环境声更加逼真。

https://media/image7.png

除了这些，还可以通过添加AUX效果器来使进入到室内的声音带有夸张的混响。

https://media/image8.png

之后在UE中给室内的部分加上这个效果器，使所有在其中发出的声音都带有这样夸张的混响。

https://media/image9.png

最后就是角色Foley的添加，主要是为玩家操作的角色添加跑步时的脚步声。

但在这之前，先解决一个角色与玩家声像不匹配的问题。因为第三人称游戏中玩家的摄像头并不与角色的摄像头重合，所以需要一个取舍——收声的朝向是跟随玩家还是跟随角色。而UE中默认收声是跟随角色，但这样的策略在大部分游戏中很可能会导致玩家对声像的错误判断，从而直接或间接导致操作失误，破坏游戏体验，所以需要将收声朝向与摄像头朝向相一致。我们通过改写蓝图来实现这一点。

https://media/image10.png

回到脚步声的Foley，首先在Wwise中将已有的四种在不同材质上高跟鞋的脚步声资产添加，使用Random Container使其可以在触发时播放相应的随机脚步声，之后添加Switch组件使这些不同材质的脚步声可以相互切换。

https://media/image11.png

之后将这些资产同步到UE中，在角色奔跑的动画中添加音效，使角色每次落脚都能发出声音。

https://media/image12.png

接下来创建各种物理表面，使角色在踩上这些表面时能够有不同的脚步声，创建各种物理材质并添加到场景中，使各个表面得以被区分。

https://media/image13.png

最后，通过蓝图的逻辑编写，使角色的脚不断向下发射射线检测所踩到的材质，之后根据材质播放相应的脚步声。

https://media/image14.png

至此，这个声音交互的实践实验项目就算是做完了。

如果还需要我帮您提取图片、转为纯文本表格或整理为作业报告格式，也可以继续告诉我。<img width="2559" height="1379" alt="UE 1" src="https://github.com/user-attachments/assets/bb793c2b-e8ff-4a94-961c-56b83486f971" />

