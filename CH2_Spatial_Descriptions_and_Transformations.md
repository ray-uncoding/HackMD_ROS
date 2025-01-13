# CH2 Spatial Descriptions and Transformations


## 2.1 Introduction


在機器人學中，我們將機器的可操作節點稱作 **joint**，這些節點之間的相對屬性（如移動、旋轉等）共同構成了機器人的最終姿態。

為了精確描述這種相對關係，我們以線性代數為基礎，為每個節點建立自己的坐標系（coordinate frame）。透過**轉移矩陣（transformation matrix）**，我們可以表示節點之間的轉換關係，包括位置（position）與方向（orientation）的改變。

這些描述將作為機器人運動學與動力學計算的基礎。

## 2.2 DESCRIPTIONS: POSITIONS, ORIENTATIONS, AND FRAMES
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
        
## 2.3 MAPPINGS: CHANGING DESCRIPTIONS FROM FRAME TO FRAME

![image](https://hackmd.io/_uploads/rJZVfGGw1e.png)

基本觀念就像圖2.4的內容，我們將其寫成數學式(加入旋轉)不難發現，frame間的轉換關係是**先旋轉、再移動**，利用這個規則，我們可以進一步把加法省略，直接將旋轉矩陣擴增至4*4矩陣，稱為**齊次座標（Homogeneous Coordinates）**

![image](https://hackmd.io/_uploads/BJArGMMPyg.png)

其結構如下:

![image](https://hackmd.io/_uploads/HJMPzffDJe.png)

它的實際運算特性集中在上半部的三列中，左側是旋轉矩陣，右側是座標原點的移動矩陣，下面的列則是用來保持計算的其次性，而相對的，計算時座標也要跟著擴增為4*1的齊次座標表達式

## 2.7 TRANSFORM EQUATIONS

轉移矩陣的計算由於被線性代數正規化了，所以具有連鎖的特性，可以順向計算，當然也可以反向計算

|![image](https://hackmd.io/_uploads/rkwqBzfPkl.png)|![image](https://hackmd.io/_uploads/B1EASMGwyl.png) ![image](https://hackmd.io/_uploads/r13bIfGwJx.png) ![image](https://hackmd.io/_uploads/SJh3tzzD1e.png) ![image](https://hackmd.io/_uploads/HyZRFGMwJl.png)|
|-|-|

## 2.8 ORE ON REPRESENTATION OF ORIENTATION

矩陣乘法是沒有交換率的，這就意味著當我們不規定旋轉的順序，我們在進行連鎖計算時可能會出現不一樣的姿態，所以普遍
來說，旋轉將分成三種方法


|X—Y—Z fixed angles ![image](https://hackmd.io/_uploads/r1JhcGzDJl.png) | X—Y—Z fixed angles ![image](https://hackmd.io/_uploads/r1JhcGzDJl.png) |
|-|-|
| 最簡單暴力的旋轉方法，固定住絕對坐標系強行旋轉，但不考慮機械結構，所以幾乎不會被採用![image](https://hackmd.io/_uploads/HyD-izzvJx.png)![image](https://hackmd.io/_uploads/ByQPofMwJx.png)![image](https://hackmd.io/_uploads/HJgYsMGvye.png)| 歐拉角，常用的方法，不過我們通常會採用ZYZ的方法，畢竟能少一個參數![image](https://hackmd.io/_uploads/SJC0izfwkl.png)![image](https://hackmd.io/_uploads/rJYJ3GGP1g.png)|

## Z—Y—Z Euler angles
| ![image](https://hackmd.io/_uploads/SJJcnfGwJl.png) | ![image](https://hackmd.io/_uploads/r1YqnMfv1e.png) |
|-|-|

## 總結

這是很基本的線性代數運算，只有先搞懂了這個線性的基礎才能接著衍生出正向逆向運動學

## [GIT HUB 旋轉計算器](https://github.com/ray-uncoding/matrix_math)