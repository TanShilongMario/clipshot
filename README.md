# ClipShot

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

把剧本、分镜脚本和人物或场景设定，转化为可拍摄的电影级九宫格分镜图与时间线镜头表；分镜完成后，再由用户选择是否依据分镜与素材制作独立的成片关键帧。

本仓库是符合 [Agent Skills](https://agentskills.io/specification) 规范的独立 Skill：`cinematic-storyboard-design`。适用于 [Cursor](https://cursor.com/docs/skills)、Codex 及其他兼容该规范的 Agent。`examples/` 里放了案例镜头表和生成提示词；分镜图等素材图片默认不入库，只留在本地。

## 它做什么

Skill 先读懂叙事、人物关系、空间和交付用途，再拆镜头，而不是直接出成片或概念海报。默认产出：

- 一段极简创作理解：核心冲突、情绪曲线、空间关系和视觉母题
- 一张严格 3×3 的九宫格制作型分镜图
- 一张带时间码的分镜解读表
- 必要时补充特殊镜头、转场和连续性提示
- 分镜交付后的关键帧制作询问；仅在用户同意并确认素材映射后输出成片关键帧

默认输出一套导演推荐方案。仅在探索阶段、用户明确要求，或同一剧情存在两种都成立的观看立场时，提供 A/B 双方案。双方案的剧情节拍和连续性锚点相同，观看立场、构图、景别、剪辑、运镜或转场至少三项形成整组差异。

## 适用与不适用

**适用**

- 叙事影片、广告、MV、短剧的镜头拆解
- 画面调度、运镜、转场和单格放大
- 动作摄影：荷兰角、黄金分割、框内切分、极端切边，以及连续运镜的起止节点
- 导演、摄影、动作部门可读的制作型分镜
- 依据已确认分镜和用户人物、场景、美术素材制作独立成片关键帧

**不适用**

- 直接生成写实成片
- 普通概念海报或精致插画
- 把长剧本硬塞进一个九宫格

## 安装

安装目录名必须是 `cinematic-storyboard-design`，以便与 Skill 的 `name` 字段一致。

### Cursor 用户级

```bash
git clone https://github.com/TanShilongMario/clipshot.git cinematic-storyboard-design
```

将克隆得到的文件夹放到：

- `~/.cursor/skills/cinematic-storyboard-design`
- 或 `~/.agents/skills/cinematic-storyboard-design`

Windows 常见路径：

```text
%USERPROFILE%\.cursor\skills\cinematic-storyboard-design
```

### Cursor 项目级

把本仓库复制为项目内的：

```text
.cursor/skills/cinematic-storyboard-design
```

或：

```text
.agents/skills/cinematic-storyboard-design
```

### 从 GitHub 导入

在 Cursor 中打开 Customize → Rules → Add Rule → Remote Rule (Github)，填入：

```text
https://github.com/TanShilongMario/clipshot
```

### 其他兼容 Agent

仓库根目录包含 `SKILL.md`。Codex 可使用 `agents/openai.yaml` 中的展示名和默认触发句。

## 使用

在对话中点名本 Skill，并提供剧本或本次要处理的片段。也可以直接使用：

```text
使用 cinematic-storyboard-design 将我的剧本设计成一套镜头语言明确的九宫格电影分镜，并提供时间线镜头表。
```

生成前必须确认这三项，缺一项会先追问：

1. 剧本正文或本次明确片段
2. 成片用途与单格画幅：横屏 `16:9`，或竖屏 `3:4` / `9:16`
3. 本轮覆盖范围：场次、时长或起止段落

人物与场景设定、时代地点、基调、目标时长、禁忌和参考作品属于强烈建议项。长剧本无法被一个九宫格清楚承载时，会先给出拆组建议，确认范围后再出图。

## 输入与输出

**输入**

1. 剧本与整体设定
2. 剧本加已有分镜脚本
3. 上述内容再附人物、服装、道具、场景或视觉参考图

已有分镜脚本是创作约束，不是不可改的答案。写实参考图默认只作连续性，不继承摄影渲染风格。

**输出顺序**

1. 必要时：缺失信息确认，或长剧本拆分建议
2. 一段简短创作理解
3. 九宫格分镜图
4. 时间线分镜解读表
5. 特殊镜头、转场与连续性提示
6. 询问是否继续制作成片关键帧
7. 用户同意后：确认目标镜号与素材映射，再输出独立关键帧

视觉语言是制作型故事板：钢笔或墨线画结构，马克笔或色块画光的位置和形态，不能交纯线稿。人物以结构人体为主，先读机位和姿态；近景和特写可有简单五官动态，手部姿势必须清楚。必须剔除照片、成片和角色插画完成度，避免下游再创作被锁死。生成后先检查实际图像；未过 GRID / STYLE / CONTINUITY / READABILITY / MOTION 门禁，以及动作或非常规镜头适用的表现力检查不得交付。详细说明放在图后的时间线表，不堆在格子里。

分镜与成片关键帧严格分阶段：分镜只决定运镜、机位、构图、调度和光影结构；用户当次提供并确认的人物、服装、道具、场景与 STYLE 素材决定关键帧的最终美术呈现。分镜的结构人体、纸面、墨线、马克笔灰阶、红色箭头、边框和镜号不能被误当作成片风格。用户未明确同意前不自动生成关键帧；素材或风格存在歧义时先让用户选择，不擅自混合或补足。

动作场面同时设计身体受力与摄影，按节拍选择蓄势、爆发和停顿，不固定套用景别顺序。特殊构图说明主体位置、裁切和空间锚点；特殊运镜说明起点、动作触发、路径、速度变化和落点。同一连续镜头可用 a/b/c 运镜节点占用相邻格，注明无剪切，镜头总时长仅计算一次；这些节点仍是分镜，不是成片关键帧。九宫格保持等大，格内空间可以采用非常规切分。

## 仓库结构

```text
clipshot/
├── SKILL.md                         # 主流程：输入确认、拆分、双方案、出图与交付
├── LICENSE                          # MIT
├── README.md
├── agents/
│   └── openai.yaml                  # Codex / ChatGPT 展示与默认触发句
├── examples/
│   ├── 文字分镜.docx                # 案例剧本
│   ├── market-chase/                # 菜市场追逐：镜头表与生成提示词
│   └── storyboards/                 # 本地分镜图目录，图片不入库
└── references/
    ├── cinematic-language.md        # 镜头语言：景别、轴线、运镜、转场、差异检查
    ├── action-cinematography.md     # 动作受力、非常规构图、运镜路径与表现力审查
    ├── visual-production.md         # 九宫格规格、提示词、红线与视觉检查
    ├── keyframe-production.md       # 分镜完成后的独立成片关键帧、素材映射与检查
    └── deliverable-schema.md        # 创作理解、时间线表、拆分建议、追问话术
```

Agent 先读 `SKILL.md`，再按任务按需读取 `references/`，避免一次装入全部细节。

## 协议

本仓库以 [MIT License](LICENSE) 发布。你可以自由使用、复制、修改、合并、发布和再分发，只需保留版权与许可声明。

## 后续

案例图片仍只保留在本地，不随仓库发布。每次请求只依据当次提供的剧本、设定和参考，不迁移其他项目的时代、角色、地点、画幅或视觉设定。
