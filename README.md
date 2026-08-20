# 电影提示词工具盒 · Compile Cinematic Prompt

把一句简单的画面描述扩展成准确、协调、可直接用于图片模型的电影感提示词。

它不是简单堆叠“电影感、8K、高质量”等形容词，而是先锁定主体与场景，再通过直观的视觉方向卡，让用户选择情绪、空间、人物姿态、光线、色彩和成像质感，最后自动翻译成专业摄影语言。

## 能做什么

- 从一句话提取主体、数量、动作、环境和硬约束
- 提供三张差异明确的视觉方向卡
- 把“孤独、怀旧、压迫”等情绪转换为可见的构图与光线证据
- 在精细模式下提供景别、机位、构图和成像介质控制台
- 检查互相冲突的专业术语
- 输出可直接复制到图片模型的完整 Prompt
- 用户明确要求时，在 Prompt 确认后继续生成图片

## 安装

### 方法一：让 Codex 安装

把这个 GitHub 仓库链接发给 Codex，并说：

```text
请安装这个仓库里的 compile-cinematic-prompt Skill。
```

### 方法二：手动复制

克隆仓库：

```bash
git clone https://github.com/kryjhgvhgfrgh-hash/compile-cinematic-prompt.git
cd compile-cinematic-prompt
```

Windows PowerShell：

```powershell
Copy-Item -Recurse .\compile-cinematic-prompt "$HOME\.codex\skills\"
```

macOS / Linux：

```bash
cp -R ./compile-cinematic-prompt ~/.codex/skills/
```

复制后开启一个新的 Codex 任务。如果 Skill 没有立即出现，重新启动 Codex。

## 最简单的用法

```text
$compile-cinematic-prompt 一个人在凌晨的海边等车
```

Skill 会先锁定场景，然后提供三张视觉方向卡，例如：

```text
A｜静谧孤独
B｜海岸悬疑
C｜梦境黎明
```

回复：

```text
C
```

也可以混合或微调：

```text
A+C
A，但整体更暖
B，但不要太黑
```

确认后，Skill 会输出完整电影感 Prompt、方向配方和场景锁定。

## 四种模式

### 1. 简单确认（默认）

只进行一轮视觉方向选择：

```text
$compile-cinematic-prompt 两个女生在雨天车站分别
```

### 2. 直接编译

跳过选择，让 Skill 自动采用推荐方向：

```text
$compile-cinematic-prompt 直接编译：一个老人深夜独自在便利店吃泡面
```

### 3. 精细模式

选择视觉方向后，再确认一次景别、机位、构图和成像介质：

```text
$compile-cinematic-prompt 精细模式：一个男孩站在废弃游乐园
```

### 4. 三个方向

一次获得三套差异明显的完整 Prompt：

```text
$compile-cinematic-prompt 三个方向：雪天，一个女孩站在空旷车站
```

## 生成图片

本 Skill 默认只编写 Prompt。需要出图时，可以在一开始说明：

```text
$compile-cinematic-prompt 精细模式：一个人在凌晨的海边等车，确认后生成16:9图片
```

也可以在拿到最终 Prompt 后回复：

```text
生成图片
```

图片生成能力是否可用取决于当前 Codex 环境。

## 快捷调整

看到方向卡或成图后，可以直接说：

```text
更冷
人物再远一点
增加负空间
不要胶片颗粒
改成固定镜头
更压迫，但不要改变人物数量
```

Skill 会尽量只修改对应变量，保持其他场景事实不变。

## 设计原则

提示词按照以下顺序编译：

```text
主体与数量
→ 动作和人物关系
→ 环境与空间位置
→ 时间和天气
→ 景别与机位
→ 构图和主体尺度
→ 色彩系统
→ 光线与空气介质
→ 材质和成像介质
→ 情绪结果
→ 必要排除项
```

专业术语必须对应一个真实的画面控制变量。Skill 会避免同时使用互相冲突的描述，例如“超广角透视＋长焦压缩”“中央对称＋三分法主构图”或“35mm 胶片＋消费级 DV”。

## 仓库结构

```text
compile-cinematic-prompt/
├── README.md
└── compile-cinematic-prompt/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── cinematic-language.md
        ├── quality-rubric.md
        └── toolbox-ui.md
```

真正需要安装的是内层的 `compile-cinematic-prompt/` 文件夹。仓库根目录的 README 只用于 GitHub 使用说明。

