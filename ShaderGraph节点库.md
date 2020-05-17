说明：本节点库来自unity官方网站翻译

https://docs.unity3d.com/Packages/com.unity.shadergraph@7.1/manual/Getting-Started.html

##  一、Artistic 艺术类

### 1.Adjustment 调整

### 2.Blend 混合

### 3.Filter 过滤

### 4.Mask 遮罩

### 5.Normal 法线

### 6.Utillity 工具类

## 二、Channel 渠道类

### 1.Combine 组合节点

**描述：**

从四个输入**R**，**G**，**B**和**A**创建新矢量。输出**RGBA**是由输入**R**，**G**，**B**和**A**组成的**四维向量**。输出**RGB**是由输入**R**，**G**和**B**组成的**三维向量**。输出**RG**是由输入**R**和**G**组成的**二维向量**。

**端口：**

| Name名称 | Direction节点方向 | Type类型 | Binding绑定 | Description描述     |
| -------- | ----------------- | -------- | ----------- | ------------------- |
| R        | Input输入         | Vector1  | None        | 输出定义的红色通道  |
| G        | Input输入         | Vector1  | None        | 输出定义的绿色通道  |
| B        | Input输入         | Vector1  | None        | 输出定义的蓝色通道  |
| A        | Input输入         | Vector1  | None        | 输出定义的Alpha通道 |
| RGBA     | Output输出        | Vector4  | None        | 输出四维向量        |
| RGB      | Output输出        | Vector3  | None        | 输出三维向量        |
| RG       | Output输出        | Vector2  | None        | 输出二维向量        |

**案例代码：**

以下示例代码表示此节点的一种可能结果。

```c#
void Unity_Combine_float(float R, float G, float B, float A, out float4 RGBA, out float3 RGB, out float2 RG)
{
    RGBA = float4(R, G, B, A);
    RGB = float3(R, G, B);
    RG = float2(R, G);
}
```



### 2.Flip  翻转

### 3.Split  分离 

### 4.Swizzle   四维索类

## 三、Input 输入类

### 1.Basic 基础类型

### 2.Geometry 几何学

### 3.Gradient 梯度

### 4.Matrix 矩阵

### 5.PBR 

### 6.Scene 场景

### 7.Texture 贴图

## 四、Master

### 1.PBR

### 2.Unlit  不发光的

## 五、Math 数学类

### 1.Advanced  高级

### 2.Basic 基础

### 3.Derivative 衍生类 

### 4.Interpolation 插补

### 5.Matrix 矩阵

### 6.Range 范围

### 7.Round 数字改变

### 8.Trigonometry 三角形

### 9.Vector 向量

### 10.Wave 波

## 六、Procedural 程序类

### 1.Noise 噪点

#### 1) Gradient Noise梯度噪声

#### 2) Simple Noise简单噪声

#### 3) Voronoi 沃罗诺伊

**描述：**

根据输入**UV**生成Voronoi或[Worley](https://en.wikipedia.org/wiki/Worley_noise)噪声。Voronoi噪声是通过计算像素与点阵之间的距离生成的。通过将这些点偏移一个伪随机数（由输入**Angle Offset**控制），可以生成一个单元簇。这些单元格的大小以及由此产生的噪声由输入**单元格密度**控制。输出**单元格**包含原始单元格数据。

**端口：**

| Name名称     | Direction节点方向 | Type类型 | Binding绑定 | Description描述                          |
| :----------- | :---------------- | :------- | :---------- | :--------------------------------------- |
| UV           | Input             | Vector 2 | UV          | Input UV value输入的UV值                 |
| Angle Offset | Input             | Vector 1 | None        | Offset value for points点的偏移值        |
| Cell Density | Input             | Vector 1 | None        | Density of cells generated产生的细胞密度 |
| Out          | Output            | Vector 1 | None        | Output noise value输出的噪点值           |
| Cells        | Output            | Vector 1 | None        | Raw cell data原始细胞数据                |

**案例代码：**

```c#
inline float2 unity_voronoi_noise_randomVector (float2 UV, float offset)
{
    float2x2 m = float2x2(15.27, 47.63, 99.41, 89.98);
    UV = frac(sin(mul(UV, m)) * 46839.32);
    return float2(sin(UV.y*+offset)*0.5+0.5, cos(UV.x*offset)*0.5+0.5);
}

void Unity_Voronoi_float(float2 UV, float AngleOffset, float CellDensity, out float Out, out float Cells)
{
    float2 g = floor(UV * CellDensity);
    float2 f = frac(UV * CellDensity);
    float t = 8.0;
    float3 res = float3(8.0, 0.0, 0.0);

    for(int y=-1; y<=1; y++)
    {
        for(int x=-1; x<=1; x++)
        {
            float2 lattice = float2(x,y);
            float2 offset = unity_voronoi_noise_randomVector(lattice + g, AngleOffset);
            float d = distance(lattice + offset, f);
            if(d < res.x)
            {
                res = float3(d, offset.x, offset.y);
                Out = res.x;
                Cells = res.y;
            }
        }
    }
}
```



### 2.Shapes 形状

### 3.Checkerboard 棋盘

## 七、Utility 工具类

### 1.Logic 逻辑

### 2.Custom Function 自定义功能

### 3.Keyword 关键字

### 4.Preview 预览

### 5.Sub Graph 子图

## 八、UV

### 1.Flipbook  活页薄

### 2.Polar Coordinates 极坐标

### 3.Radial Shear 径向剪

### 4.Rotate 旋转

### 5.Spherize 球形化

### 6.Tiling And Offset 平铺与偏移

### 7.Triplanar

### 8.Twirl 