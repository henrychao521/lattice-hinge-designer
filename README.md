# 格狀鉸鏈設計推論系統 Lattice Hinge Designer

雷射切割彎木（laser kerf bending / lattice hinge）的參數化設計計算器。
輸入材料與幾何參數,即時推算最少連桿數、彎折半徑與工作應力,並可匯出雷射切割用 SVG 檔。

**線上使用**: https://henrychao521.github.io/lattice-hinge-designer/

## 功能

- 六種材料預設值（壓克力、樺木合板、MDF、實木、POM、PP）,G 與 τ 可手動覆寫
- 依 Fenner 扭轉連桿模型計算:`n ≥ (β/α)·Θ·G·b/(τ_allow·l)`
- 幾何干涉檢查（單刀切縫條件:`w·cosθ + t·sinθ ≤ w + k`）
- 設計應力上限滑桿（靜態彎折 vs 反覆開合的疲勞裕度）
- 四種切割圖樣即時預覽:直線格狀（扭轉式）、波浪（彎曲式）、十字（混合式）、長孔/蜂巢（挖除式）
- 匯出雷射切割 SVG（紅線 0.1mm 切割線）與參數報告 txt
- 教學用逐步推導展開面板,適合課堂展示計算流程

## 技術說明

純靜態單檔 HTML + vanilla JS,無後端、無建置流程,直接以 GitHub Pages 部署。

## 理論來源

- P. Fenner, *Laser-cut Lattice Living Hinges* 系列 (Deferred Procrastination, 2011–2012) — 扭轉連桿模型與公式推導
- A. Porterfield, *Curved Laser Bent Wood* (Instructables, 2014) — 曲面彎折與圖樣實驗
- Trotec Laser, *Cutting technique for bending applications* — 材料別 kerf 圖樣建議

## 注意事項

木質材料的剪切模數 G 與降伏應力 τ 受樹種、纖維方向、含水率影響極大,
表列值僅供初估,實際設計請以試片實測校正。

## 修訂紀錄

- **Rev.B (2026-07-07)** — 內容修正與優化：
  - 直線/波浪圖樣切割線改為 n+1 條（m 條交錯切線僅形成 m−1 個串聯扭轉連桿，原 n−1 條實際只有 n−2 個有效連桿）
  - 切段長改為 `2l+gap`，使相鄰列切縫重疊區（實際受扭長度）恰等於公式假設的連桿長 l（原本短少 gap/2，應力低估約兩成）
  - 十字圖樣間距改為臂長 + junction，修正原間距過密導致同列水平切線相連、板材直接斷開的問題
  - 幾何干涉角改求「第一個」違反角（投影寬度非單調，原二分法在 w≫t 時失效）
  - 新增內彎半徑小於板厚警告、輸入欄位清空防呆；雷射 SVG 內嵌參數註解便於追溯
- **Rev.A** — 初版

## 授權

MIT License — 歡迎 fork 修改,加入自己的圖樣或材料資料。
