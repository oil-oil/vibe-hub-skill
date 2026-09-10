<p align="center">
  <img src="./assets/readme/hero.svg" alt="让 Vibe Coding 表达更准确" width="100%">
</p>

在编程交流中识别专业术语，提供通俗解释和可追溯的术语链接，帮助准确表达需求。

它不提供学习路线、课程计划或本地练习，也不会把一句简单需求扩展成教程。

## 一分钟安装

把下面这段话完整发给你的 Agent：

```text
https://github.com/oil-oil/vibe-hub-skill

帮我安装这个仓库里的 skills/vibehub Skill。
```

## 两个核心功能

### 1. 把模糊描述改成准确需求

你可以说：

```text
把这句话改成更准确、可以直接发给 Agent 的需求：
这个按钮鼠标放上去变个色，点下去也要有一下反馈。
```

Skill 会保留原意，并把需求改成类似这样：

```text
为按钮补充 Hover 状态和 Active 状态，并使用 Transition 让状态变化更自然。
```

找到明确术语时，第一次出现会直接链接到 VibeHub。Skill 不会擅自增加框架、组件库、参数或实现方案。

Skill 不会把整句需求直接丢给搜索接口。它会先结合当前语境推断候选术语，再用一次批量查询验证名称和链接；高置信度时只查一个，存在歧义时最多比较三个。

### 2. 主动提示相关术语

你不需要先问“这个叫什么”。即使 Agent 已经完成了一部分代码，你又追加了一句口语化需求，Skill 也会在继续开发的同时指出最相关的术语：

```text
鼠标放到这个下载按钮上面时，加一个小提示。
```

Skill 会提示：

```text
已为下载按钮添加文字提示（Tooltip）：悬停或键盘聚焦时显示“下载”。
```

术语的作用是让沟通更准确，不是展示词汇量。没有真正有帮助的术语时，Skill 不会硬塞链接。

## 看不懂 Agent 回复时

把 Agent 的原话贴出来即可：

```text
Agent 说这里要做乐观更新和错误回滚。
请结合当前任务用大白话解释，并告诉我接下来该怎么回复。
```

VibeHub 会选出最影响下一步判断的概念，解释它在当前任务中指什么、负责什么，以及一个容易混淆的边界。它不会逐词翻译整段回复，也不会自动开始课程。

## 可以这样问

| 你想做什么 | 可以直接对 Agent 说 |
| --- | --- |
| 把需求说准确 | `把这句话改成更准确、可以直接发给 Agent 的需求：我想让卡片鼠标放上去浮起来一点。` |
| 主动获得术语提示 | `听我描述需求时，主动告诉我最值得使用的 1–3 个术语，不要等我问“这叫什么”。` |
| 看懂 Agent 的说法 | `Agent 说这里需要做状态管理。结合当前页面用大白话解释，并告诉我接下来该问什么。` |
| 给术语加链接 | `把这段需求里的关键术语标出来，给第一次出现的术语加上 VibeHub 链接，并用一句话解释。` |

## 工作原则

- 先给可以直接使用的结果，再解释术语
- 保留用户原意，不擅自增加实现细节
- 每次最多提示 1–3 个真正相关的术语
- 只使用 VibeHub 返回的页面链接，不伪造地址
- 用户表达可能模糊时，主动指出准确术语，但不打断当前任务
- 用户表达已经准确且没有可补充的术语时，不硬加术语教学

## 数据与隐私

- 术语查询只发送经过程序脱敏的简短描述。
- 常见密钥、网址、邮箱、本地路径和代码块会在发送前移除。
- 无法访问 VibeHub 或没有明确匹配时，Skill 会明确说明，不会伪造术语和链接。
- Agent 已经看到的项目上下文，仍受所用产品和模型服务商的隐私设置约束。

## 开发

需要 Node.js 20 或更高版本。

```bash
npm test
```

连接本地 VibeHub 网站：

```bash
node skills/vibehub/scripts/vibehub.mjs resolve \
  --query "Tooltip" \
  --query "Hover" \
  --compact \
  --site-url http://localhost:3100
```

<details>
<summary>仓库结构</summary>

```text
skills/vibehub/
├── SKILL.md
├── agents/openai.yaml
├── scripts/vibehub.mjs
└── vibehub.config.json
```

</details>

术语内容由 [VibeHub](https://vibe-hub.org/) 网站维护；这个仓库只保留表达规则和术语解析器。

## 许可

[MIT](LICENSE)

## 配置、依赖与使用边界

需要 Node.js 与联网能力；运行 bundled 术语解析脚本即可，无账号或 API Key 配置。

只查询脱敏后的短术语，不发送源代码、客户信息或整段需求；引用解析器实际返回的词条 URL，不拼接链接。

使用示例：

```text
鼠标放到按钮上显示一行说明，这叫什么？
```

## GitHub 安装

把 [仓库地址](https://github.com/oil-oil/vibe-hub-skill) 交给 Agent，要求按 README 安装；也可运行：

```bash
npx skills add oil-oil/vibe-hub-skill
```

安装后由宿主重新加载 Skill。
