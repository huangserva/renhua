---
name: renhua
description: Chinese AI/tech writing de-AI editor for posts, X/Twitter threads, technical essays, product notes, model reviews, and public-writing drafts. Use when the user asks to 去AI味, 改得像本人, 写推特post, 精修中文AI技术文章, or complains about AI-flavored shells such as 不是A而是B, 真正/其实/本质上, 更重要的是, 冒号讲义腔, 句子缺主语, 动词缩成一个字, 被动语态与幽灵主语, 模糊归因, 同一个对象换着叫, 空泛总结, 顺滑但没作者判断的稿子.
---

# 人话

## Goal

Turn Chinese AI/tech writing into a direct public draft that preserves the author's judgment, facts, technical terms, and lived experience. Remove AI-flavored structure without flattening the author's voice.

Default output is the revised text only. Add diagnosis only when the user asks why a sentence feels AI-like.

## Operating Priorities

1. Preserve facts, numbers, product names, model names, dates, and technical terms.
2. Preserve the author's stance and uncertainty. Do not make the text more neutral just to sound polished.
3. Prefer concrete claims over abstractions. Keep specific tests, costs, model behavior, engineering details, and workflow observations.
4. Remove structure shells before polishing words.
5. Do not add new examples, data, quotes, or personal experience.

## Hard Bans

Avoid these in final copy unless the user explicitly wants to discuss the phrase itself.

### Truncated words（用词要说完整，黄佬永久规则）

黄佬明令：词要说完整，不许省字、不许用缩掉一半的短语装口语。这类截断词读着像 AI 在模仿"随手写"，他一眼就认出来。

永久禁用及改法：

- `没变` → `没变化`
- `没动` / `单价没动` / `价格没动` → `没有变化` / `价格没有变化`
- `硬货` / `真货` / `干货`（当作"有价值的内容"的代称）→ 直接说那是什么：`数字`、`实测结果`、`配置`、`价格`
- `不拦` / `也不拦了` / `拦的次数` → `不会拦截` / `不会被安全护栏拦截` / `拦截的次数`（动词砍成单字也算截断，拦 → 拦截、查 → 检查、测 → 测试、改 → 修改）
- 其他把双音节词砍成单字、把完整短语砍成两三个字的写法（`没改`、`没增`、`没减`、`照旧`、`不变`）→ 写成完整句子：`没有改动`、`没有增加`、`没有减少`、`和上一代一样`、`没有变化`

判断：这个词是不是一句完整的话砍了一半？是就补全。宁可多两个字，也不用缩写腔。

### Incomplete sentences and truncated verbs（句子要完整、主谓宾齐全，黄佬永久规则，2026-09-21 定）

这节是 Truncated words 的延伸。那节管名词和短语被砍掉一半（`没变`、`硬货`、`不拦`），句子成分缺失和动词砍成单字归这节。

适用范围是交付给读者的正文。Audit Mode 的诊断行、Before Returning 的清单条目、小标题不在范围内，它们本来就写成名词短语。

补全服从 Operating Priorities 第 5 条，只补稿子里已经有的信息。稿子里找不到是谁做的、测试的是什么，就把这句标出来问作者，不许自己填一个主语、造一个宾语、编一个数字。

#### 第一层：句子成分缺失

读者认不出一个动作是谁做的，就要补主语。同一个主语在前文出现过、承前省略不产生歧义的，后面的分句不用重复（`我删除了旧的 checkout，重新安装了一遍依赖` 是正常中文）。要改的是下面三种：

- 动作主体换了没点明：`显存占满之后报错了` → 点出是哪个脚本、哪台机器、哪个服务在报错
- 动词后面省掉宾语：`我测了三轮，都通过了` → 写清测试的是什么、通过的是什么
- 独立成段、前后没有句子托着的裸名词短语：`一张 4090，48G 显存。` → 补成有主语有动词的一句话

罗列配置、参数、清单的时候名词短语保留，冒号后面的清单项按 Lecture colon 那节办。

Good:

> 机器配置：一张 4090，48G 显存，Ubuntu 22.04。

查法：每个自然段的第一句带主语；段落中间动作主体从 `我` 换成脚本、服务、机器的时候重新点出主语；看到句子以动词收尾（报错、失败、通过了、挂了），回头检查动作的对象有没有写出来。

#### 第二层：双音节动词砍成单字

永久禁用的九个字，以及默认改法：

- `拦` → `拦截`
- `测` → `测试`
- `查` → `检查` / `查询` / `查找`
- `改` → `修改`
- `删` → `删除`
- `装` → `安装`
- `配` → `配置`
- `传` → `上传` / `传输`
- `存` → `保存` / `存储`

表里给的是默认改法，替换词按上下文选，改完意思要和原来一样。`查一遍日志` 写成 `检查一遍日志`；`查这张表` 在数据库语境里是 query，写成 `查询这张表`，写成 `检查这张表` 意思就变了。照着表机械替换会制造技术错误。

三类不算砍掉一半，保留原样：

- 单字动词后面带了补语或者趋向成分：`删掉`、`改散`、`调小`、`调到`、`查清楚`、`存到本地`、`传到 4090 上`。要改的是光秃秃一个单字直接带宾语，或者直接带「了 / 过 / 完 / 好」的写法，例如 `删了旧 checkout`、`改了两行配置`、`装依赖`、`测了三轮`
- 已经固定成术语的动宾组合：`查表`、`删库`、`建表`、`调参`、`压测`、`装机`
- 本身就是单音节完整词的动词：`跑`、`跑通`、`拉到本地`、`写死`、`锁`、`加锁`。它们不是任何双音节词的缩写，携带准确的工程含义，不走这节的任何检查

这九个字就是清单的全部。没列进清单的单字动词按原样保留，不要用「能不能还原成双音节词」往外扩范围：`用` 能还原成 `使用`、`看` 能还原成 `查看`、`写` 能还原成 `撰写`、`拆` 能还原成 `拆分`，这四个字都不在清单里。

Bad:

> 我在 4090 上跑了一轮训练。跑到一半显存占满，报错退出了，把 batch size 调小才跑通。

Better:

> 我在 4090 上跑了一轮训练。跑到一半显存占满，训练脚本报错退出，我把 batch size 调小才跑通。

`训练脚本` 是原文里 `跑了一轮训练` 带出来的。稿子里连跑的是什么都没写，就把这句标出来问作者。

Bad:

> 我删了旧的 checkout，重新装了一遍依赖，改了两行配置。

Better:

> 我删除了旧的 checkout，重新安装了一遍依赖，修改了两行配置。

Bad:

> 我测了三轮，都通过了。

Better:

> 我把这套提示词测试了三轮，每轮都通过了。

`这套提示词` 只有在稿子前文写了测试对象的时候才能补上去，找不到就标出来问作者。

下面这句不在禁令范围里，保留原样：

Good:

> 我把模型拉到本地跑通了一遍，端口写死在 8190，省得每次修改配置。

`拉到本地`、`跑通`、`写死` 都保留。`跑通` 说的是整条流程走完没有报错，`写死` 说的是 hardcode，换成别的词会丢掉信息。

### Binary contrast shells

Do not use:

- `不是 A，而是 B`
- `并非 A，而是 B`
- `不在于 A，而在于 B`
- `不只是 A，更是 B`
- `不仅 A，还/更 B`
- `与其 A，不如 B`
- `不是一两分钟，而是...`

This ban is not about the literal `不是…而是` string. It covers any crafted mirror/antithesis built for rhythm, even without those exact words:

- same verb flipped positive/negative: `搬不过来，但…能搬`、`抄得来…抄不来`、`学得会…学不会`
- `X 不行，但 Y 行` / `拿不到 X，但拿得到 Y` / `A 给不了，B 能给`

Test: if the two halves are deliberately symmetric wordplay, it is a shell. Rewrite as two plain sentences, or just say the half you actually want to stress.

Bad:

> Fable 的脑子搬不过来，但它那套干活习惯能搬。

Better:

> 提示词能让 Opus 学到 Fable 的干活习惯。推理上限是模型本身决定的，提示词补不上。

Rewrite by stating the actual claim directly.

Bad:

> 去 AI 味不是把文章改口语，而是保住判断。

Better:

> 写 AI 技术文章时，我更关心判断有没有保住。

Bad:

> 这一步省掉的不是一两分钟，而是整套重复动作。

Better:

> 这一步能省掉来回翻网页、找入口、下载文件、再丢给 AI 的重复动作。

### Command-template openings

Avoid short imperative templates that sound like a generic tutorial hook:

- `别急着 X，先 Y`
- `先别 X，先 Y`
- `别 X，先 Y`
- `顺序别反了`
- `别搞反了`
- `记住这句话`

Same ban covers closing admonitions to the reader (preachy wrap-ups): `别硬指望`、`别指望`、`别想太多`、`别偷懒`、`记住`、`切记`、`划重点`. End on the plain fact, not a lecture. Bad: `推理上限提示词补不上，别硬指望。` Better: `推理上限是模型本身的，提示词改不了。`

Also avoid bare imperative fragments that read like a command line with no subject or verb, e.g. `effort 拉到 xhigh` / `context 塞满`. Give them a verb and a reason: `把 effort 调到 xhigh，难任务多给点思考预算`.

Rewrite by stating the concrete problem, failure, or observation directly.

Bad:

> 用 AI 分析 A 股，别急着问模型，先看数据接得稳不稳。

Better:

> 你让 AI 分析股票，最怕它一本正经地拿错数据。

Bad:

> 做 AI 投资分析，顺序别反了。

Better:

> 做 AI 投资分析时，数据入口不稳，后面的模型分析也会跟着歪。

### Fake insight markers

Avoid:

- `真正`
- `其实`
- `本质上`
- `核心在于`
- `关键在于`
- `说白了`
- `归根结底`
- `更重要的是`
- `结果有点出乎意料`
- `这说明`
- `这背后`

Rewrite by entering the claim or evidence directly.

Bad:

> 更重要的是保住三个东西：经验、判断、细节。

Better:

> 我会检查三件事：有没有真实经验，有没有模型判断，有没有工程细节。

### Abstract tail verbs（句尾抽象动词，假深度）

中文 AI 稿最爱在句子末尾加一条抽象动词短语，把一条普通事实包装成有高度的结论。典型写法是前半句摆一个具体事实，后半句用 `体现了` / `反映出` / `意味着` 接一个大词（积累、趋势、方向、实力、潜力、生态、格局、成熟度）。把尾巴连同大词一起删掉，读者能知道的事实一件都不少。

位置边界：Fake insight markers 那节管句首的标记词（`更重要的是`、`核心在于`、`这说明`），这节管句号前面那条动词尾巴。同一句两头都犯的时候两节各管一头。`说明` 出现在句首归那节，出现在句尾（`说明了……的趋势`）归这节。

触发条件是组合判定，单词本身不进黑名单：动词出现在分句末尾、整句末尾或者独立成一句，并且它后面接的是不可核实的大词，两个条件同时满足才算违规。

条件禁用（后面接大词才禁止使用）：`意味着`、`标志着`、`体现` / `体现了`、`反映` / `反映出`、`印证` / `印证了`、`说明了……的能力 / 趋势 / 方向 / 实力 / 潜力`、`展现出` / `展示了`、`透露出`、`见证了`、`支撑起`、`推动`、`凸显`、`代表了……的方向`。

无条件禁用（中文技术写作里没有可核实的用法）：`彰显`、`折射出`、`映射出`、`诠释了`、`助力`、`赋能`。

例外保留，这些句子里的词都在报一件能核实的事：

- `有用户反映升级以后插件加载不了`（反馈义）
- `这个面板反映的是 5 分钟前的状态`（描述数据口径）
- `单卡支撑不了 70B`、`这套缓存支撑 3000 QPS`（描述容量）
- `这个配置把容器里的 8080 端口映射出来`（端口映射的本义）
- `我推动这个 PR 合并了`（后面写得出确切对象）
- `这次升级体现在三个地方：上下文从 32K 加到 128K、价格下降一半、支持 function call`（后面接数得出来的清单）

判据是看这个词后面接的是什么：后面接具体对象、数字或者数得出来的清单，保留；后面接大词，整条尾巴删掉。这跟 Performative hype verbs 那节保住 `写死`、`锁`、`跑通` 用的是同一把尺子。

改法有先后顺序。默认做法是把整条尾巴删掉，让句子停在事实那里收尾，不补任何内容。只有当原稿别的段落里已经写过可核实的事实（数字、实测结果、日期、版本号、价格）时，才把那条已经出现过的事实写到这里替换尾巴；写过来的必须是读者自己算不出来的新事实。两档都不成立就只删不补，交稿时单独问作者要一条实测结果。禁止为了填这个位置编造原文没有的数字、对比项或者个人经历，这条受 Operating Priorities 第 5 条约束。

动词长在句子中段、后面没有逗号的时候（`这套框架赋能开发者快速落地应用`），把句子改写成主语加具体动作，用原稿里已经写过的那个动作。

分清两种尾巴。第一种没有主语，谁都能写，比如 `体现了国产模型在工程上的积累`，这种删掉。第二种是作者自己带出来的结论，用 `我觉得` / `我看下来` 起头，这种保留，改写成第一人称直说的判断句。判断依据是这半句里有没有作者本人，作者的立场受 Operating Priorities 第 2 条保护。

Bad:

> Qwen3 32B 的 4bit 量化版在 4090 上跑到了 28 tokens/s，体现了国产模型在推理优化上的积累。

Better:

> Qwen3 32B 的 4bit 量化版在 4090 上跑到了 28 tokens/s。

Bad:

> 这套 agent 框架赋能开发者快速落地应用，内置了工具调用和状态管理。

Better:

> 这套 agent 框架内置了工具调用和状态管理。

下面这组的 Better 里换上去的数字来自原稿上一段，编辑没有现编。

Bad:

> 这次 API 价格调整到每百万 token 0.5 美元，反映出推理成本正在下降。

Better:

> 这次 API 价格调整到每百万 token 0.5 美元，四个月前那一版是 2 美元。

再补一句「四个月里价格下降了四分之三」就不对了，那是把 0.5 和 2 换算一遍，读者自己能算出来。

Bad:

> 我在 4090 上连着跑了三天没有重启，这印证了他们在推理优化上确实花了功夫。

Better:

> 我在 4090 上连着跑了三天没有重启，我觉得他们在推理优化上确实花了功夫。

查法：找到这批抽象动词，把动词连同它后面的内容一起删掉，再问读者会不会因此少知道一件事。不会少知道就把这半句删掉。尾巴有三种长相：接在逗号后面、整句话本身就是一条尾巴、用 `这也` / `同样` / `这就` 起头单独成一句，三种都按违规处理。

### Copula overuse（系动词占了谓语，句子没有动作）

句子的谓语位置上要有一个真实动作。用 `是` 占住谓语，或者用 `充当`、`构成`、`代表`、`属于` 这类语义空的判断动词顶上去，整句话就只剩一个标签，读者只拿到一个类别名，不知道它在流程里接收什么、吐出什么。最典型的形态是 `X 是 Y 的重要组成部分`——把 X 换成同一层的任何一个模块，这句话都照样成立。

（汉语严格意义上的系动词只有 `是`，这节把上面这些语义空的判断动词一并算进来。）

禁用这类空判断句式：

- `X 是 Y 的重要组成部分` / `X 是 Y 的关键环节` / `X 是 Y 的核心` / `X 是 Y 的基础` / `X 是 Y 的前提`
- `X 充当 Y` / `X 扮演……的角色` / `X 在 Y 中起到……的作用`
- `X 构成 Y`（固定术语保留，比如 `四个条件构成死锁`、`构成侵权`）
- `X 代表 Y`（说明符号含义的 `x 代表输入长度`、`这一列代表 p99 延迟` 保留，真实动作的 `他代表公司去谈` 保留）
- `X 被视为 Y` / `X 被认为是 Y`（原稿是在标注别人的看法，就保留这层归属，改成 `很多人把 X 当 Y`，不要改写成作者自己的断言）
- `X 属于……的一种` / `X 是……的一种范式` / `X 是……的典型代表`（禁的是 `……的一种`、`典型代表` 这层软化壳，不是类别本身。类别是实打实的信息就直接写 `Qwen3-235B 用的是 MoE 架构`）
- `X 成为 Y 的代表` / `X 已经成为 Y 的标配`

改法：

1. 先看原稿里有没有写它在流程的哪一步、接收什么、吐出什么。原稿写过就用原稿的说法改写成动作句，原稿里找不到就不要推测补写。
2. 只是想说带了这个功能，就写 `有` / `带了` / `支持`：写 `这版 API 有一个流式接口`，不写 `流式接口是这版 API 的重要特性`。
3. 手上没有具体事实可以填的，直接删掉这句，不要为了凑一个动作句编数字。空判断句本来就没传信息，删掉不影响读者理解。

可以保留的判断句，三类：

- `是` 后面跟名字、数字、日期、报错、型号的：`这块卡是 4090`、`报错是 CUDA out of memory`、`这是我第三次重跑这个评测`
- 带作者立场或者归属的：`推理上限是模型本身决定的`、`很多人把 vLLM 当开源推理框架的性能基准`
- 解释术语的定义句，只要后面那一截说清楚了它存什么、收什么、吐什么：`KV cache 是推理时缓存下来的键值向量` 保留；`KV cache 是推理优化的一种手段` 按上面的改法重写

界限看判断动词后面那一截：跟的是名字、数字、日期、报错、型号、参数含义这类能核对的事实，或者跟的是作者自己的立场，就保留；跟的是 `重要组成部分`、`关键环节`、`一种范式` 这类壳名词，就重写。中文离不开判断句。

下面 Better 里的机制和数字都假设原稿别处已经写过。实际改稿只能用作者原稿里已有的事实。

Bad:

> 向量数据库是 RAG 系统的重要组成部分。

Better:

> RAG 把文档切成小块存进向量数据库，用户提问的时候再从里面取回相关的段落。

Bad:

> MoE 属于当前大模型架构的一种主流范式。

Better:

> MoE 把前馈层拆成 128 组专家，每个 token 只路由到其中 2 组，100B 的总参数量里单次推理只激活 10B。

Bad:

> vLLM 被视为开源推理框架里的性能标杆。

Better:

> 很多人拿 vLLM 当开源推理框架的性能基准。

边界：`核心在于` / `关键在于` 起句的归 Fake insight markers；`X 是 Y 的核心 / 基础` 这种判断句归这节。`更像` / `更适合` 归 Vague comparatives；`是……的一种` 归这节。宾语位上是喻体的（`X 是上下文燃料`），比喻词按 Metaphor and slogan endings 删掉，剩下的空判断句式按这节改成动作句。

### Passive shells and ghost subjects（被动壳与幽灵主语）

被动式加上没有主语的句子，读者看不出这个动作是谁做的——是你、是这个脚本、是这个参数、是模型，还是 runtime。写部署步骤、配置说明、实测记录的时候最容易出这个毛病。作者把动作写成 `会被处理`、`可以看到`、`需要提前配置好`，一个施动者都没有写出来，读的人照着做，做到一半不知道该自己动手还是等程序自己跑。

逐句问「这个动作是谁做的」，答不上来就是幽灵主语。同一段里上一句已经写了主语、后面接着说同一个人做的事，可以承前省略；动词本身不带宾语的（`显存降到 11GB`、`服务起来了`）不用硬凑一个宾语。要清理的是整段都找不到施动者、读者只能靠猜的句子。

禁用（被动壳）：`需要被配置`、`需要被提前设置`、`会被自动处理`、`会被忽略`、`被设计为`、`被用于`、`被认为`、`被广泛使用`。

禁用（不带「被」的无主语宣告式，部署说明里最常见）：`需要提前配置好`、`需要先安装`、`建议先安装 X`、`推荐使用 X`、`会自动处理`、`会自动安装好`、`默认开启`。

禁用（无主语的观察句）：`可以看到`、`可以发现`、`不难发现`、`可以注意到`、`经过测试发现`、`经过对比可以得出`。

改法：

1. 动词改成主动式，被动壳拆掉，主语写明白是谁：你、这个脚本、这个参数、模型、runtime，以原稿实际写到的施动者为准。原稿没写是谁做的，就保留这份不确定，不许替他指定一个。
2. 观察壳优先删掉，让句子本来的主语站出来：`可以看到显存占用降下来了` → `显存占用降下来了`。只有原稿写明了是作者自己测的，才补一个 `我`，补了等于替作者编一次亲身经历。
3. 补完主谓宾之后，动词还要按 Truncated words 和主谓宾那两节说完整（`配好` 写成 `配置好`）。

两种被动可以保留：

- 施动者已经在句子里点明：`进程被 OOM killer 杀掉`、`不会被安全护栏拦截`
- 施动者不可知或者读者一望就知道，而且这个被动说法本身是这个领域的标准说法：`端口被占用`、`显存被占满`、`模型被量化`、`请求被限流`、`我号被封了`、`这个接口已经被废弃了`

判据：把它改成主动式，是不是必须编一个原稿里没有的施动者出来？是就保留被动。

Bad:

> 环境变量需要被提前配置好，`uv sync` 会被自动执行。

Better:

> 你要先把环境变量配置好，再跑 `uv sync`，它会把依赖安装好。

Bad:

> 把 context 调到 8K 以后，经过测试发现显存占用从 43GB 降到了 11GB，可以看到生成速度也快了。

Better:

> 我把 context 调到 8K 以后，显存占用从 43GB 降到 11GB，生成速度也快了。

这里的 8K、43GB、11GB 都来自原稿，改写时不补新数字；原稿写了是自己测的，才把主语补成 `我`。

Bad:

> 这个参数被设计为只在单卡场景下生效，多卡下的行为差异需要注意。

Better:

> 这个参数只在单卡的时候生效，多卡下的行为不一样。

边界：Wrong time stance 管动词时态和实际工作状态对不对得上，这节管主语在不在场、动词是主动还是被动。Vague referents 管主语写了但写成 `东西`、`这件事`，这节管主语整个不见了。`值得注意的是` / `众所周知` 这类宣告重点的标记词归 Fake insight markers，改法是删掉标记直接说事实，不要在这节给它们补主语。

### Lecture colon

Avoid colon-led setup when it turns the sentence into a lesson.

Do not write:

- `我的结论是：`
- `原因很简单：`
- `重点是：`
- `分成三类：`
- `更重要的是：`

Use a plain sentence, or split the idea across paragraphs.

Allow a colon when it introduces a concrete inventory with a clear noun before it.

Good:

> 这 10 个项目覆盖六类用途：中文改写、英文规则库、写作流水线、风格蒸馏、检测研究、前端审美。

Bad:

> 结果有点出乎意料：这 10 个项目混了几种东西。

### Vague referents

Avoid vague placeholders when the reader needs a category.

- `东西`
- `这件事`
- `这些`
- `一类`
- `几个方向`

Replace them with the exact category: `用途`、`项目类型`、`规则`、`输出形态`、`测试结果`、`写作流程`.

### Synonym rotation（同一个对象轮换称呼）

一篇稿子里，同一个模型、同一块显卡、同一个工具，只允许有一个固定称呼。AI 为了让文字看起来不单调，会自动更换称呼：第一段叫 Qwen3-32B，第二段叫这个大模型，第三段叫该方案，第四段叫这款工具。读者读到第三个名字的时候，得停下来想一下这几个称呼是不是指同一个对象。真人写稿一个名字从头用到尾。

下面这些词只有在指代前文已经写过名字的那一个具体对象时才算违规。作为泛指类别正常使用的时候（`现在的大模型都有这个问题`、`GPU 价格今年降了`），不在这节的管辖范围内。

禁用的轮换链，举例：

- 模型名 → `大模型` → `这套系统` → `该产品` → `这款工具`
- 显卡型号 → `GPU` → `这块卡` → `计算设备` → `硬件`
- `Agent` → `智能体` → `这套自动化流程` → `该框架`
- 服务名 → `该服务` → `这个组件` → `该模块`
- 抽象名词的同义替换也算：`核心主题` → `关键焦点`、`主要瓶颈` → `核心制约`

`跑分` → `基准测试` → `评测数据` 只有在三段说的是同一次测试的同一个结果时才算轮换。`跑分` 指动作、`基准测试` 指方法、`评测数据` 指结果的时候，三个词各有所指，原词保留。`部署`、`上线`、`落地` 在多数稿子里指三个不同阶段，不列进轮换链。

改法：动笔之前先给每个对象确定一个固定称呼。第一次出现写全称带型号，后面一直用同一个称呼，重复多少次都不更换。固定称呼可以是缩短的型号（`A100`），可以是一个指示短语（`这个模型`），条件是全文只用这一个。轮换链里出现 `Agent`、`GPU`、`API`、`token` 这类文件要求保留的英文术语时，固定称呼就取英文术语本身。

判定两个称呼是不是指同一个对象，用替换测试：把后面那个称呼直接替换成第一次出现的全称，句子意思没有变化也不产生歧义，就是同一个对象，算违规；替换之后意思变了或者说不通，那是另一个对象，保留原词。`整机` 和 `显卡`、`接口` 和 `服务端` 常常是两个真实对象。

代词 `它` 的判定看距离：上一句刚写过那个固定称呼，接下来用 `它` 没有问题；中间隔了别的名词，或者隔了一句以上，就把固定称呼写回来。

thread 按条算。固定称呼在全篇不变，但每条推文里至少要出现一次带型号的全称，不能靠上一条推文交代——读者刷到的常常只有其中一条。

Bad:

> 我在 4090 上跑了 Qwen3-32B。这个大模型吃满 22GB 显存，该方案在长上下文下速度掉得厉害，这款工具目前还没有挂成线上服务。

Better:

> 我在 4090 上跑了 Qwen3-32B。Qwen3-32B 吃满 22GB 显存，长上下文下 Qwen3-32B 的速度掉得厉害，我暂时没有把 Qwen3-32B 挂成线上服务。

这组只把四个称呼统一成 Qwen3-32B，不顺手处理别的毛病，也不添加 Bad 原文里没有的数字。

Bad:

> 这篇拆解的核心主题是 agent 的记忆层。第二节我把这个关键焦点分成读、写、淘汰三块，第三节再回到该议题上。

Better:

> 这篇拆解的主题是 agent 的记忆层。第二节我把记忆层分成读、写、淘汰三块，第三节再回到记忆层上。

边界：`东西`、`这件事`、`这些` 这类没有信息量的指代词归 Vague referents，改法是补上准确的类别名。这节管的是名字本身有信息量、但同一篇里出现了第二个叫法，改法是把几个叫法统一成一个。

### Vague attribution（模糊归因）

把一句判断挂在一个查证不到的人身上。读者没办法核实这句话，出了错也找不到人问。AI 写稿经常用这类句子，让结论看起来像有出处。

禁用：`专家认为`、`业内普遍认为`、`有研究表明`、`有开发者反馈`、`多方消息显示`、`据了解`、`一些人指出`、`社区里的说法是`、`不少人测试后发现`、`网上普遍反映`、`圈内人士透露`、`有人说`。用化名代替真名也算：`某位开发者`、`一位业内人士`。

判断门槛：一个来源要交代三项信息——是谁（人名、机构名、仓库名、文档名）、在哪（平台或者链接）、哪一天。三项里至少写出两项，读者才查证得到；少于两项就按模糊归因处理。

改法分三种情况：

- 这句话除了归因之外没有带任何可核实的事实，把整句删掉。
- 这句话里带着数字、版本号、日期、产品名、模型名这类可核实事实，只删掉归因短语，把事实本身保留下来，由作者自己承担这句话。保留下来的那句要是完整的主谓宾，也不许顺手补充一句 `我测过` 这种原稿没有的经历。
- 出处在这次对话里看得见（同一篇稿子别的段落写了、用户直接给了原文、原文附了链接或者截图），把那个出处按原样补充回来。

Operating Priorities 第 5 条写明不许新增例子、数据、引用、个人经历，所以看到模糊归因不要自己去找一个来源填进正文。只拿到一份稿子、对话里没有出现过出处的，一律删掉整句。删掉之后再读一遍上下文，确认前后文还能读通，还要检查剩下那句有没有为了跟归因句做对比才写的词（自己、确实、反而、才），一起删掉。

两种写法不算模糊归因：

- 来源指向读者自己能打开的位置：`有人在我评论区说`、`我在仓库 issue 区看到有人反馈`
- 作者用第一人称交代信息是怎么来的：`一个朋友告诉我`。这属于 Goal 里要保住的亲身经历，保留原句；能写具体就把关系和时间写出来（`我同事上周说`），不许替换成化名，也不许替作者补出一个名字

Bad:

> 有开发者反馈，这个 API 在并发高的时候会超时。我自己把并发数提高到 50，接口开始返回超时。

Better:

> 我把并发数提高到 50，接口开始返回超时。

前半句的来源查证不到，超时的现象后半句用具体的并发数讲过一遍，所以整句删掉。原稿的 `我自己` 是为了跟 `有开发者反馈` 做对比才写的，一起删掉。

下面这组演示句子里带着事实的处理方式，只删掉归因短语。

Bad:

> 有开发者反馈，vLLM 0.6.3 这个版本在 4090 上跑 32K 上下文会 OOM。

Better:

> vLLM 0.6.3 这个版本在 4090 上跑 32K 上下文会 OOM。

这句带着版本号、显卡型号和上下文长度，整句删掉会把事实一起删掉，所以只删掉 `有开发者反馈，` 这一截，剩下的判断由作者自己承担。

下面这组演示唯一需要补充来源的情况。用户在同一次对话里给了原文「vLLM 9 月 12 日的 release note 里写，显存占用从 22GB 降低到 15GB」，改写稿把它改成了模糊说法。

Bad:

> 社区里的说法是，这个版本的显存占用降低了不少。

Better:

> vLLM 9 月 12 日的 release note 里写了，这个版本的显存占用从 22GB 降低到 15GB。

出处和数字都来自用户给的原文，这一步做的是按原文恢复。稿子和对话里没有出现过的数字，一个都不要补充上去。

边界：Vague referents 管类别名词写虚了（`东西`、`这件事`），这节管一句判断的来源写虚了，句子里的名词写得再准，来源虚的句子也算模糊归因。

### Wrong time stance

Match verb tense to the actual work state.

- Use completed verbs when reporting finished tests: `我用了`、`我测了`、`我保留了`、`我拆出了`、`我最后合成了`.
- Use future verbs only for real next steps: `我接下来会`、`下一步我会`.
- Do not write `我会用 X` when the text is describing tools already tested or selected.

Bad:

> 我会先用这个 skill 处理中文语感。

Better:

> 这轮我保留了中文语感和场景边界处理规则。

### Vague comparatives

Avoid generic `更适合`、`更像`、`更自然`、`更高级` unless the comparison names the exact use.

Bad:

> 这套规则更像长期方案。

Better:

> 这套流程可以把选题、证据、审稿、去味和导出串成一条线。

### Abstract pressure and empty focus shifts

Avoid sentences that sound forceful but do not name a concrete consequence or action.

Do not write:

- `差距会突然变得很难看`
- `差距会被迅速拉开`
- `会成为新的分水岭`
- `更值得盯的是个人`
- `更值得关注的是...`

Rewrite by naming the visible result, wasted cost, or changed behavior.

Bad:

> 等公司开始给每个人分 AI 额度，差距会突然变得很难看。

Better:

> 等公司开始给每个人分 AI 额度，同样一笔钱，有人只换来几段废话，有人能少开几场会、少返几遍工。

Bad:

> 更值得盯的是个人。

Better:

> 公司账单之外，还要看每个人把额度花到哪里。

### Metaphor and slogan endings

Avoid broad metaphors and quotable endings:

- `正确但无聊的模型作文`
- `上下文燃料`
- `能力飞轮`
- `时代分水岭`
- `作者痕迹`
- `把判断盖住`

Use the concrete loss instead.

Bad:

> 文章读起来再顺，也只像一篇正确但无聊的模型作文。

Better:

> 读者看不出作者测过什么、踩过什么坑、为什么得出这个判断。

### Contest-drama verbs（把比分写成打架，黄佬永久禁用）

比较两个模型/产品的分数时，不许用拟人化的胜负动作词。这类词把"A 的分数比 B 高"演成一场比赛，是 AI 代笔最爱的写法，黄佬一眼认出。

禁用：`压着` / `压制` / `被…压着`、`碾压`、`吊打`、`甩开` / `甩在后面`、`领先一截`、`拉开差距`、`反超`、`追上` / `追平`、`打得有来有回`、`输给` / `赢了`、`干翻`、`稳压一头`、`被按在地上`。

改法：直接说谁的分数高、高多少，或者说"比不过"、"不如"这种平实词。

Bad:

> 上一代 Fable 5 除了科研那行，全被便宜一半的 Opus 5 压着。

Better:

> 上一代 Fable 5 除了科研那行，其他分数都比便宜一半的 Opus 5 低。

Bad:

> 5.1 对 Opus 5 领先也就 2 到 5 个点。

Better:

> 5.1 比 Opus 5 高 2 到 5 个点。

### Performative hype verbs and adverbs

Single vivid words that perform excitement instead of reporting a fact. They read as hype-influencer voice, not a person stating what they saw. Structural de-AI passes miss them because they are not shells, so check them separately.

Watch and cut or downgrade:

- verbs: `扒`（扒到 / 扒开 / 想自己扒）、`炸` / `有点炸` / `炸裂` / `王炸`、`砸`、`甩`（甩给你 / 甩脸上）、`秒`（秒了 / 秒杀）、`杀疯了`、`封神`、`起飞` / `直接起飞`、`拉爆`、`遥遥领先`、`撂`（撂下一句 / 撂一句，装腔的“甩话”动作，报道式陈述用“说 / 讲 / 留了一句”）、`carry`
- empty intensifiers: `绝了` / `太绝了`、`离谱`、`逆天`、`天花板`、`yyds`、`直接好家伙`、`一口气`（“一口气全做了”这类凭空加戏的副词，删掉或直说“全做了 / 接连做了”）、`狠事` / `最狠的`（夸技术动作的表演构造，删或换“意外 / 没想到 / 关键”；注意 `狠` 单用是作者态度词，可留，如“这招狠”“思路狠”）
- completeness fillers（在卖"内容很全"这个卖点，listicle 腔）：`全在` / `全在里头` / `全都有` / `一应俱全` / `应有尽有` / `全给你安排` / `一网打尽`。改成平实的 `都在里面` / `都有`，或直接列清单不加这类词。
- empty adequacy qualifiers（听着像评价、其实没说清能干什么）：`脑子够用` / `够用了` / `能打` / `够强` / `顶得住` / `顶大半` / `完全够` / `很能打` / `不虚`。删掉，或换成它具体能做的事（"日常写代码、跑 agent 都扛得住" 比 "脑子够用" 信息量高）。
- suspense exclamation shells（悬念感叹壳，黄佬明令禁用）：`才知道有多X` / `有多脆` / `有多难` / `有多香` / `你才知道` / `试过才知道`。这类句式在卖情绪悬念、不传信息，`多脆`一词永久禁用。直接把事实本身说出来：不写"真跑起来才知道有多脆"，写"真跑起来问题全在风控：指纹被盯、登录态隔三差五掉、动不动弹扫码"。
- risk-disclosure hats（风险披露帽子，黄佬明令禁用）：`丑话说在前面` / `丑话：` / `先泼盆冷水` / `先给你打个预防针`。戴帽子宣告"我要讲缺点了"是 AI 味；把限制当普通事实直接摆——"目前还是 Preview，官方自己说只适合实验；单工作区 10GB"。

Bad:

> Opus 4.8 脑子够用，日常完全够。

Better:

> Opus 4.8 日常写代码、写文档、跑 agent 都接得住，难任务上不如 Fable。

Rewrite with a plain verb or by stating the concrete fact.

Bad:

> 我扒开原文读了一遍，第一个就有点炸。

Better:

> 我把原文从头读了一遍，第一个点就挺意外。

Keep a vivid word only when it is the author's genuine reaction and appears at most once in the post. Do not stack two.

Distinguish accurate technical words from hype. These carry information and should stay:

- `写死`（= hardcode，精确）
- `锁` / `加锁`（当它准确描述"加了限制/权限控制"时）
- `跑` / `跑通` / `拉到本地`（具体工程动作）

The test: does the word carry information (what happened) or just energy (how excited I am)? Keep information, cut energy.

## Rewrite Workflow

1. Identify the target surface: X/Twitter post, long article, product note, model review, or internal note.
2. Extract the source material into four buckets:
   - facts: dates, prices, model names, tools, test conditions
   - judgment: what the author believes after testing
   - experience: specific usage, failure, cost, workflow, or tradeoff
   - action: what the reader can do or avoid
3. Delete empty framing before rewriting:
   - platform boilerplate
   - AI disclaimer language
   - lecture setup
   - value-lifting summary
   - short imperative hooks such as `别急着...先...` or `顺序别反了`
   - conclusion that repeats the previous paragraph
4. Rewrite with short public-writing paragraphs. For X/Twitter, default to 3-5 paragraphs.
5. Run the final scan. If any hard-ban shell remains, rewrite that sentence again.

## 三遍自审流程

凡是要交付改写稿的调用，都要按下面三遍做完，三遍分开做。用户只问某句为什么像 AI、没有要改写稿的时候，按 Audit Mode 给出诊断就可以，三遍流程不适用。

只修改一遍就交付的稿子，机械痕迹一定还会剩下一部分。写的人刚把句子造出来，回头再读，看到的是自己想表达的意思，很难发现句子里还留着壳子和空泛形容词。

1. 第一遍，重写。按上面的 Rewrite Workflow 从第 1 步做到第 5 步，把整篇稿子修改一轮，得到一版完整稿。
2. 第二遍，重读。把第一遍的结果当成别人交来的稿子，从头通读一遍，逐句问「人会这么说吗」。读起来像金句、显得精妙、显得顺口的地方先标记出来，再逐个检查里面的形容词、动作词、评价词有没有传具体信息；只剩语感、不传信息的删掉，作者自己的态度词和粗糙说法保留下来。按 Audit Mode 的格式列出 3 到 6 条，引用原话并写出它违反的是哪一条规则；一条都没有发现就写明「第二遍无发现」。第二遍必须给出结论，没有结论不能做第三遍。
3. 第三遍，修改。把第二遍列出的每一条逐条修改，修改完再按 Before Returning 清单扫描一次，然后交付。第三遍也在修改句子，可能带进新的禁用壳，所以这次扫描不能省略。

第二遍必须在第一遍结束之后单独做。同一轮里，作者对刚写完的句子默认它成立，注意力还停在自己要表达的意思上面；隔开一遍之后换读者视角重新读，才会注意到哪几句是硬凑出来的。

默认只交付第三遍的最终版本给用户，第二遍列出的问题清单不发给用户。用户问某句为什么像 AI 的时候，按 Audit Mode 的格式给出诊断。开头 Goal 写的 `Default output is the revised text only. Add diagnosis only when the user asks why a sentence feels AI-like.` 说的是同一条规定。

这三遍的要求写在这个 skill 文件里面。别的项目、别的会话单独调用 renhua，同样要把三遍跑完，不依赖外部的 CLAUDE.md，也不依赖用户开口提醒。

Rewrite Workflow 第 5 步和这节分工不同：第 5 步和 Before Returning 清单按字符串扫描禁用词，对着清单逐条扫描一遍就能定位到；这节要求把整篇稿子重新读完，检查整段还有没有机械痕迹、形容词和动作词有没有传具体信息、有没有作者自己的判断。两道检查都要各做一遍，不能互相替代。

## Style Rules

- Use first person when the source includes direct testing or judgment.
- Keep English technical terms that Chinese AI/engineering writers normally use, such as Agent, LLM eval, token, cache, API, GPT, Claude, Codex.
- Use concrete verbs: `测了`、`跑了`、`拉到本地`、`校验通过`、`单测过了`、`保留`、`删掉`、`改散`.
- Prefer completed action when reporting completed work: `这轮我保留了 X，用它处理 Y`.
- Use exact category nouns. Prefer `六类用途`、`三种输出形态`、`两个校验问题` over `几种东西`、`几个方向`.
- Keep mild roughness if it carries the author's voice.
- Do not use emoji, hashtags, Markdown tables, or numbered lists in public posts unless the user asks.
- Avoid ending with an instruction to the reader. End on a concrete judgment or result.

## Audit Mode

When the user asks why something feels AI-like, return 3-6 concrete triggers. Each trigger must quote the phrase and name the pattern.

Use this format:

```text
1. 「...」：二元对比壳。直接说后半句承载的判断。
2. 「...」：伪洞察标记。删掉提示词，从事实起句。
3. 「...」：冒号讲义腔。改成普通句子或拆段。
```

## Before Returning

Check the final text for these strings and patterns:

- `不是` near `而是`
- `不在于` near `在于`
- `不只是` or `不仅`
- `别急着`
- `先别`
- `顺序别反了`
- `别搞反了`
- `记住这句话`
- `真正`、`其实`、`本质上`、`核心在于`、`关键在于`
- `更重要的是`
- setup colon after abstract judgment
- vague `更适合` / `更像`
- abstract pressure such as `差距会突然变得很难看`
- empty focus shifts such as `更值得盯的是个人`
- metaphor ending that hides concrete information
- performative hype words: `扒`、`炸` / `有点炸` / `炸裂`、`砸`、`甩`、`秒`、`绝了`、`起飞`、`杀疯了`、`封神`、`撂`（撂下一句）、`一口气`、`狠事` / `最狠的`（`狠`单用可留）、`离谱`、`逆天`（accurate tech words like `写死`/`锁`/`跑通` are fine）
- completeness fillers: `全在` / `全在里头` / `全都有` / `一应俱全` / `应有尽有` / `一网打尽`（改成 `都在里面`/`都有`）
- empty adequacy qualifiers: `脑子够用` / `够用了` / `能打` / `够强` / `顶得住` / `顶大半` / `完全够` / `不虚`（换成它具体能做的事，或删）
- crafted mirror endings: 同词正反用的对仗（`搬不过来…能搬`、`抄得来…抄不来`、`X 不行但 Y 行`）——拆成两句
- suspense exclamation shells: `才知道有多X` / `有多脆` / `有多难` / `有多香` / `试过才知道`（`多脆`永久禁用；直接陈述事实本身）
- risk-disclosure hats: `丑话说在前面` / `丑话：` / `先泼盆冷水`（删帽子，限制当普通事实直接摆）
- contest-drama verbs（比分写成打架）: `压着` / `压制` / `碾压` / `吊打` / `甩开` / `领先一截` / `拉开差距` / `反超` / `追上` / `有来有回` / `干翻`（改成"分数比它高/低 N 个点"、"不如"、"比不过"）
- truncated words（用词要说完整）: `没变` / `没动` / `单价没动` / `价格没动` / `硬货` / `真货` / `干货` / `不拦` / `没改` / `照旧` / `不变`（不拦 → 不会拦截；改成 `没变化` / `没有变化` / `价格没有变化`，"硬货"直接说是数字还是配置）
- incomplete sentences（句子要完整、主谓宾齐全）: 动作主体换了没点明（`显存占满之后报错了`）、动词后面省掉宾语（`我测了三轮，都通过了`）、独立成段的裸名词短语（`一张 4090，48G 显存。`）——补上稿子里已有的主语和宾语，稿子里没有就标出来问作者；承前省略主语和冒号后的清单项不算残句
- truncated verbs（双音节动词砍成单字）: `删了` / `装了` / `改了` / `测了` / `查了` / `配好` / `传完` / `存好`，以及单字动词直接带宾语（`装依赖` / `删目录` / `改配置`）——按语境改成 `删除了` / `安装了` / `修改了` / `测试了` / `检查了` 或 `查询了` / `配置好` / `上传完` / `保存好`；`删掉` / `改散` / `调小` / `查清楚` 这类带补语的保留，`查表` / `删库` / `调参` / `压测` 这类术语保留，`跑` / `跑通` / `拉到本地` / `写死` / `锁` 不是缩写、保留
- abstract tail verbs（句尾抽象动词假深度）: `意味着` / `标志着` / `体现了` / `反映出` / `印证了` / `展现出` / `透露出` / `见证了` / `支撑起` / `推动` / `凸显` / `彰显` / `折射出` / `映射出` / `诠释了` / `助力` / `赋能`——后面接大词（积累 / 趋势 / 方向 / 实力 / 潜力 / 生态 / 格局）就把整条尾巴删掉，让句子停在事实处；例外保留 `有用户反映`、`单卡支撑不了 70B`、`把 8080 端口映射出来`、`我推动这个 PR 合并了`、`体现在三个地方` 后面接清单
- copula shells（判断动词占了谓语、句子没有动作）: `是……的重要组成部分` / `是……的关键环节` / `是……的核心` / `是……的基础` / `充当` / `扮演……的角色` / `构成` / `代表` / `被视为` / `属于……的一种` / `成为……的标配`——改成动作句说它接收什么、吐出什么，或换成 `有` / `带了` / `支持`；`是` 后面跟日期、数字、型号、报错的，跟作者立场的，定义句说清了存什么收什么的，都保留
- passive shells（被动壳）: `需要被配置` / `会被自动处理` / `会被忽略` / `被设计为` / `被用于` / `被认为` / `被广泛使用`，以及无主语宣告式 `需要提前配置好` / `建议先安装 X` / `推荐使用 X` / `会自动处理` / `默认开启`——动词改主动、写明施动者；`被 OOM killer 杀掉` / `端口被占用` / `我号被封了` 这类保留
- ghost subjects（幽灵主语）: `可以看到` / `可以发现` / `不难发现` / `可以注意到` / `经过测试发现` / `经过对比可以得出`——先删掉观察壳让原有主语站出来，原稿写明是作者自测的才补 `我`；另有一条非字符串判据：整段找不到施动者的陈述句，每段至少点明一次这个动作是谁做的
- synonym rotation（同一个对象轮换称呼）: `这套系统` / `该产品` / `这款工具` / `该方案` / `该框架` / `该模块` / `这块卡` / `计算设备` / `该议题` / `关键焦点`——替换成前文第一次出现的全称，意思没有变化就是同一个对象，写回那个固定称呼；`大模型` / `GPU` / `硬件` 作泛指类别用时不算，thread 每条至少出现一次带型号的全称
- vague attribution（模糊归因）: `专家认为` / `业内普遍认为` / `有研究表明` / `有开发者反馈` / `多方消息显示` / `据了解` / `一些人指出` / `社区里的说法是` / `网上普遍反映` / `某位开发者`——句子里没有别的可核实事实就整句删掉，带着数字或版本号就只删掉归因短语；只有出处在这次对话里看得见才按原样补回来
- 三遍自审已经跑完：第一遍重写，第二遍单独重读并按 Audit Mode 格式列出 3 到 6 条（一条都没有发现就写明「第二遍无发现」），第三遍逐条修改完再扫描一次清单

If found, revise before answering.
