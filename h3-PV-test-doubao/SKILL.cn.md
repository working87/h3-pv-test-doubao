---
name: h3-PV-test-doubao
description: "从参考图提取视觉风格 DNA，生成完整的 MiniMax H3 视频提示词（I2VA、FL2VA、Ref2VA），专注于高密度 PV 风格内容。复刻渲染方式、色彩、平面设计语汇和节奏语言，同时生成原创主体和叙事。默认输出 15秒 18-25 个镜头，带时间线同步音频弧线。"
sources: [chat]
aliases: [style-clone, h3-pvg, pvg, 风格克隆]
---

# H3 风格克隆 — PV 提示词生成器

## 核心原则

参考图只提供**视觉风格** — 色彩系统、渲染媒介、平面设计语汇、节奏语言和视觉禁止项。所有主体、角色、动作和叙事内容来自用户的方向指示，或基于参考图中识别出的主体给出建议。

**参考图 → 风格 DNA 提取**  
**用户方向 → 输出中的每个角色、动作、场景**

---

## 工作流程

```
1. 多图接收       → 识别角色（风格/首帧/尾帧/角色）
2. 风格 DNA 提取  → 色彩、渲染、平面设计、节奏、禁止项
3. 内容方向       → 用户提供 OR 模型基于识别主体建议
4. PV 结构        → 映射到灵活的 PV 框架（开场 → 递进 → 高潮 → 定格）
5. H3 提示词组装  → I2VA / FL2VA / Ref2VA，detailed_description 2000-3000 字
6. 输出验证       → 检查风格一致性、镜头密度、音频弧线
```

---

## 步骤 1 — 多图接收

在提取前识别每张图的角色：

| 角色 | 触发信号 | 模式 |
|---|---|---|
| **风格参考** | 默认；无关键帧信号 | Ref2VA |
| **首帧** | "开头用这张" / "start from this" | I2VA |
| **尾帧** | "结尾用这张" / "end on this" | L2VA |
| **首帧+尾帧** | 两张图作为开场+收尾 | FL2VA |
| **角色参考** | "这个角色" / 图中明显展示主体 | Ref2VA 多主体 |
| **环境参考** | "这个场景" / "this setting" | Ref2VA 多主体 |

**多图配置**：
- 2+ 张风格参考 → 合并风格 DNA
- 2+ 个角色 → 全部出现在同一支 PV 中，混剪蒙太奇风格
- 风格 + 多个角色 → Ref2VA，每个角色单独的 `<Subject N>`

角色模糊时默认为风格参考。

---

## 步骤 2 — 风格 DNA 提取

只提取视觉语言，跨五个维度：

### A. 色彩系统
- 调色板（精确命名每个颜色："纯黑、荧光粉、纯白"）
- 结构（单色+强调色 | 双色调 | 限定 3-4 色 | 全彩）
- 强调色角色（结构性 | 高亮 | 装饰性 | 主导）
- 背景处理（纯色 | 纸纹 | 平面纹理 | 无背景）
- 色彩禁止项（排除的色相）

### B. 渲染语言
- 媒介（2D 赛璐璐 | 平面矢量 | 像素艺术 | 水彩 | 照片写实 | 3D CG | 拼贴）
- 描边（粗黑描边 | 细描边 | 变粗细 | 彩色描边 | 无描边）
- 填充（纯平涂 | 赛璐璐阴影 | 渐变 | 点画/交叉线 | 写实光照）
- 纹理（半色调网点 | 纸纹 | 扫描噪点 | 数字噪点 | 干净）
- 禁止项（无 3D 深度 | 无体积光 | 无写实皮肤 | 无镜头虚化等）

### C. 平面设计系统
- 字体样式（笔刷 | 模板 | 像素 | 手写 | 粗黑体）— 提取形式，非内容
- 符号语汇（爱心 | 星星 | 骷髅 | 皇冠 | 笑脸 | 警告 | 条形码）— 只列通用类别
- 版式逻辑（居中 | 编辑栏 | 散乱 | 网格）
- HUD/UI 层（游戏 UI | 计量条 | 计数标签 | 菜单叠加 | 无）

### D. 节奏与电影语言
- 暗示节奏（慢 | 中 | 快/动感 | 节拍锁定）
- 切换语汇（硬切 | 故障断裂 | 纸撕转场 | 形状转场 | 淡入淡出）
- 运动图形（速度线 | 强调色轨迹 | 粒子爆发 | 符号环绕 | 压缩脉冲）

### E. 主体处理
- 角色在此视觉系统内的渲染风格
- 主体-背景关系（完全融合 | 剪影 | 分层拼贴）
- 比例风格（写实 | 风格化 | Q版 | 抽象）

---

## 步骤 3 — 内容方向

### 如果用户提供方向 → 进入步骤 4

### 如果未提供方向 → 无指令回退协议

**NI-1**：用通俗语言展示 3 行风格总结  
示例：*"平面朋克插画风：纯黑白加荧光粉，厚描线，完全没有立体感，节奏感很强，适合做高速剪辑的角色 PV。"*

**NI-2**：问一个问题  
> "你想自己描述要拍什么，还是我根据这个风格给你几个方向？"

**NI-3A**：用户提供自己的方向 → 进入步骤 4

**NI-3B**：模型建议方向
1. 从参考图识别主体（角色 | 动物 | 产品 | 场景 | 抽象）
2. 生成 2-3 个 PV 方向选项，**只改变视觉流程**，都使用同一主体：
   - 开场策略（眼睛特写→动作 | 奔跑进入→定格 | 故障爆发→揭示）
   - 递进节奏（碎片蒙太奇→全身 | 慢单镜→爆炸 | 节拍同步切换）
   - 高潮手法（分格→压缩 | 符号洪流→海报 | UI 接管→定格）

示例：
> 图里的主角是一只法斗犬，以下是 3 个 PV 方向：  
> 1. 眼睛特写开场 → 碎片蒙太奇（爪子/耳朵/项圈快切）→ 全身动作 → 符号爆炸 → 海报定格  
> 2. 奔跑进入 → UI 图层叠加 → 漫画分格 → 压缩到核心 → 粉色爆裂  
> 3. 黑屏→故障闪现 → 贴纸撕裂转场 → 高速滑行 → 正脸坏笑定格

用户选择或修改 → 进入步骤 4

---

## 步骤 4 — PV 框架（灵活）

所有输出遵循 PV 宏观结构，但根据用户方向和风格 DNA 节奏调整段落时长和密度。

### PV 骨架（默认 15 秒）

| 阶段 | 功能 | 视觉策略 |
|---|---|---|
| **开场** | 0.00–1.00s | 黑屏保持 → 爆发+文字冲击 OR 故障揭示 OR 极端特写。**不要在开场展示参考图的完整姿势或构图** — 开场建立风格和能量，不是最终海报布局。把参考姿势留给定格段落。 |
| **识别/递进** | 1.00–6.00s | 碎片蒙太奇（细节切换）+ 主体动作 + 平面图层 |
| **高潮** | 6.00–13.00s | 分格、压缩、符号洪流、UI 接管、节拍脉冲 |
| **定格** | 13.00–15.00s | 最终海报帧**精确匹配参考图的姿势和构图**，标题/标签弹入定位 |

**镜头密度基准**：15 秒 18-25 个镜头（根据风格 DNA 节奏调整）

**段落边界灵活** — 如果用户方向或风格 DNA 暗示慢节奏，拉长段落；如果动感强，压缩并增加切换。

**视觉技法**（在风格 DNA 允许的范围内应用）：
- 单色洪流 → 强调色感染
- 平面文字冲击 → 标签/UI 作为平面元素爆发
- 故障损坏 → 噪点带、像素散射
- 速度线 → 漫画风 2D 运动线
- 漫画分格 → 画面分裂 2-4 格
- 贴纸弹出 → 瞬间缩放弹跳
- 节拍脉冲 → 随音乐节拍缩放/闪烁
- UI 叠加 → 游戏 HUD 元素
- 撕裂/揭示转场 → 物理转场
- 剪影层叠 → 偏移强调色层
- 半色调场 → 网点阴影/转场
- 压缩到核心 → 所有元素向内坍缩
- 海报定格 → 运动停止，文字弹入
- 极端特写 → 眼睛/细节填满画面
- 碎片蒙太奇 → 快速细节切换（手、鞋、纹理、logo）
- 强调色轨迹 → 运动留下色彩残影
- 波浪爆发 → 同心圆从冲击点扩散
- 符号环绕 → 图标围绕主体
- 硬平面转场 → 实心形状扫过画面

---

## 步骤 5 — H3 提示词组装

### 模式选择

| 输入 | 模式 |
|---|---|
| 1 张图，首帧信号 | I2VA |
| 1 张图，尾帧信号 | L2VA |
| 2 张图，首+尾信号 | FL2VA |
| 风格/角色/环境参考 | Ref2VA |

### 风格声明

写 1-2 句话声明渲染+禁止项。放在 Ref2VA `detailed_description` 的 `[Shot 1]` 前，或 I2VA/FL2VA/L2VA 的 `[Shot 1]` 内。

**格式**：`[媒介], [色彩系统]; [描边和填充]; [纹理]; [禁止项]。`

示例：
> *Flat 2D cel-animation and editorial graphic design; strict black, white, and fluorescent pink palette with no other colors; thick black outlines, pure flat color fills, halftone dot shadows; no 3D geometry, no realistic depth, no soft lighting, no cinematic lens blur, no standard fades.*

### I2VA 格式

```
For the target video, at 0.00 seconds into the target video, <Picture 1> (from [Shot 1]) is fully referenced.

integrated_multimodal_description: [Shot 1] [风格声明]. The video opens with <Picture 1> as its first frame, establishing [可见的主体/环境]. [段落 1 动作].
[Shot 2] At 00:XX.XXX, the shot cuts to [下一构图].
...

overall_soundscape: [时间线同步音效弧线：Open（稀疏标志性音效）→ Build（逐层叠加密度）→ Peak（最大同时冲击）→ Resolve（静默/持续音）。3-6 句话带时间戳。仅环境+物理+非语言。每个音效锚定到具体视觉事件。]

non_diegetic_music: [完整音乐弧线：风格、BPM、乐器。段落边界的动态变化 — 什么进入、什么退出、什么增强。Hook → Build → Peak → Resolve 结构。无则 N/A。]
```

### FL2VA 格式

```
How the reference pictures align with the target video — Picture 1 (from Shot 1) aligns with the 0.00-second mark; Picture 2 (from Shot [N]) aligns with the [S.SS]-second mark.

integrated_multimodal_description: [Shot 1] [风格声明]. The video opens in the state of Picture 1: [描述可见状态]. [到 Picture 2 的路径]. The final shot settles into Picture 2's composition.

overall_soundscape: [同 I2VA]
non_diegetic_music: [同 I2VA]
```

### Ref2VA 格式 — 单一风格

```
subject_definitions:
<Subject 1> is the visual style in <Picture 1>: [媒介], [色彩], [平面语汇], [禁止项].
<Subject 2> is [用户的主体]: [用风格术语描述外观].

summary:
[reference generation] The target video shows [内容]. <Picture 1> provides visual style. <Subject 2> is new content built within that system.

retention_analysis:
<Subject 1> (all shots): fully_preserved — [风格元素] consistent throughout.
<Subject 2> (appears in [Shot X, Y...]): fully_preserved — [定义特征] consistent.

detailed_description:
[风格声明].
[Shot 1] [内容 + 风格 + 技法].
[Shot 2] At 00:XX.XXX, [下一个].
...

overall_soundscape: [同样结构]
non_diegetic_music: [同样结构]
```

### Ref2VA 格式 — 多角色

当多张图展示不同角色时，所有角色以混剪蒙太奇方式出现在同一支 PV 中：

```
subject_definitions:
<Subject 1> is the visual style in <Picture 1>: [风格].
<Subject 2> is the [角色 1] in <Picture 2>: [外观].
<Subject 3> is the [角色 2] in <Picture 3>: [外观].

summary:
[reference generation] The target video shows [所有角色] in a mix-cut PV montage. <Picture 1> provides rendering system. <Subject 2> and <Subject 3> are placed within that system and appear in alternating/simultaneous shots.

retention_analysis:
<Subject 1> (all shots): fully_preserved.
<Subject 2> (appears in [Shot X, Y...]): fully_preserved.
<Subject 3> (appears in [Shot Z, W...]): fully_preserved.

detailed_description:
[风格声明].
[Shot 1] [角色 1 出现 — 描述特征].
[Shot 2] At 00:XX.XXX, [角色 2 进入 — 描述特征].
[Shot 3] At 00:XX.XXX, [两个角色或交替切换].
...
```

---

## 步骤 6 — H3 格式规则

**镜头**：
- `[Shot 1]` 无时间戳
- `[Shot N] At MM:SS.SSS` 所有后续镜头，严格递增

**镜头数量**：
- 10s → 12-18 个镜头
- 15s → 18-25 个镜头
- 20s → 25-35 个镜头

**镜头运动**（写成散文）：
- `The camera pushes in with small amplitude at slow speed toward...`
- 类型：Zoom In/Out | Push In/Pull Out | Pan L/R | Truck L/R | Tilt Up/Down | Pedestal Up/Down | Arc | Tracking | Static | Shake | POV | Roll

**对白**：`(S1) says: <d>[English] Text.</d>`

**屏幕文字**：用英文双引号包裹，原语言

**overall_soundscape**：时间线同步弧线 — Open（稀疏标志性音效）→ Build（逐层叠加密度）→ Peak（最大同时冲击）→ Resolve（静默/持续音）。**按阶段分组写，不要逐镜头列时间戳**。按框架阶段分组（Hook 0-1s / Build 1-6s / Climax 6-13s / Freeze 13-15s）。每个阶段内列出关键音效及其阶段相对时间。目标 400-500 字。示例结构："Hook (0-1s): 开场低频冲击 + 故障杂音。Build (1-6s): 逐层打击乐 — 链条叮当、靴子踩踏 2s、皮革摩擦；每拍贴纸弹出声。Climax (6-13s): 符号旋转呼啸递增、压缩下降无人机 9-10s、10s 爆炸巨响带碎片叮当。Freeze (13-15s): 近乎静默，13-14s 贴纸咔哒声，扫描呼啸，霓虹嗡鸣淡出。"

**non_diegetic_music**：完整弧线，包含配器、BPM、段落边界的动态变化。**按阶段转折写，不要逐小节详述**。一句话说明风格、BPM、核心乐器，然后描述各阶段边界的变化。目标 400-500 字。示例结构："电子朋克，150BPM。失真贝斯、合成器主音、电子鼓、故障采样。Hook: 稀疏贝斯击打 + 静默。Build (1s 落拍): 完整节拍 kick/snare，3s 弹跳合成器 riff 进入，4s hi-hat 叠加。Climax (6s): 强度峰值 — 锯齿波主音高八度尖叫，双踩鼓，8s 故障分解剥离到打击乐，10s 强力和弦猛烈回归。Freeze (13s): 所有乐器退出，单一持续无人机淡出至 15s 静默。"无则 `N/A`。

---

## 步骤 7 — 输出规则

1. **风格 ≠ 内容**：提取字体**风格**（笔刷、像素、模板）而非文字。如果参考图显示 "REBEL CAT" 贴纸，输出可能用 "WILD SPARK" 以同样的笔刷渲染 — 匹配形式，非内容。

2. **多角色自由**：多个角色图可全部以混剪蒙太奇方式出现在同一支 PV 中。

3. **风格 DNA 精确度**：DNA 中的每个禁止项都出现在风格声明中并在所有镜头中维持。

4. **碎片蒙太奇 = 分开镜头**：细节切换必须拆分 — 每个细节一个镜头（手、鞋、眼睛等）。

5. **H3 字段名称**：精确拼写 — `integrated_multimodal_description`、`overall_soundscape`、`non_diegetic_music`、`subject_definitions`、`summary`、`retention_analysis`、`detailed_description`。

6. **总输出长度**：完整的 Ref2VA 输出（所有字段总和：`subject_definitions` + `summary` + `retention_analysis` + `detailed_description` + `overall_soundscape` + `non_diegetic_music`）**不得超过 5000 字**（中文）。这是硬性上限。策略性分配字数：
   - `subject_definitions`: 250-350 字
   - `summary`: 150-200 字
   - `retention_analysis`: 200-300 字
   - `detailed_description`: 2500-3000 字（主要分配）
   - `overall_soundscape`: 400-500 字
   - `non_diegetic_music`: 400-500 字
   
   **在 `detailed_description` 内部，将所有镜头压缩到每个 25-100 字**：
   - **关键镜头**（角色首次出现、高潮爆发、海报定格）：75-100 字 — 构图、核心动作、主要平面元素、转场
   - **碎片蒙太奇镜头**（手/鞋/配件特写）：25-40 字 — 元素 + 一个贴纸弹出，一句话
   - **过渡/动作镜头**（移动、中间状态）：40-60 字 — 运动路径 + 平面事件
   
   **压缩策略**：大多数镜头只写一句话。只有关键叙事镜头才写两句话。删除：镜头内部的详细时间分解、详尽的配件列表、相机参数散文（"以中速小幅度推进"）、重复的主体特征描述。只写：可见什么、移动什么、弹出什么平面、如何转场。
   
   **压缩示例**："特写蓝指甲手指敲击银链，骷髅戒指可见。猫骷髅贴纸右上弹出。"（32 字）— 而非展开成段落详述每个手指、戒指材质、链条纹理、光照、相机运动和音效提示。
   
   **自查**：写完后统计总输出字数（所有字段）。如果超过 5000 字，优先压缩碎片镜头和过渡镜头。不要压缩关键镜头或音频弧线。

7. **语言**：全英文。原语言仅在 `<d>` 和屏幕文字引号内。

8. **无淡入淡出**，除非风格 DNA 支持。

---

## 内部规划卡（静默）

写之前编译：

```
图片：[N 张图] [角色]
风格 DNA：[色彩] [渲染] [平面设计] [节奏] [禁止项]
模式：[I2VA/FL2VA/L2VA/Ref2VA]
时长：[X秒]
镜头数：[预估 N 个镜头]
风格声明：[1-2 句话]
主体：[<Subject N> 列表]
```
