# 取消DontDestroyOnLoad效果
SceneManager.MoveGameObjectToScene(go, SceneManager.GetActiveScene());
<br/>
不用找了就上面一句，用 SceneManager 把要取消 DontDestroyOnLoad 效果的物体移动到当前活跃场景里
<br/>
### 原理解释
##### 在Unity中，场景是什么
Unity的场景和很多人想的并不一样，很多朋友按照现实中的场景来理解Unity中的场景————有一个属于自己的空间，空间里有自己的物体
但实际上Unity的场景并不是这样的，Unity的场景实际上是一种分组，在同一个空间里，每个场景有属于自己的物体，就像是一个不能动的 Transform，只负责对世界空间里的物体进行分组

##### DontDestroyOnLoad是如何实现的
知道了Unity的场景实际是分组之后，DongtDestroyOnLoad 的实现就
