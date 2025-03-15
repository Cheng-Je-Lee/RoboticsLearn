# Euler 角與 RPY（Roll-Pitch-Yaw）

## 1. Euler 角是什麼？
Euler 角（歐拉角）是一組用來描述剛體旋轉的三個角度，常見的旋轉順序有 **XYZ、ZYX、ZXY** 等，根據應用領域的不同會選擇不同的順序。

### 旋轉順序（常見）
1. **XYZ（固定軸旋轉）**：先繞 X 軸旋轉，再繞 Y 軸，最後繞 Z 軸。
2. **ZYX（RPY角）**：這種順序最常用在機器人學，也稱為 **Roll-Pitch-Yaw（滾轉-俯仰-偏航）**。


## 2. RPY（Roll-Pitch-Yaw）
**RPY 角 = 一種 Euler 角的表示方式（ZYX 順序）**，用來表示機器人的姿態，特別是在飛行器、機械手臂、ROS 系統中。

- **Roll（滾轉）**：繞 X 軸旋轉（左右傾斜）
- **Pitch（俯仰）**：繞 Y 軸旋轉（前後仰起）
- **Yaw（偏航）**：繞 Z 軸旋轉（左右轉向）

這樣的旋轉順序叫做 **ZYX Euler 角**，所以 RPY 角 **本質上是 Euler 角的一種特定排列**！


## 3. 兩者的區別
|  | Euler 角（一般） | RPY 角（ZYX Euler 角） |
|---|---|---|
| **旋轉順序** | 任意順序（XYZ, ZYX, ZXY...） | 固定 ZYX |
| **常見用途** | 3D 旋轉數學、電腦圖形學 | 機器人運動學、飛行器、ROS |
| **表示方式** | α, β, γ | Roll, Pitch, Yaw |


## 4. 公式與計算（ZYX 旋轉）
若以 **RPY（ZYX）** 角旋轉，則變換矩陣為：

\[
R = R_z(\text{Yaw}) \cdot R_y(\text{Pitch}) \cdot R_x(\text{Roll})
\]

其中，每個單軸旋轉矩陣為：

\[
R_x(\theta) = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta & \cos\theta \end{bmatrix}
\]

\[
R_y(\theta) = \begin{bmatrix} \cos\theta & 0 & \sin\theta \\ 0 & 1 & 0 \\ -\sin\theta & 0 & \cos\theta \end{bmatrix}
\]

\[
R_z(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}
\]


## 5. Python 計算示例
```python
import numpy as np
from scipy.spatial.transform import Rotation as R

# 定義 RPY 角度（單位：度）
rpy_angles = [30, 45, 60]  # Roll, Pitch, Yaw

# 轉換成弧度
rpy_radians = np.radians(rpy_angles)

# 使用 SciPy 計算旋轉矩陣
rotation = R.from_euler('zyx', rpy_radians)
rotation_matrix = rotation.as_matrix()

print("旋轉矩陣：")
print(rotation_matrix)
```

這樣就能得到一個 3x3 的旋轉矩陣！
