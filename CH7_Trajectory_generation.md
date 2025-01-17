## CH7 Trajectory generation


機器手臂路徑規劃，是希望我們以Tool frame的移動座標為主，設想這個路徑在每個單位時間的姿態，判斷它是否可行，以及每個時刻的朝向與角速度

而透過前面的章節，我們已經可以透過逆向運動學推導出這些數據了，所以本章節會著重討論於路徑選擇、路徑規劃、奇點分析等等問題。

首先，我們要對路徑規劃方法有初步的認識，步驟大概是這樣：
1. 利用順逆姿態學找到起點和終點的姿態
2. 用 joint-state 或 Cartesian-state 進行路徑分析
3. 選擇想要的優化算法
4. 丟給SOLVE讓它換算角度
5. 機器人動力學讓它動，依照預設的最大速度下前進

## 7.3 JOINT-SPACE SCHEMES

![image](https://hackmd.io/_uploads/SJlVfn4vyg.png)

將初始姿態和最終姿態的角度標記在角度時間軸上，設定自己想要的路徑時間，然後就可以開始規劃角速度變化了，通常情況下，我們會希望這個變化是平順的，為此，衍生出了幾個方法

### 多次項方程式逼近法 

假定有個多次方的多項式，可以逼近這些點，並且讓機器手臂平順地通過，通常會以至少三次方程式為基準

![image](https://hackmd.io/_uploads/ryaxznEvye.png)
||三次方程式逼近|多次方程式逼近|
|-|-|-|
|初始定義|![image](https://hackmd.io/_uploads/H1Vr-3Vwke.png)||
|參數解|![image](https://hackmd.io/_uploads/Bywwb2NPkg.png)|![image](https://hackmd.io/_uploads/rkekG34Dyx.png)|

### 二次方程式修正法

如果我們只是想要簡單的讓角速度變化柔順一點，那可以讓過於尖銳的角度加上二次方程式的圓角就好，並且也可以透過添加一些假的點位(Pseudo via point)進入算式中，讓角速度變化平順以外，還通過原本計畫好的點位

|![image](https://hackmd.io/_uploads/rkAARVLP1l.png)|![image](https://hackmd.io/_uploads/HyYV04Uw1l.png)|
|-|-|

公式化的修正方法如下，我們於圖上標註出角度座標、時間區段等參數，並套入以下公式得到優化的角速度路徑，公式雖然看著很雜，但對於程式碼來說，這個方法的計算是最輕鬆的

![image](https://hackmd.io/_uploads/BkZ0Jr8P1g.png)

|![image](https://hackmd.io/_uploads/SyFreHLwJx.png)| ![image](https://hackmd.io/_uploads/B1JugHUPkl.png)| ![image](https://hackmd.io/_uploads/ByP0xrIw1e.png)|
|-|-|-|


## 7.4 CARTESIAN-SPACE SCHEMES

笛卡爾坐標系算法對於實際操作來說很重要，因為它可以在三維空間中直接指定路經座標，最後反推出最佳化的路徑，並透過逆向運動學啟動機器手臂，但是上述的步驟非常的繁瑣，很仰賴機器手臂的運算刷新率，也就是說，高階的機器手臂想要運行這種分析，都不可避免的要開發一套屬於自己的逆向運動學簡化演算法，才能運行這個重要的分析


首先，想要在笛卡爾坐標系中優化路徑，就不可避免的要用上假的點位(Pseudo via point)進入算式中來輔助計算路徑，但不同於角度座標的標注法，笛卡爾坐標系中的假點位有可能無法用rotation matrix一路從state frame押上來，換句話說，假點位不一定是機器手能構到的位置，那自然的，它就不符合我們前幾章節構建的機器手臂轉移矩陣，為此，我們需要對分析的座標做出矩陣拓展，變成一個6*1的座標矩陣，利用純座標矩陣的特性表達出(位置、朝向)等資訊，再做演算法

這部分就放原文吧，非常非常重要的觀念
![image](https://hackmd.io/_uploads/BydhXrLwkg.png)

而座標與座標之間的移動方面，在沒有其他演算法的干預下，如果有多條路線與朝向可以選擇，我們請向於選擇動靜比較小的路線，可以使用座標矩陣可以計算長度的特性，將可選路線進行差值計算，並選擇差值最小的路線

![image](https://hackmd.io/_uploads/Skz4NHLP1e.png)

![image](https://hackmd.io/_uploads/Hymt4HIDye.png)


## 7.5 GEOMETRIC PROBLEMS WITH CARTESIAN PATHS

要注意以下路徑規劃可能的情況，他們可能導致程式崩潰

|![image](https://hackmd.io/_uploads/ryGZvHLvJg.png)|![image](https://hackmd.io/_uploads/r1LjLSLv1x.png)|![image](https://hackmd.io/_uploads/BJkTLBIPJg.png)|
|-|-|-|
|Problems of type 1: intermediate points unreachable|Problems of type 2: high joint rates near singularity| Problems of type 3: start and goal reachable in different solutions|
|路徑遭遇奇異點，joint-state不會卡但Cartesian-space會直接死|路徑鄰近奇異點，joint-space的角速度會在此刻大幅增加|起點、終點路徑條件相斥，只能另尋解法|


## 7.6 PATH GENERATION AT RUN TIME

|joint-state 公式|Cartesian-state 公式|
|-|-|
|![image](https://hackmd.io/_uploads/BkFBKrIvJg.png)|![image](https://hackmd.io/_uploads/H11QYS8PJx.png)|
|![image](https://hackmd.io/_uploads/r1YNKHLvyx.png)|![image](https://hackmd.io/_uploads/ryiQtBLwJx.png)|

最後，笛卡爾如果算完記得丟到SOLVE返還角度值
![image](https://hackmd.io/_uploads/rJv_KSLwkl.png)

