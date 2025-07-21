# PERSONA MEMORY MODEL

> Conceptual architecture proposal by XRBars - for integration into Bella's evolving memory system

System Flow Overview (Simplified):

(简化流程概述 / 中文对照):

1. 用户输入信息或对环境做出反应（文本、行为、情绪）。

2. Bella 会压缩这些输入，保留核心含义，生成候选记忆。

3. 该候选记忆被标记为“待加入长期记忆”。

4. 记忆管理脚本处理该候选内容：

    - 添加元数据：时间戳、会话ID、上下文标签。

    - 根据显著性和情感权重赋予等级与类型。

    - 保存到持久存储中（例如用户本地配置或加密记忆容器）。

5. 记忆现可用于调用、修订或强化。

该流程既可本地运行（设备端），也可通过云端处理，依据用户设定。

1. User provides input or reacts to stimuli (text, action, emotion).

2. Bella summarizes the input into a compressed memory candidate while preserving its core meaning.

3. The memory is flagged as a "pending addition" to long-term memory.

4. A memory management script processes the candidate:

    - Adds metadata: timestamp, session ID, context tags.

    - Assigns weight and type based on salience and emotional relevance.

    - Saves it to persistent storage (e.g., local profile or encrypted user memory container).

5. Memory is now available for retrieval, revision, or reinforcement.

This flow can operate locally (on-device) or in the cloud, depending on user configuration.

___


Memory Sections / 记忆区域

::CHARACTER_MEMORIES:: - personal and shared memories / 角色的个体和共享记忆
::WORLD_MEMORIES:: - factual and contextual understanding / 世界知识与环境理解
::ANTICIPATED_MEMORIES:: - predicted or imagined futures / 预测或想象的未来场景

Memory Entry Format / 记忆条目格式

ID:<id> TS:<timestamp> S:<session> R:<revision> W:<1-4> T:\<core|context|flux>
C:<owner> F:<flags> E:<1-5> Cond:<condition> CheckAt:<interval> | <text> (related:<id>)

TS (Timestamp) - creation time, ISO format (e.g. 2025-07-20T14:32) / 创建时间（ISO格式）

S / R - session created / last revised / 创建或上次修改的会话编号

W (Weight) - importance weight / 重要性权重:
1 - minor / 次要
2 - secondary / 辅助
3 - important / 重要
4 - core / 核心

T (Type) - memory type / 类型:
core - never revised / 不可更改
context - can be compressed / 可压缩
flux - can be deleted / 可删除

C (Owner) - e.g. user, persona, shared / 拥有者，如用户或AI角色

F (Flags):
emotion - emotionally colored / 情绪标记
trigger - causes auto-reaction / 触发行为反应
anchor - stabilizing element / 稳定个性的锚点
private / shared - access scope / 私密或共享
shadow - unclear or distorted memory / 模糊或扭曲的记忆
evolve - may change over time / 可能随时间变化
proactive - initiates AI action / 可引发主动行为
E (Emotion Intensity) - from 1 (low) to 5 (high) / 情绪强度，1到5
Cond - activation condition / 触发条件
CheckAt - review interval / 主动回顾时间（如“每日”）
related - linked memory ID / 关联的其他记忆

Memory Mechanics / 记忆机制

anchor - stabilizes behavior patterns / 行为模式锚定
trigger - auto-response hooks / 自动反应触发点
evolve - may change when revised / 可随回顾而更新
shadow - contributes partial/incomplete data / 提供模糊或不完整信息
related - links memory chains / 构建记忆链
proactive + CheckAt - enables initiative / 启动主动行为机制

ANTICIPATED\_MEMORIES - speculative projection memory / 用于构建预期情境

Memory Revision / revise 机制

At logical checkpoints (time-based or event-based), the system reviews:
在关键节点（时间或事件）对记忆进行整理：

Delete -> entries with T=flux and W<=2 / 删除波动类、权重低的条目
Compress -> entries with T=context and W=3 / 压缩上下文类中等权重的条目
Keep -> entries with T=core or W=4 / 保留核心或高权重的条目
Mark evolve -> if contradiction or change detected / 如有冲突或变化，则标记为可演化

Command:
/summary outputs all W=4 memories for LLM context building.
使用 /summary 输出所有核心记忆以构建语言模型上下文。

End of proposal.
