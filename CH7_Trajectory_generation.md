## CH7 Trajectory generation

## 7.3 JOINT-SPACE SCHEMES
我們希望機器人路徑規劃方案具有運算效率高、避免奇異點問題、光滑過渡運動場景的特性。

要學習基本的路徑規劃方法，首先我們先以角度-時間圖來看

![image](https://hackmd.io/_uploads/SJlVfn4vyg.png)

當我們規劃好最終姿態和最後姿態後，透過逆姿態矩陣轉換成每個伺服馬達所需的角度，並於角度-時間圖標記出起點和終點，此時如圖，會有很多選擇讓我們在路徑中分配角加速度，但想動的順，我們可以抓住幾個設計要領

### 多次項方程式逼近法 ![image](https://hackmd.io/_uploads/rJpLgnVDke.png)

![image](https://hackmd.io/_uploads/SyZZ1nNPJx.png)

||三次方程式逼近|多次方程式逼近|
|-|-|-|
|初始定義|![image](https://hackmd.io/_uploads/rJNIlhNDJl.png)|![image](https://hackmd.io/_uploads/H1Vr-3Vwke.png)|
|參數解|![image](https://hackmd.io/_uploads/r1bTehNP1g.png) ![image](https://hackmd.io/_uploads/BJdplhNwkg.png)|![image](https://hackmd.io/_uploads/Bywwb2NPkg.png)|

也有一些路徑是三次項不夠用的，此時也可以依照需求自由新增 ![image](https://hackmd.io/_uploads/ryaxznEvye.png)
![image](https://hackmd.io/_uploads/rkekG34Dyx.png)


