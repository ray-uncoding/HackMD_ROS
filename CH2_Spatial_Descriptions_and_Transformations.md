# CH2 Spatial Descriptions and Transformations


### 2.1 Introduction


在機器人學中，我們將機器的可操作節點稱作 **joint**，這些節點之間的相對屬性（如移動、旋轉等）共同構成了機器人的最終姿態。

為了精確描述這種相對關係，我們以線性代數為基礎，為每個節點建立自己的坐標系（coordinate frame）。透過**轉移矩陣（transformation matrix）**，我們可以表示節點之間的轉換關係，包括位置（position）與方向（orientation）的改變。

這些描述將作為機器人運動學與動力學計算的基礎。

### 2.2 DESCRIPTIONS: POSITIONS, ORIENTATIONS, AND FRAMES
![image](https://hackmd.io/_uploads/BkLiobfP1e.png)

首先，線性代數描述**frame**與**frame**的相對關係，是透過矩陣乘法來表示其轉換關係，而為了有利於運算，我們為其定下一些規則，來方便我們將機器人的伺服馬達、滑軌等**joint**節點標準化成可以被計算的形式

+ Position (3×1 位置向量) ![image](https://hackmd.io/_uploads/r1uutZfwJg.png)
```
        xyz元素表示在此joint frame中的主軸投影量
```
+ Orientation (相對方向) ![image](https://hackmd.io/_uploads/r14p9WfP1e.png)
```
        要描述方向，就得用相對的方法旋轉frame
        所以描述joint方向的方法理所當然地採用了rotation matrix
```
+ otation Matrix（旋轉矩陣） ![image](https://hackmd.io/_uploads/H1L_TWfv1x.png)
```
        旋轉矩陣是正交矩陣，即它的轉置矩陣和逆矩陣的計算結果一致
        這個特性很大程度的簡化了逆向運動學的解構
```
+ Frame ![image](https://hackmd.io/_uploads/rktsAWMP1e.png)

```
        Frame 需要完整的描述joint之間的數學關係，所以除了轉動，還要加上移動
        才能完整的表達方向的變化，所以當我們需要描述一個點在不同frame的轉換關係時
        我們可以透過座標原點的變化加上選轉的變化來完整的把座標轉換到想要的joint上
```
![image](https://hackmd.io/_uploads/H1t2C-zD1e.png)
        

















