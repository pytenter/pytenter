<div align="center">
  <img src="https://pytenter.github.io/static/assets/portrait.webp?v=20261109-avatar" width="144" height="132" alt="潘子逸的插画头像" />
  <h1>潘子逸 · Ziyi Pan</h1>
  <p><strong>华南理工大学 · 未来技术学院</strong></p>
  <p>数据科学与大数据技术专业 · 2024 级本科生</p>
  <p>具身智能 · 机器人模型微调 · 大模型高效推理与量化</p>
  <p>
    <a href="https://pytenter.github.io/">个人学术主页</a>
    &nbsp;·&nbsp;
    <a href="mailto:ftben@mail.scut.edu.cn">ftben@mail.scut.edu.cn</a>
  </p>
</div>

## 关于我

我主要关注**具身智能与高效推理**：围绕真实机器人场景开展数据整理、模型微调与闭环评估，同时探索循环状态与 KV Cache 的低比特表示，分析量化误差在长跨度推理中的累积与传播。

目前的研究与实践包括：

- **机器人模型微调**：Kinova Gen3 真实示范数据、图像与状态数据适配、π0.5 模型微调。
- **循环状态量化**：GDN / KDA 的持续 INT8 状态存储、可学习正交旋转、状态与局部输出联合重建。
- **KV Cache 压缩**：面向长思维链推理的混合精度分配与压缩域解码。
- **机器人评估**：结合 MuJoCo 仿真与 Kinova Gen3 真机，记录和分析策略在桌面操作任务中的表现。

## 论文与研究

### LeaRSQ：面向线性注意力循环状态量化的可学习旋转

**第一作者 · 稿件已完成**

- **研究问题**：线性注意力模型的循环状态需要在每步解码中反复读取和更新，INT8 量化误差可能沿循环路径持续传播，固定旋转难以适配不同模型的状态分布。
- **算法创新**：冻结预训练参数，在 GDN 的 Key 侧和 KDA 的 Value 侧学习正交旋转；联合优化局部输出与状态重建，使用 H64 截断反向传播考虑多步误差。
- **贡献**：连接适配模型的表示学习与实际推理路径，覆盖 Qwen3.5-9B / GDN 和 Ling-3.0-tiny / KDA；稿件描述了 SGLang 中冻结旋转与融合状态更新的集成方案。

[查看研究介绍与方法图 →](https://pytenter.github.io/#learsq)

### TrajKV：面向长思维链推理的轨迹感知混合精度 KV Cache 量化

**共同第一作者 · ICASSP 在投**

- **研究问题**：低比特 KV Cache 误差会在后续注意力计算与自回归生成中递归传播，不同历史位置对后续解码的影响并不相同。
- **算法创新**：联合历史注意力反映的因果重要性与 INT2→INT4 重建收益，将符合条件的 25% 历史 Value 升为 INT4，其余历史 Value 与 Key 保持 INT2。
- **贡献**：结合轨迹误差诊断、选择性精度保护与 K2/V2/V4 压缩域解码，避免完整物化历史 FP16 KV Cache。论文在 DeepSeek-R1-Distill-Llama-8B 上报告：AIME24 准确率由匹配的 PatternKV-Base 的 35.56% 提升至 53.33%。

[查看研究介绍与实验结果 →](https://pytenter.github.io/#trajkv)

## 项目与机器人实践

### Kinova Gen3 真机微调

围绕桌面抓取与放置任务，开展 Kinova Gen3 机械臂的数据处理、π0.5 模型微调与闭环评估，将真实视觉观测、机器人状态和动作标签用于策略训练与实验分析。

- **真实数据整理**：完成 **107 条真实示范轨迹**的采集与整理，以及机器人状态和动作标签重建。
- **模型微调**：进行图像与状态数据适配、微调训练和检查点验证，构建面向真实机器人数据的训练流程。
- **实验与记录**：开展 MuJoCo / Kinova Gen3 闭环评估，记录抓取、搬运与放置过程中的策略表现。

[查看真机录屏与机械臂过程图 →](https://pytenter.github.io/#project-video-title)

其他公开仓库：[PatternKV 复现与实验](https://github.com/pytenter/Bounded-pattrenKV-method) · [多模态 RAG 论文整理](https://github.com/pytenter/Multi-Model-RAG)

## 技术与实践

- **语言与工具**：Python、C/C++、PyTorch、Linux、Git、LaTeX。
- **模型与推理**：机器人策略微调、循环状态与 KV Cache 量化、SGLang 推理集成。
- **实验与数据**：MuJoCo、Kinova Gen3、示范轨迹整理、状态与动作标签重建、模型微调与评估。
