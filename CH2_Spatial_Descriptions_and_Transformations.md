# CH2 Spatial Descriptions and Transformations


### 2.1 Introduction


在機器人學中，我們將機器的可操作節點稱作 **joint**，這些節點之間的相對屬性（如移動、旋轉等）共同構成了機器人的最終姿態。

為了精確描述這種相對關係，我們以線性代數為基礎，為每個節點建立自己的坐標系（coordinate frame）。透過**轉移矩陣（transformation matrix）**，我們可以表示節點之間的轉換關係，包括位置（position）與方向（orientation）的改變。

這些描述將作為機器人運動學與動力學計算的基礎。

### 2.2 DESCRIPTIONS: POSITIONS, ORIENTATIONS, AND FRAMES

##### Position
![image](https://hackmd.io/_uploads/HyVENbfP1x.png)

##### Orientation
