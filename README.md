# video-prompt-cleaner：对比视频模型前，先清掉提示词里的技术偏向

用同一批提示词测试几个视频生成模型时，如果提示词里写了「用 diffusion 生成」「[CODE] 这个仪表盘」「Three.js + GSAP」，结果就会偏向擅长这种做法的模型，对比不公平。

这个 skill 删掉提示词里所有关于「用什么技术做」的内容，只保留「片子是什么样」的内容。

## 适合什么时候用

- 做多模型视频评测，需要一套公平的提示词
- 表格里有一列提示词，要去掉其中的模型名、引擎名和渲染标签
- 要求只删不改

## 删什么，留什么

删掉：

- 渲染标签，如 `[CODE]` `[DIFF]` `[HYB]` `[3D]` `[CG]`
- 技术路线词，如 diffusion、code-gen、hybrid
- 引擎和模型名，如 Remotion、Three.js、GSAP、Blender、Runway、Sora、Kling、Veo
- 整段技术说明，如 Stack、Technical Notes、Render notes

原样保留：旁白、屏幕文字、配色和色值、镜头与光线、场景标题和时间码、故事内容。描述画面的普通说法也保留，比如「一个打开的 3D 盒子」。

## 只删不改，并且自动核对

留下的每个字都和原文完全一致，包括大小写、标点、空格和换行。删完后，脚本逐字比对原文和清洗后的版本，只要有一个字符被新增或改动就报错。不通过核对不交付。

## 你会拿到什么

- **表格**：在原表格里新增一列清洗后的提示词
- **对照网页**：每处删除用删除线标出并编号，鼠标悬停可以看到删除原因，方便你按编号抽查
- **汇报**：清洗了多少条、删了多少处、核对是否通过、可疑残留是怎么判断的

也可以直接贴几条提示词，它会返回清洗后的文本。

## 需要准备

Python 3。处理 .xlsx 文件时还需要 openpyxl：

```bash
pip3 install openpyxl
```

## 怎么用

- 「把这个表 G 列的 prompt 清洗一下，A 列是编号」
- 「去掉这几条 prompt 里的模型名和技术栈，只删不改」

清洗结果请按编号列和原表对应，不要用提示词文本去匹配。提示词往往有几千个字符，Excel 的 VLOOKUP 超过 255 个字符就会匹配失败。

## 包含的文件

- `SKILL.md`
- `references/deletion-rules.md`：删除规则和边界情况示例
- `scripts/extract_column.py`：把表格中的一列导出为单独的文本文件
- `scripts/verify_and_report.py`：逐字核对、扫描残留、写回表格、生成对照网页

## 安装

```bash
git clone https://github.com/Minerva67/video-prompt-cleaner.git ~/.claude/skills/video-prompt-cleaner
```

重启 Claude Code 后，直接描述你的任务就会触发。也可以输入 `/video-prompt-cleaner` 手动调用。

更多 skill 见 [claude-skills](https://github.com/Minerva67/claude-skills)。
