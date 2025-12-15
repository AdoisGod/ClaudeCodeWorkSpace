---
name: motion-control-troubleshooting
description: "Systematic troubleshooting for industrial motion control systems. Use for servo/stepper motor issues, positioning problems, homing failures, communication errors, EMI, vibration. Triggers (CN): 故障診斷、馬達問題、原點復歸失敗、定位不準、通訊錯誤、伺服異常. Triggers (EN): troubleshoot, motor issue, homing fail, position error, servo alarm. Coordinated by: project-coordinator."
---

# Motion Control Troubleshooting

## 診斷流程

```
1. OBSERVE    記錄症狀、頻率、條件、錯誤碼
      ↓
2. ISOLATE    單軸測試、不同速度、不同負載
      ↓
3. BASICS     電源穩定？連線牢固？安全解除？
      ↓
4. SEARCH     查案例庫（references/common-issues-database.md）
      ↓
5. VERIFY     實施方案 → 測試 10+ 次 → 記錄結果
```

---

## 症狀快查表

| 症狀 | 可能原因 | 案例 |
|------|---------|------|
| 原點復歸間歇失敗 | 編碼器電池低、感測器髒污 | Case 001 |
| 位置漂移 | 編碼器問題、機械滑動 | - |
| 小行程不準 | 背隙、加減速不足 | Case 002 |
| 通訊 OK 但不動 | 驅動器參數錯誤 | Case 003, 006 |
| 隨機位置跳動 | EMI、編碼器線鬆 | Case 005 |
| 振動/震盪 | 增益過高、機械共振 | - |
| 馬達無法 Enable | 安全迴路、驅動器故障 | Case 006 |
| 煞車異常 | 氣壓低、閥卡住 | Case 004 |

---

## 常見問題診斷

### 原點復歸問題

**檢查順序**：
1. **編碼器** - 絕對式：電池電壓 3.0-3.6V；增量式：Z 脈波正常
2. **機構** - 歸零方向無障礙、連軸器無滑動
3. **參數** - 歸零模式、歸零速度、offset
4. **安全** - 互鎖允許、極限開關設定

### 定位精度問題

**檢查順序**：
1. **量測** - 用外部儀器確認實際誤差量
2. **機構** - 背隙、軸承磨損、熱膨脹
3. **參數** - 加減速、In-Position 範圍
4. **編碼器** - 解析度足夠？安裝穩固？

### 通訊問題

**檢查順序**：
1. **連線** - LED 指示、線纜完整、終端電阻
2. **模式** - 控制模式正確（Position/Velocity/Torque）
3. **參數** - Panasonic: POT/NOT (B→A)；Yaskawa: POT/NOT = 0x8
4. **測試** - 先試 JOG，再試複雜指令

### EMI 干擾

**檢查順序**：
1. **識別** - 特定馬達運轉時才發生？高電流時更嚴重？
2. **走線** - 訊號線離電源線 >50mm
3. **測試** - 暫時移開可疑線纜
4. **解決** - 磁環（繞 2-3 圈）、屏蔽線、分離走線

---

## 案例庫使用

案例庫位於 `references/common-issues-database.md`

**搜尋方式**：
- 用英文關鍵字：Encoder Battery, Homing, EMI, POT/NOT
- 依類別瀏覽：Motion Control / Pneumatic / Communication

**目前案例**（v1.0）：
- Case 001: 絕對式編碼器電池導致歸零失敗
- Case 002: 旋轉軸小角度定位（背隙）
- Case 003: Panasonic 伺服 POT/NOT 參數
- Case 004: 氣壓煞車異常
- Case 005: 光學尺 EMI 干擾
- Case 006: Yaskawa 伺服極限開關參數
- Case 007: 拖鏈 EMI（參照 Case 005）

---

## 參數調整原則

### 速度迴路
1. 從原廠預設開始
2. 增加 Kvp 直到開始震盪
3. 降回 70-80%
4. 增加 Kvi 減少穩態誤差

### 位置迴路
1. 先調好速度迴路
2. 增加 Kpp 直到過衝或震盪
3. 降回 70-80%
4. 調整前饋（如有）

### 自動調諧
- 用實際負載條件執行
- 自動調諧後可能需微調
- 保存成功的參數組

---

## 安全提醒

**測試前**：
- 確認急停可用
- 清空工作區域
- 從慢速小行程開始

**改參數時**：
- 記錄原值
- 一次改一個
- 每次改完都測試

---

## 與 project-coordinator 協作

本 skill 可被 `project-coordinator` 協調。

### 提供給 coordinator
- 故障案例庫
- 診斷流程

### 接收 coordinator 請求
- 「工作紀錄的這個問題要加到案例庫嗎？」
- 「有沒有類似的案例？」

### 新案例加入標準
從工作紀錄轉為正式案例需要：
- ✅ 明確症狀描述
- ✅ 完整診斷過程
- ✅ 驗證結果（10+ 次）
- ✅ 通用性（不只適用單一設備）

---

## 版本記錄

| 版本 | 日期 | 變更 |
|------|------|------|
| v2.0 | 2025-12-12 | 精簡主文件、加入 project-coordinator 協作 |
| v1.0 | 2025-11-30 | 初始版本，7 個案例 |
