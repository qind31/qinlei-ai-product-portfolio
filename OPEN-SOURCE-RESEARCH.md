# 开源方案调研与技术选型

> 本文只记录来源、方法与可借鉴思路，不复制任何第三方源码。许可证状态以各上游仓库为准；未核实的明确标注。

## 1. 调研目的

为两件事寻找依据：

1. 作品集如何组织：README 与案例文档应包含哪些结构；
2. 视频与字幕管线有哪些成熟做法。

## 2. 作品集展示方式调研

| 来源 | 可借鉴点 | 许可证 / 说明 |
| --- | --- | --- |
| [README Design Patterns](https://github.com/Just-Agent/README-Design-Skill/blob/main/skills/readme-design/references/patterns.md)（Just-Agent） | 标准 README 结构与作品集结构：身份、精选项目、能力亮点、技术栈、当前方向；强调以事实而非形容词表达价值 | MIT（GitHub API 元数据，未逐字核对 LICENSE 原文）；只借鉴结构，不复制文本 |
| [Retrospective and portfolio](https://github.com/AICanCode-org/ecommerce-backend/blob/main/docs/phase-8-retrospective.md)（AICanCode-org） | 案例叙事：问题 → 方案 → 安全证据（威胁/防护/测试）→ 架构取舍 → 可验证证据 → 下一步 | MIT（GitHub API 元数据，未逐字核对 LICENSE 原文）；只借鉴方法 |
| [Portfolio-PO-IT-Management](https://github.com/iconejeroit/Portfolio-PO-IT-Management) | 产品经理作品集按项目拆分案例到 docs/ | 仅作结构参考，未深读源码；MIT（GitHub API 元数据，未逐字核对 LICENSE 原文） |

对本作品集的影响：

- 第一屏给出身份、定位、文档入口与诚实状态；
- 案例用"问题—方案—个人职责—验证—状态"组织，而非堆功能；
- 安全与取舍用表格表达，便于招聘者快速定位；
- 结论尽量给出可验证依据，避免空泛形容词。

## 3. 视频与字幕管线调研

| 来源 | 借鉴内容 | 许可证 / 说明 |
| --- | --- | --- |
| [FFmpeg 官方文档](https://ffmpeg.org/ffmpeg-filters.html#ass) | concat 拼接、libass 烧录 ASS、字体目录指定、时长探测 | 官方资料；FFmpeg 构建为 LGPL，未分发二进制 |
| [tylkokcr/ShortPulse](https://github.com/tylkokcr/ShortPulse) | ASS 头结构、CJK 文本处理、镜头→拼接→单次字幕烧录的路径、跨平台路径转义、字体能力不能靠假设 | 项目 MIT；只借鉴设计思路，未复制源码 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | 图片+配音+字幕的短视频编排流程参考 | 项目 MIT；Python/MoviePy 栈较重，未复用代码；仅进行源码与流程调研，未实际运行，未集成。 |
| [remotion-dev/remotion](https://github.com/remotion-dev/remotion) | 复杂动画合成能力评估 | 自定义双层许可（非 MIT）；评估后未采用 |
| FFmpeg slideshow / Ken Burns 社区实践 | 静态图缓慢推进/平移的常见实现与参数含义 | 社区资料，作为思路参考；社区文章未作为证据引用，具体参数与效果结论以本机实测为准 |

## 4. 选型结论

| 问题 | 选择 | 理由 |
| --- | --- | --- |
| 字幕方案 | ASS + libass | 中文排版与位置控制成熟 |
| 视频编码 | H.264 / yuv420p | 竖屏短视频交付兼容性优先 |
| 字体 | 开源中文字体（OFL） | 覆盖中文，许可清晰；不分发字体文件 |
| 渲染环境 | 本机离线验证 | 先验证可行性与观感，不引入云服务成本 |
| 自动化服务 | 暂缓，未来候选 VPS / 轻量容器 | 需成本、并发与数据流量评估 |

## 5. 反例与修正

- **不选择 Cloudflare Containers**：当前阶段无法证明其成本、冷启动与网络收益优于简单 VPS。
- **不直接采用旧版全局缩放渲染**：审查发现它本质是静态轮播；最小改造为每镜头独立参数后，才支持不同构图与运动。
- **不把配置正确当成视觉合格**：V1 配置测试通过但观感失败；后续用抽帧与帧间差异量化，确认幅度不足并修正。

## 6. 引用与合规

- 以上项目只作为方法与结构参考，未复制源码、文案或品牌资产。
- 每个引用保留项目名称与来源；许可证未核实的不擅自声明。
- 不向作品集添加第三方源码；不为原项目擅自添加开源许可证。
