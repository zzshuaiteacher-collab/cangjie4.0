# 仓颉 v4.0：Obsidian 知识库标准结构

为了实现 99% 的绝对模仿度，本地 Obsidian 仓库必须遵循以下物理分区：

## 1. 00_Raw_Sources (地毯式全渠道搬运)
*   **WeChat_Posts/**: 微信公众号历史文章全量采集（保留时间戳、阅读量）。
*   **Transcripts/**: 播客、视频、深度访谈实录（还原即兴表达）。
*   **Writings/**: 书籍、研报、长篇 Newsletter。
*   **Social_DNA/**: 微博、评论区互动（捕捉碎片化的人格特质）。

## 2. 01_Entities_Wiki (持久化实体账本)
*   **Concepts/**: 核心分析框架（如：#第一性原理, #护城河）。
*   **Companies/**: 目标公司档案。
*   **Figures/**: 相关人物图谱。

## 3. 02_Style_Fingerprints (量化表达金库)
*   **Metaphor_Vault.md**: 结构化的隐喻与类比仓库。
*   **Vocabulary_Gold.md**: 专属高频词与术语表。
*   **Writing_Pattern.json**: 量化指纹（句长、标点密度、段落节奏）。
*   **Golden_Corpus/**: 精选 L5 级黄金语料，作为 Few-Shot 锚点。

## 4. 03_Logic_Graph (图谱重构层)
*   **Triples_Index.md**: 实体关系三元组总索引。
*   **Internal_Tensions.md**: 思想内部矛盾与纠结记录。

## 5. 04_Evolution_Ribs (纠错补丁层)
*   **Correction_Log.md**: 分层级的 [C-理/文/情/排] 补丁记录。

## 📥 知识入库打标语法
在原始 Markdown 文件中，推荐使用以下行内标注供 AI 检索：
*   `(Style: #Metaphor | Emotion: #High_Arousal | Logic: #Reasoning)`
*   `(Entity: [[王兴]] | Stance: #Critical)`
