# CH4 Inverse manipulator kinematics

## 4.1 INTRODUCTION

逆向動力學是希望我們透過指定機器人末端的空間座標，反推算其姿態的理論，但其難點在於，這個解是非線性的，解不唯一且有奇點存在，為了解決這個難題，機器人機構通常都被設計成有幾何解或數值解的方法(換句話說，有著固定的形式)，方便查找公式，換算出合理的姿態

## 4.4 ALGEBRAIC / GEOMETRIC

### Algebraic solution 代數解

為了方便解題，我們先以平面的三自由度機器手臂作為範例，首先，先用第三章學到的D-H表格製作出齊次轉移矩陣，並簡化下齊次轉移矩陣的代數關係
|![image](https://hackmd.io/_uploads/S13wwVGDkl.png)|![image](https://hackmd.io/_uploads/SkmQuNMvyx.png)|
|-|-|

然後我們就可以發現到，當我們將轉移矩陣的移動元素平方合化簡後，就可以壓出第二角度，只不過SIN值有正有負，分別對應兩種姿態

|![image](https://hackmd.io/_uploads/HJyfhVGDJe.png)|![image](https://hackmd.io/_uploads/H1IQn4MvJx.png)|![image](https://hackmd.io/_uploads/ByovhVzPyl.png)|
|-|-|-|

再來是第一角度的計算過程，比較繁瑣一點

1. 先將xy的角度1給獨立出來，想辦法用三角函數的合差化積簡化
2. 假定K1K2作為合差化積的常數，並透過換算把角度反壓出來
3. 帶回xy公式，合差化積
4. 換算，得解(必要參數K1K2，xy)

|![image](https://hackmd.io/_uploads/r1lR6NMvyl.png)|![image](https://hackmd.io/_uploads/r1J_A4GvJl.png)|
|-|-|
|![image](https://hackmd.io/_uploads/B1hu1rGv1l.png)|![image](https://hackmd.io/_uploads/rynlgSzDye.png)|

最後是第三角度，無腦換，難度都集中在第一個角度上

![image](https://hackmd.io/_uploads/HyUCeHzD1x.png)

要記得，算完後理論上來說會有兩種姿態解，選路徑比較小的

### GEOMETRIC幾何解

和代數解類似，一樣是透過找關係得解，運算過程也類似

|![image](https://hackmd.io/_uploads/HyeesrzwJe.png)|![image](https://hackmd.io/_uploads/HkngsSGv1x.png)|![image](https://hackmd.io/_uploads/Hk8WorfvJx.png)|
|-|-|-|
|![image](https://hackmd.io/_uploads/Sy_YjHMPJg.png)|![image](https://hackmd.io/_uploads/rk1qsHGwkl.png)|![image](https://hackmd.io/_uploads/BJoqiSzwJe.png)|![image](https://hackmd.io/_uploads/H1Hsjrfv1l.png)|
