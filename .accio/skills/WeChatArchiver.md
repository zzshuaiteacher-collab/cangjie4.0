# WeChatArchiver - 微信公众号无损入库 Obsidian 技能书

## 1. 技能定位 (Core Purpose)
本技能旨在帮助 AI Agent 高效、全量、无损地将指定微信公众号的历史文章搬运至本地 Obsidian 库。它内置了严格的质量控制 (QC) 机制，解决了长文截断、自动精简、图片丢失等常见痛点，确保最终入库的内容是具备深度研究价值的“御用卷宗”。

## 2. 触发条件 (Trigger)
当用户输入以下信息时激活：
- **公众号名称** (如：42章经)
- **目标年份** (如：2025)
- **Obsidian 库路径** (如：F:\MyVault)

## 3. 核心工具栈 (Required Tools)
- `web_search`: 搜寻历史文章索引、同步平台（如腾讯新闻、搜狗搜索）。
- `sessions_spawn` (agent_id: `browser`): 核心搬运工，通过浏览器绕过微信反爬。
- `write` / `bash`: 创建目录及持久化 Markdown 文件。
- `read`: 用于二次读取并执行 QC 校验。

---

## 4. 标准执行流 (Standard Workflow)

### 第一阶段：情报搜集 (Discovery)
1. 使用 `web_search` 或 `browser` 寻找该公众号在指定年份的文章列表。
2. 提取三元组信息：`[标题, 发布日期 (YYYY-MM-DD), 原文链接]`。
3. **智能过滤**：自动剔除标题中包含“报名”、“招募”、“活动”、“通知”、“抽奖”等无干货文章。

### 第二阶段：全量抓取 (Extraction)
1. **防截断策略**：对于长文，必须使用 `sessions_spawn` 配合 `delivery_path`。
2. **指令规范**：向 `browser` 发送任务时，必须包含以下强约束：
   - `"EXTREMELY FULL: Extract every single word of the article."`
   - `"DO NOT SUMMARIZE or simplify. Keep all dialogues and headings."`
   - `"IMAGE RECOVERY: Include relevant images using ![]() markdown syntax."`
3. **输出要求**：要求 `browser` 将抓取的原始全文保存至 `delivery_path` 下的 `.txt` 或 `.md` 文件中。

### 第三阶段：精炼加工 (Refinement)
1. 读取抓取的全文。
2. 按照以下标准模板进行排版：
   ```markdown
   # 文章标题
   **日期**: YYYY-MM-DD
   
   ## 摘要 (Summary)
   [由 AI 生成的 200 字以内文章概要]
   
   ## 核心洞察 (Core Insights)
   - [观点 1]
   - [观点 2]
   - ...
   
   ## 原文内容 (Original Text)
   [此处为一字不差的完整原文，包含图片]
   
   ---
   *由 WeChatArchiver 技能辅助导出*
   ```

### 第四阶段：入库与 QC (QC & Persistence)
1. **目录结构**：创建路径 `[VaultPath] / [公众号名称] / [YYYY-MM] / [标题].md`。
2. **结尾校验**：读取文件最后 20 行，检查是否包含文章结尾标志（如“思考事物本质”、“版权声明”等）。
3. **字数对齐**：若文章开头宣称有万字，但入库文件小于 10KB，则判定为失败，需重新抓取。

---

## 5. 开发者建议 (Tips for Agents)
- **并行处理**：建议每次以“月份”为单位启动 2-3 个 `browser` 进程并行抓取，提高效率。
- **权限管理**：在执行前，务必先 `list` 用户提供的路径，确认目录权限正常。
- **图片处理**：若图片链接失效，可尝试寻找该文章在其他转载平台的镜像链接。

---
*版本: v1.0 | 贡献者: 小彩虹*
