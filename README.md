# Verifiable Reasoning & Tool-Use Post-training

研究问题：能否把测试时搜索偶尔发现的正确推理/工具轨迹，通过监督微调和可验证奖励强化学习，内化为模型更稳定的单次推理能力？

实验主线：

```text
starting policy
  -> best-of-N test-time search
  -> verified trajectories
  -> trajectory SFT
  -> GRPO / RLVR
  -> controlled evaluation and ablation
```

## 当前阶段

Phase 0：建立可复现工程、冻结任务/轨迹协议，并在 RTX 4060 笔记本上完成兼容性验证。

此仓库目前只包含工程底座和数据协议，不包含尚未运行的训练结果。

## 模型范围

- 调试模型：`Qwen/Qwen3.5-0.8B`
- 正式实验候选：`Qwen/Qwen3.5-4B`
- RTX 4060：0.8B 全流程；4B 量化推理与小规模 Search
- 正式 4B GRPO：不在 4060 上强行运行

## 快速检查

无需安装第三方依赖即可检查当前底座：

```powershell
$env:PYTHONPATH = "src"
python -m unittest discover -s tests -v
python -m verifiable_posttraining.cli doctor
python -m verifiable_posttraining.cli schema-demo
```

Linux/WSL：

```bash
PYTHONPATH=src python -m unittest discover -s tests -v
PYTHONPATH=src python -m verifiable_posttraining.cli doctor
PYTHONPATH=src python -m verifiable_posttraining.cli schema-demo
```

GPU 电脑上的详细步骤见 `docs/GPU_HANDOFF.md` 与
`docs/FOUR_DAY_GPU_SPRINT.md`。

## 学习分级

- A：必须掌握并能独立写出核心逻辑
- B：必须读懂并能够修改
- C：正确调用即可

详细映射见 `docs/LEARNING_MAP.md`。所有真实实验必须保留配置、随机种子、原始输出、指标和失败样例，禁止补写或虚构结果。

