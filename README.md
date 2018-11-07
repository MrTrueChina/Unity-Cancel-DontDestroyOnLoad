# 取消DontDestroyOnLoad效果
<br/>
SceneManager.MoveGameObjectToScene(go, SceneManager.GetActiveScene());<br/>
<br/>
不用找了就上面一句，用 SceneManager 把要取消 DontDestroyOnLoad 效果的物体移动到当前活跃场景里。
<br/>
<br/>

## 原理解释
### 在Unity中，场景是什么
Unity的场景和很多人想的并不一样，很多朋友按照现实中的场景来理解Unity中的场景————有一个属于自己的空间，空间里有自己的物体。<br/>
但实际上Unity的场景并不是这样的，Unity的场景实际上是一种分组，在同一个空间里，每个场景有属于自己的物体，就像是一个不能动的 Transform，只负责对世界空间里的物体进行分组。

### 加载场景是如何实现的
在知道场景实际上是一种分组后加载场景的实现就容易理解了，加载场景实际就是删除掉原来的场景，场景里的物体就被一起删除。之后加载新场景，新场景的物体一起被加载进来。这期间空间还是那个空间，只有物体发生了变化。

### DontDestroyOnLoad 是如何实现的
知道了Unity的场景实际是分组之后，DongtDestroyOnLoad 的实现就好理解的多了，如果你对一个物体使用了 DontDestroyOnLoad，那么你就会在 Hierarchy 面板看到一个叫“DontDestroyOnLoad”的场景，这个物体从他原来的场景里移动到了 DontDestroyOnLoad 场景里，这个场景在加载场景时不会被删除，场景里面的物体自然也不会被删除，可以一直存在。

### 如何取消 DontDestroyOnLoad
知道 DontDestroyOnLoad 的实现原理后要取消效果就很简单了，物体是因为在 DontDestroyOnLoad 场景里才避开了加载场景时的销毁，那只要把他从 DontDestroyOnLoad 场景里移动到普通场景里这个效果自然就没有了。<br/>
最好找的普通场景当然是当前激活场景，于是用 SceneManager.GetActiveScene() 获取当前激活场景，之后用 SceneManager.MoveGameObjectToScene() 移动过去就行了。
