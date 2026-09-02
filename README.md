# ClipShot

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

把剧本、分镜脚本和人物或场景设定，转化为可拍摄的电影级九宫格分镜图与时间线镜头表。

本仓库是符合 [Agent Skills](https://agentskills.io/specification) 规范的独立 Skill：`cinematic-storyboard-design`。适用于 [Cursor](https://cursor.com/docs/skills)、Codex 及其他兼容该规范的 Agent。本轮发布不含案例图片。

## 它做什么

Skill 先读懂叙事、人物关系、空间和交付用途，再拆镜头，而不是直接出成片或概念海报。默认产出：

- 一段极简创作理解：核心冲突、情绪曲线、空间关系和视觉母题
- 一张严格 3×3 的九宫格制作型分镜图
- 一张带时间码的分镜解读表
- 必要时补充特殊镜头、转场和连续性提示

默认提供 A/B 两套镜头方案：剧情节拍和连续性锚点相同，观看立场、构图、景别、剪辑、运镜或转场至少三项形成整组差异。用户明确只要一套时，按用户要求执行。

## 适用与不适用

**适用**

- 叙事影片、广告、MV、短剧的镜头拆解
- 画面调度、运镜、转场和单格放大
- 导演、摄影、动作部门可读的制作型分镜

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
使用 cinematic-storyboard-design 将我的剧本设计成两套镜头语言差异明确的九宫格电影分镜，并提供时间线镜头表。
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

已有分镜脚本是创作约束，不是不可改的答案。参考图只提炼造型、空间、材质、色彩或线稿语言。

**输出顺序**

1. 必要时：缺失信息确认，或长剧本拆分建议
2. 一段简短创作理解
3. 九宫格分镜图
4. 时间线分镜解读表
5. 特殊镜头、转场与连续性提示

视觉语言是制作型故事板：钢笔或墨线结构速写，大块灰阶马克笔区分层次，克制的红色动线标记人物路径、视线或镜头运动。详细说明放在图后的时间线表，不堆在格子里。

## 仓库结构

```text
clipshot/
├── SKILL.md                         # 主流程：输入确认、拆分、双方案、出图与交付
├── LICENSE                          # MIT
├── README.md
├── agents/
│   └── openai.yaml                  # Codex / ChatGPT 展示与默认触发句
└── references/
    ├── cinematic-language.md        # 镜头语言：景别、轴线、运镜、转场、差异检查
    ├── visual-production.md         # 九宫格规格、提示词、红线与视觉检查
    └── deliverable-schema.md        # 创作理解、时间线表、拆分建议、追问话术
```

Agent 先读 `SKILL.md`，再按任务按需读取 `references/`，避免一次装入全部细节。

## 协议

本仓库以 [MIT License](LICENSE) 发布。你可以自由使用、复制、修改、合并、发布和再分发，只需保留版权与许可声明。

## 后续

案例图片将另作补充，不包含在本轮发布中。每次请求只依据当次提供的剧本、设定和参考，不迁移其他项目的时代、角色、地点、画幅或视觉设定。
