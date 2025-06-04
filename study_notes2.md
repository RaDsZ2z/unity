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