# CH3 Manipulator kinematics

## 3.4 CONVENTION FOR AFFIXING FRAMES TO LINKS

![image](https://hackmd.io/_uploads/B1U8HXfDkx.png)

經過第二章我們對frame之間的轉換關係有初步了解，那接下來的問題就是要如何正確地把機械結構描述成數學結構，而在數學上描述兩軸之間的相對關係，至少需要兩項參數:

|1. 軸之間的正交距離（Link Length, a）|2. 軸之間的相對夾角（Link Twist, 𝛼）|
|-|-|
|兩軸的最短距離|兩軸的相對旋轉|
    
而機器人學中，由於joint的形式多種多樣(例如伺服馬達和滑軌)其對應的形式很難只用兩項參數就推算出準確的轉移矩陣，所以除了訂定旋轉軸(Z)的相對關係參數(a、𝛼)，還必須加入正交軸(X)之間的相對關係(d、𝜃)

|3. 沿正交軸的位移（d）|4. 旋轉軸的旋轉角度（𝜃）|
|-|-|
|用於描述滑軌式（prismatic）關節的移動行為|用於描述旋轉式（revolute）關節的角度變化|

![image](https://hackmd.io/_uploads/rJNQ_mzD1x.png)

## Denavit—Hartenberg notation 例子

軸具有方向性，盡量以右手定則先訂定旋轉軸Z的方向，再來列表

| ![image](https://hackmd.io/_uploads/B1KijQzP1l.png)| ![image](https://hackmd.io/_uploads/Hy96jXGDJl.png)|
|-|-|
|![image](https://hackmd.io/_uploads/rJmlyEzPke.png)|![image](https://hackmd.io/_uploads/HyKmkEfDJl.png)|

## D-H表與齊次轉移矩陣的關係

### 轉換公式
|![image](https://hackmd.io/_uploads/SkQz-NMPyx.png)|![image](https://hackmd.io/_uploads/S1a4-4zv1g.png)|
|-|-|

### 範例
|![image](https://hackmd.io/_uploads/Hkn2ZVzvkl.png)|![image](https://hackmd.io/_uploads/Hk-CbNMDyg.png)|
|-|-|
