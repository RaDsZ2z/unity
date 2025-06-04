# 21.欧拉角与四元数

unity编辑器中的“旋转”各分量使用值一般情况下是0到360的**欧拉角**来表示

![21_1](./img/21_1.png)

使用**四元数**来表示角度是unity中一种更常用更高效的做法。可能我们不理解四元数，但是可以将欧拉角和四元数进行相互转换  

```C#
//下面这个vector表示物体沿y轴旋转30度  
Vector3 rotate = new Vector3(0, 30, 0);
Quaternion quaternion = Quaternion.identity;
//欧拉角转换为四元数
quaternion = Quaternion.Euler(rotate);
//四元数转为欧拉角
rotate = quaternion.eulerAngles;
//看向一个物体
quaternion = Quaternion.LookRotation(new Vector3(0, 0, 0));//返回需要旋转的角度
```

> 这里有个问题，既然物体可以“看向一个物体”，那么“物体的朝向”是如何定义的？视频中没有讲

# 22.Debug

可以输出到控制台 普通信息、警告、错误

```C#
Debug.Log("test1");
Debug.LogWarning("test2");
Debug.LogError("test3");
```

运行之后可以点击对应按钮显示或隐藏对应类型的信息

![22_1](./img/22_1.png)

除了输出文字到控制台  还可以通过在游戏场景中绘制的方式进行debug

```C#
//绘制一条线
Debug.DrawLine(new Vector3(1,0,0), new Vector3(1, 1, 0));
Debug.DrawLine(new Vector3(1,0,0), new Vector3(1, 1, 0), Color.blue);
//绘制一条射线
Debug.DrawRay(new Vector3(1, 0, 0), new Vector3(1, 1, 0), Color.red);
```

“这些线只有开发人员看得到，真正的游戏场景里是看不到的”  

上面绘制的线段和射线是不一样的：线段的两个参数是两端点，射线的第一个参数是起点，第二个参数以起点为原点，表示方向  

![22_2](./img/22_2.png)

# 23.物体类的使用

如何使用脚本修改物体的状态（位置形状颜色等等...）

有物体`EmptyObject`和对应脚本`ObjectClassTest.cs`

![23_1](./img/23_1.png)

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ObjecClasstTest : MonoBehaviour
{
    public GameObject Cube;
    // Start is called before the first frame update
    void Start()
    {
        GameObject go = this.gameObject; //在这里this可以省略
        //名字
        Debug.Log(go.name);
        //可以直接这样写
        Debug.Log(gameObject.name);
        //标签
        Debug.Log(gameObject.tag);
        //图层
        Debug.Log(gameObject.layer);
        //立方体的名称
        Debug.Log(Cube.name);
        //Cube在场景中是否激活
        Debug.Log(Cube.activeInHierarchy);
        //Cube物体本身的激活状态
        Debug.Log(Cube.activeSelf);
        //获取Fransform组件
        Transform trans = this.transform; //由于每个物体都有一个transform组件，有很简便的获取transform组件的方法，跟gameObject一样
        Debug.Log(transform.position);
        //获取其它组件
        BoxCollider bc = GetComponent<BoxCollider>();

        //获取当前物体的子物体身上的某个组件
        //GetComponentInChildren<CapsuleCollider>(bc);

        //获取当前物体的父物体身上的某个组件
        //GetComponentInChildren<BoxCollider>(bc);

        //添加一个组件
        gameObject.AddComponent<AudioSource>();
        //给Cube添加
        Cube.AddComponent<AudioSource>();
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}

```

上方代码输出的标签和图层就是上图右上角的标签和图层

![23_2](./img/23_2.png)

这里是否打勾对应物体是否激活，且在场景中非激活状态的物体的所有子物体也是非激活的。若GameObject的勾取消了 则

```C#
Debug.Log(Cube.activeInHierarchy);//输出 false Cube在场景中未激活
Debug.Log(Cube.activeSelf);//输出 true Cube物体本身是激活的
```



当前进度 15:00