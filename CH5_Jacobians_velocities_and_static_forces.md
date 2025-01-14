# CH5  Jacobians: velocities and static forces



## 5.1 NOTATION FOR TIME-VARYING POSITION AND ORIENTATION

雅可比矩陣 (Jacobian matrix) 本身是用於進行大量計算的數學工具，透過提取系統之間的轉移矩陣元素，達到簡化矩陣運算，直觀的用系統化思維解題的參數式狀態轉移矩陣。

對於機器人動力學則是一個特別需要大量計算的學科，非常適合使用 Jacobian 簡化運算。
為此，我們首先進行一些基本定義：

![image](https://hackmd.io/_uploads/r1IsUUXP1l.png) ![image](https://hackmd.io/_uploads/BJpm8I7P1e.png) ![image](https://hackmd.io/_uploads/S1CtLUXD1l.png)

我們對先前章節提到的靜態運算模型加入時間，並且假設每個單位都連續的，以此對單位時間內的點進行微分得到速度，但必須注意:

    1. 速度是相對的，因此速度參數具有參考坐標系區別
    2. 在未指定情況下，假設默認參考的是基坐標系

![image](https://hackmd.io/_uploads/HyLd887D1g.png)

而有速度，自然也有角速度的定義，角速度很大程度上會複雜化我們接下來的運動學方程式，這也是我們為何要採用Jacobin的原因

![image](https://hackmd.io/_uploads/HJbqwUXw1g.png) ![image](https://hackmd.io/_uploads/B1YYPImwyx.png)

參照角速度的幾何定義，我們不難發現，當坐標系同時具有速度、角速度，且這個座標點不位在參考坐標系的轉軸上時，這個座標除了他本身的系統速度，還會再加上一個旋轉造成的切線速度，就像是一個棒球選手將球甩投出去一樣，這使得我們不得不為了切線速度多加入一個參數模型來處理它

![image](https://hackmd.io/_uploads/BJlqYIXwyl.png) 
![image](https://hackmd.io/_uploads/Skc35LXvyx.png) ![image](https://hackmd.io/_uploads/H1-koUmvke.png) ![image](https://hackmd.io/_uploads/H1_yjLmPJx.png)

圖中，計算單位時間內繞軸B旋轉的座標點Q的運動路徑，也就是一個圓弓，利用三角函數代換出幾何定義後，它正好就是轉軸與座標的叉積，最後完成了速度模型的基本定義公式

![image](https://hackmd.io/_uploads/r1Jz3LXD1e.png)


## 5.4 MORE ON ANGULAR VELOCITY

在開始探討角速度的應用之前，我們先複習線性代數中的兩個重要概念

|orthonormal matrix正交矩陣| Skew-symmetric matrices反對稱矩陣|
|-|-|
|正交表示該矩陣與其自身轉置矩陣的乘法會得到單位矩陣，相當於它的轉置矩陣和反矩陣一致，且都會還原系統狀態，例如旋轉矩陣 ![image](https://hackmd.io/_uploads/rJPQcDmwJe.png)|該矩陣的轉置矩陣和自身剛好相差一個負號，其特性非常好用，任何矩陣的轉置減去自身就可以出現反對稱矩陣 ![image](https://hackmd.io/_uploads/Hy-YjPmDkx.png)

反對稱矩陣的特性不僅止於此，我們可以用正交矩陣的微分和轉置正交矩陣的乘法製作出反對稱矩陣，機器人學中，我們為了找出旋轉軸的數學模型，我們假定旋轉軸就是一個新的座標體系，並且對它進行座標系統的處理，即如下過程

1. 定義反對稱矩陣的做法 ![image](https://hackmd.io/_uploads/SksYhvQvJg.png)
2. 依照前面的數學模型，定義出座標與速度的關係 ![image](https://hackmd.io/_uploads/BkAR3D7Dyx.png)
3. 化簡最後的參數，得到旋轉軸的定義 ![image](https://hackmd.io/_uploads/S1OM6w7Pye.png) ![image](https://hackmd.io/_uploads/HycETPXDke.png)
4. 標記上對應的符號 ![image](https://hackmd.io/_uploads/HyYOaDmDyx.png) ![image](https://hackmd.io/_uploads/B1fKpP7D1e.png) ![image](https://hackmd.io/_uploads/BJ2Y6PQvye.png)

對照一下 ![image](https://hackmd.io/_uploads/r1Jz3LXD1e.png) 最後一項Q點轉動到A坐標系下就是P點，剛好可以銜接上剛剛推出來的轉動軸，也就是說，這個公式的所有未知參數都被我們用數學模型定義出來了，只要D-H表得知所有節點的對應轉動、移動關係，就可以推導速度公式

所以顯而易見的，我們接下來要做的事情就是將機器人節點標準化並帶入運動學的速度公式中，找到每個節點的速度、角速度公式

## 5.6 VELOCITY "PROPAGATION" FROM LINK TO LINK

![image](https://hackmd.io/_uploads/HyJbhdmwkx.png)

我們希望機器人機構最後如圖所示，每個joint都有自己的坐標系和速度、加速度，稍微整理一下，並針對等式兩側做反轉處理
![image](https://hackmd.io/_uploads/rJlihdQwye.png)

|伺服馬達|滑軌|
|-|-|
|![image](https://hackmd.io/_uploads/SJkJTu7v1x.png) ![image](https://hackmd.io/_uploads/HyLcT_mP1l.png) |![image](https://hackmd.io/_uploads/SkcGadmv1g.png)|

## 節點角速度、速度分析例子

![image](https://hackmd.io/_uploads/H1oByKQvyl.png)

![image](https://hackmd.io/_uploads/r12P1FXwJl.png)







