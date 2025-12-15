# 運動原語定義

## 文件資訊
- **文件編號**: 30-motion-primitives.md
- **版本**: v2.0（精簡版）
- **建立日期**: 2025-12-11
- **適用設備**: PD20 自動化檢測設備

---

## 說明

本文件定義設備中各軸的**關鍵位置名稱**和**感測器檢查原語**。

**文件定位**：
- **本文件（30-motion-primitives.md）**：位置名稱定義、感測器檢查原語
- 20-axes-specs.md：軸硬體規格（行程、速度、驅動器）
- 31/32/33/34-motion-sequences.md：動作序列（引用本文件的位置名稱）
- 35-actuator-control-reference.md：氣缸控制快速參考

**用途**：
- 定義位置變數命名規範（用於料號參數、PLC 程式）
- 提供動作序列文件的位置引用基礎
- 定義通用的感測器檢查邏輯

**v2.0 更新說明**：
- ❌ 移除：運動參數變數定義（Speed/Acce/Dece）→ 改由 PLC 程式自行定義
- ❌ 移除：基本動作定義（絕對移動、Jog 等）→ 通用功能，不需重複說明
- ❌ 移除：氣缸動作原語 → 改由 35-actuator-control-reference.md 統一管理
- ✅ 保留：關鍵位置定義（座標變數名稱）
- ✅ 保留：感測器檢查原語（通用邏輯）

---

## 目錄

### 1. 軸關鍵位置定義
- [Conv_Y1 / Conv_Y2 - 產品輸送Y軸](#conv_y1--conv_y2---產品輸送y軸)
- [Conv_R1 / Conv_R2 - 產品旋轉軸](#conv_r1--conv_r2---產品旋轉軸)
- [Conv_Z - 搬運天車Z軸](#conv_z---搬運天車z軸)
- [Conv_X - 搬運天車X軸](#conv_x---搬運天車x軸)
- [Laser_Z - Y52量測雷射上下](#laser_z---y52量測雷射上下)
- [Handle_Z1 - 手把圓對焦](#handle_z1---手把圓對焦)
- [Valve_X - 氣閥高度計伸縮](#valve_x---氣閥高度計伸縮)
- [Vis_Z / Vis_X - 鑰匙孔相機軸](#vis_z--vis_x---鑰匙孔相機軸)
- [Handle_1 / Handle_2 - 手把裂痕用軸](#handle_1--handle_2---手把裂痕用軸)
- [Slot_Z / Slot_X - Slot相機軸](#slot_z--slot_x---slot相機軸)
- [Handle_3/4/5 - 手把裂痕檢測軸](#handle_345---手把裂痕檢測軸)
- [Inner_X1 / Inner_X2 - Slot雷射伸縮](#inner_x1--inner_x2---slot雷射伸縮)
- [Slot_Y1 / Slot_Y2 - Slot相機開合](#slot_y1--slot_y2---slot相機開合)
- [HLight_Z1 - 上手把背光移動](#hlight_z1---上手把背光移動)
- [SLight_X1 / SLight_X2 - Slot燈源移動](#slight_x1--slight_x2---slot燈源移動)
- [DCheck_R1 / DCheck_R2 - Foup門旋轉](#dcheck_r1--dcheck_r2---foup門旋轉)
- [Door_X - Foup門移動](#door_x---foup門移動)

### 2. 感測器檢查原語
- [感測器狀態檢查](#感測器狀態檢查)
- [等待感測器ON](#等待感測器on)
- [等待感測器OFF](#等待感測器off)

---

# 1. 軸關鍵位置定義

## Conv_Y1 / Conv_Y2 - 產品輸送Y軸

### Conv_Y1 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Conv_Y1_Home | 原點位置 | 所有序列 |
| Conv_Y1_Safe | 安全位置 | SEQ-001 |
| Conv_Y1_Load | 入料位置 | SEQ-001 |
| Conv_Y1_Carry | 搬運位置 | SEQ-003 |
| Conv_Y1_LeftHandle | 左手把拍照 | SEQ-101 |
| Conv_Y1_RightHandle | 右手把拍照 | SEQ-102 |
| Conv_Y1_Keyhole | 鑰匙孔拍照 | SEQ-103 |
| Conv_Y1_FrontValve_Photo | 前氣閥拍照 | SEQ-104-1 |
| Conv_Y1_RearValve_Photo | 後氣閥拍照 | SEQ-104-2 |
| Conv_Y1_HandleCrack | 手把裂痕拍照 | SEQ-105 |
| Conv_Y1_FrontValve | 前氣閥量測 | SEQ-106 |
| Conv_Y1_RearValve | 後氣閥量測 | SEQ-107 |
| Conv_Y1_Y52Laser | Y52雷射量測 | SEQ-108 |

### Conv_Y2 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Conv_Y2_Home | 原點位置 | 所有序列 |
| Conv_Y2_Ready | 預備位置 | SEQ-302 |
| Conv_Y2_Unload | 出料位置 | SEQ-002 |
| Conv_Y2_Carry | 搬運位置 | SEQ-003 |
| Conv_Y2_Slot | Slot拍照 | SEQ-201 |
| Conv_Y2_FoupInner | Foup內部拍照 | SEQ-202 |
| Conv_Y2_InnerLaser | Inner雷射量測 | SEQ-203 |

---

## Conv_R1 / Conv_R2 - 產品旋轉軸

### Conv_R1 關鍵位置（旋轉軸固定4個位置）

| 位置名稱 | 角度值 | 位置編號 | 用途 | 使用序列 |
|---------|-------|---------|------|---------|
| Conv_R1_Pos1 | 0° | 1 | 正面（右手把/開門/關門） | SEQ-001/002/102/301/302 |
| Conv_R1_Pos2 | 90° | 2 | 側面（鑰匙孔/前氣閥/Y52） | SEQ-103/106/108 |
| Conv_R1_Pos3 | 180° | 3 | 背面（左手把） | SEQ-101 |
| Conv_R1_Pos4 | 270° | 4 | 側面（後氣閥） | SEQ-107 |

### Conv_R2 關鍵位置（旋轉軸固定4個位置）

| 位置名稱 | 角度值 | 位置編號 | 用途 | 使用序列 |
|---------|-------|---------|------|---------|
| Conv_R2_Pos1 | 0° | 1 | 正面（Foup內部） | SEQ-002/202/301/302 |
| Conv_R2_Pos2 | 90° | 2 | 側面（Slot/Inner） | SEQ-201/203 |
| Conv_R2_Pos3 | 180° | 3 | 背面（預留） | - |
| Conv_R2_Pos4 | 270° | 4 | 側面（預留） | - |

---

## Conv_Z - 搬運天車Z軸

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Conv_Z_Home | 原點位置 | 所有序列 |
| Conv_Z_Transport | 運輸高度 | SEQ-003 |
| Conv_Z_Grip | 夾取高度 | SEQ-003 |
| Conv_Z_Place | 放置高度 | SEQ-003 |

---

## Conv_X - 搬運天車X軸

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Conv_X_Home | 原點位置 | 所有序列 |
| Conv_X_Standby | 待機位置 | SEQ-003 |
| Conv_X_Stage1 | 載台1上方 | SEQ-003 |
| Conv_X_Stage2 | 載台2上方 | SEQ-003 |
| Conv_X_DoorOpen | 開蓋平台上方 | SEQ-003 |

---

## Laser_Z - Y52量測雷射上下

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Laser_Z_Home | 原點位置 | 所有序列 |
| Laser_Z_Measure | 量測位置 | SEQ-108 |
| Laser_Z_Safe | 安全位置 | SEQ-108 |

---

## Handle_Z1 - 手把圓對焦

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Handle_Z1_Home | 原點位置 | 所有序列 |
| Handle_Z1_Focus | 對焦位置 | SEQ-101/102 |

---

## Valve_X - 氣閥高度計伸縮

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Valve_X_Home | 原點（收回） | 所有序列 |
| Valve_X_Measure | 量測位置（伸出） | SEQ-106/107 |

---

## Vis_Z / Vis_X - 鑰匙孔相機軸

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Vis_Z_Home | 原點位置 | 所有序列 |
| Vis_X_Home | 原點位置 | 所有序列 |
| Vis_Z_Keyhole | 鑰匙孔拍照高度 | SEQ-103 |
| Vis_X_Keyhole | 鑰匙孔對焦位置 | SEQ-103 |
| Vis_Z_Valve | 氣閥拍照高度 | SEQ-104 |
| Vis_X_Valve | 氣閥對焦位置 | SEQ-104 |

---

## Handle_1 / Handle_2 - 手把裂痕用軸

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Handle_1_Home | 原點位置（Z軸） | 所有序列 |
| Handle_2_Home | 原點位置（X軸） | 所有序列 |
| Handle_1_Crack | 裂痕檢測高度 | SEQ-105 |
| Handle_2_Crack | 裂痕檢測位置 | SEQ-105 |

---

## Slot_Z / Slot_X - Slot相機軸

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Slot_Z_Home | 原點位置 | 所有序列 |
| Slot_X_Home | 原點位置 | 所有序列 |
| Slot_Z_Scan | Slot掃描高度 | SEQ-201 |
| Slot_X_Slot | Slot拍照位置 | SEQ-201 |

**特別說明**：Slot_Z 是 LineScan 的 Trigger 軸，執行線性掃描移動。

---

## Handle_3/4 - 手把裂痕檢測軸

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Handle_3_Home | 原點位置 | 所有序列 |
| Handle_4_Home | 原點位置 | 所有序列 |
| Handle_3_Crack | 裂痕檢測位置1 | SEQ-105 |
| Handle_4_Crack | 裂痕檢測位置2 | SEQ-105 |

**備註**：SEQ-105 硬體尚未安裝，此序列暫不可用。

---

## Inner_X1 / Inner_X2 - Slot雷射伸縮

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Inner_X1_Home | 原點位置 | 所有序列 |
| Inner_X2_Home | 原點位置 | 所有序列 |
| Inner_X1_Measure | Inner量測位置 | SEQ-203 |
| Inner_X2_Measure | Inner量測位置 | SEQ-203 |

---

## Slot_Y1 / Slot_Y2 - Slot相機開合

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Slot_Y1_Home | 原點位置 | 所有序列 |
| Slot_Y2_Home | 原點位置 | 所有序列 |
| Slot_Y1_Open | 左Slot相機開啟 | SEQ-201 |
| Slot_Y2_Open | 右Slot相機開啟 | SEQ-201 |

---

## HLight_Z1 - 上手把背光移動

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| HLight_Z1_Home | 原點位置 | 所有序列 |
| HLight_Z1_Light | 背光位置 | SEQ-101/102 |

---

## SLight_X1 / SLight_X2 - Slot燈源移動

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| SLight_X1_Home | 原點位置 | 所有序列 |
| SLight_X2_Home | 原點位置 | 所有序列 |
| SLight_X1_Slot | Slot照明位置 | SEQ-201 |
| SLight_X2_Slot | Slot照明位置 | SEQ-201 |

---

## DCheck_R1 / DCheck_R2 - Foup門旋轉

### 關鍵位置

| 位置名稱 | 角度值 | 用途 | 使用序列 |
|---------|-------|------|---------|
| DCheck_R1_Home | 0° | 原點位置 | 所有序列 |
| DCheck_R2_Home | 0° | 原點位置 | 所有序列 |
| DCheck_R1_Latch | 90° | Latch拍照位置 | SEQ-304 |
| DCheck_R2_Gasket | 依料號 | 膠條拍照旋轉角度 | SEQ-303 |

---

## Door_X - Foup門移動

### 關鍵位置

| 位置名稱 | 用途 | 使用序列 |
|---------|------|---------|
| Door_X_Home | 原點位置 | 所有序列 |
| Door_X_Open | 開門工作位置 | SEQ-301 |
| Door_X_Close | 關門工作位置 | SEQ-302 |
| Door_X_Rotate | 可旋轉位置 | SEQ-303/304 |
| Door_X_Gasket | 膠條拍照位置 | SEQ-303 |
| Door_X_Latch | Latch拍照位置 | SEQ-304 |
| Door_X_Standby | 待機位置 | 待機 |



---

# 2. 感測器檢查原語

## 感測器狀態檢查

### 說明
確認感測器當前狀態，不等待狀態改變。

### 用途
- 前置條件檢查
- 互鎖條件檢查
- 安全狀態確認

### 範例
- 檢查入料Buffer是否有工件：`In110 = TRUE`
- 檢查載台1是否無工件：`In010 AND In011 AND In012 = FALSE`
- 檢查氣缸是否在上位：`In112 AND In113 AND In114 = TRUE`

---

## 等待感測器ON

### 說明
等待感測器從OFF變為ON狀態，設定逾時時間防止無限等待。

### 用途
- 等待氣缸動作完成
- 等待工件到位
- 等待軸到達指定位置

### 範例
- 等待入料Buffer氣缸上升到位：等待 `In112 AND In113 AND In114 = TRUE`
- 等待載台1工件在席：等待 `In010 AND In011 AND In012 = TRUE`
- 等待定位氣缸鎖定：等待 `In100 = TRUE`

---

## 等待感測器OFF

### 說明
等待感測器從ON變為OFF狀態，設定逾時時間防止無限等待。

### 用途
- 確認氣缸離開某位置
- 確認工件已移除
- 確認軸已離開某位置

### 範例
- 確認載台1工件已移除：等待 `In010 AND In011 AND In012 = FALSE`
- 確認入料Buffer無工件：等待 `In110 = FALSE`
- 確認定位氣缸解除：等待 `In101 = TRUE`（同時 In100 = FALSE）

---

## 附錄：位置命名規範

### 格式規則
```
[軸名]_[位置功能描述]

範例：
- Conv_Y1_Home：Conv_Y1 的原點位置
- Conv_Y1_LeftHandle：Conv_Y1 的左手把拍照位置
- Conv_R1_Pos1：Conv_R1 的位置1（0度）
```

### 常用位置類型
- **Home**：原點位置（所有軸必備）
- **Safe**：安全位置（避讓位置）
- **Standby**：待機位置
- **Load**：入料位置
- **Unload**：出料位置
- **Carry**：搬運位置
- **Measure**：量測位置
- **Focus**：對焦位置
- **PosN**：旋轉軸固定位置（N = 1~4）

---

## 相關文件

### 20 層（硬體規格）
- `20-axes-specs.md` - 軸的詳細規格與行程範圍（硬體資訊）
- `22-sensors-specs.md` - 感測器完整清單
- `23-actuators-specs.md` - 執行器完整清單

### 30 層（動作序列）
- **本文件（30-motion-primitives.md）** - 位置名稱定義、感測器檢查原語
- `31-motion-sequences-common.md` - 通用流程（使用本文件定義的位置）
- `32-motion-sequences-stage1.md` - 載台1 檢測序列
- `33-motion-sequences-stage2.md` - 載台2 檢測序列
- `34-motion-sequences-door.md` - 開門模組/載台3 檢測序列
- `35-actuator-control-reference.md` - 氣缸控制快速參考表

### 40 層（互鎖與安全）
- `40-interlock-rules.md` - 互鎖規則（涉及感測器與位置條件）
- `41-safety-circuits.md` - 安全迴路定義

### 50 層（PC-PLC 介面）
- `50-plc-memory-map.md` - PLC 記憶體映射（料號參數區 DM20000~）

---

## 維護記錄

| 版本 | 日期 | 修改內容 | 修改人 |
|------|------|---------|--------|
| v2.0 | 2025-12-11 | 精簡版：移除運動參數變數、基本動作定義、氣缸章節；保留關鍵位置定義和感測器檢查原語 | Yao |
| v1.1 | 2025-11-16 | 修正軸數量，修改部分氣缸名稱 | - |
| v1.0 | 2025-10-29 | 初始版本，完整定義29個軸、7組氣缸、感測器原語 | - |

---

## 使用說明

### 如何使用本文件

**查詢位置名稱**：
1. 在目錄中找到對應的軸
2. 查看該軸的關鍵位置定義表
3. 找到需要的位置名稱和使用序列

**設計動作序列**：
1. 參考本文件定義的位置名稱
2. 在序列文件（31/32/33/34.md）中引用這些位置
3. 位置座標值由料號參數提供（DM20000~區）

**PLC 程式實作**：
1. 使用本文件的位置名稱作為變數名
2. 從料號參數區讀取實際座標值
3. 運動參數（Speed/Acce/Dece）由 PLC 程式自行定義

### 何時查閱其他文件

- 需要軸的硬體規格（行程、速度） → `20-axes-specs.md`
- 需要氣缸控制邏輯 → `35-actuator-control-reference.md`
- 需要完整動作流程 → `31/32/33/34-motion-sequences.md`
- 需要記憶體位址 → `50-plc-memory-map.md`

---

**文件結束**
