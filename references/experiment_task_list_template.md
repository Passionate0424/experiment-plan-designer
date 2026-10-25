# 实验执行 Task 追踪看板模板 (Experiment Task Checklist Template)

> **使用说明**：
> 本文件为**独立的动态执行追踪看板**（通常保存为项目或实验目录下的 `TASK_LIST.md`，如 `docs/TASK_LIST.md`）。
> 它与静态的设计方案（`plan_<idea>.md`）彻底解耦，专用于实验执行期间的高频状态更新、巡检标注与判据对账。

---

# 实验执行看板：[项目 / Idea 名称] Task Tracking Ledger

- **对应实验计划文档**：[plan_xxx.md](./plan_xxx.md)
- **最新巡检时间**：`YYYY-MM-DD HH:MM:SS`
- **执行环境快照**：`[GPU 型号 / Conda 环境 / Git Commit Hash]`

## 1. 任务总体进度概览 (Status Overview)

| 总任务数 | 已通过 (Go / Passed) | 运行中 (In Progress) | 待执行 (Pending) | 阻断/待排查 (No-Go / Blocked) |
| :---: | :---: | :---: | :---: | :---: |
| **N** | `0` | `0` | `N` | `0` |

---

## 2. 基于实验矩阵的 Task 推进清单 (Task Matrix Checklist)

> **表格轴向定义**：
> - **纵轴 (Rows)**：执行任务编号 (Task ID，按子实验或阶段划分，如 TASK-01, TASK-02, TASK-04a-1...)；
> - **横轴 (Columns)**：对应子实验模块全称、核心自变量配置与测试轮次范围、关联执行脚本与后台 tmux 会话、核心 Go 判据阈值、当前状态标识、实测关键指标与结论追溯；
> - **单元格 (Cells)**：各任务在该调度与判据维度上的实时进展、真实数值记录与对账判定。

- **状态标识说明**：
  - `[ ]` **未开始 (Pending)**：等待前置任务就绪或尚未启动；
  - `[-]` **运行中 (In Progress)**：后台正在执行，注明 tmux session 或进程 PID；
  - `[x]` **已完成并通过 (Passed / Go)**：实测指标达到设定的通过判据（Go），交付物与测试门禁全部就绪；
  - `[!]` **受阻或未达标 (Failed / No-Go)**：实测指标未达到判据或发生异常，触发归因分析与方案调整。

| 任务编号 | 对应子实验模块 | 核心自变量配置 / 轮次 | 关联执行脚本 / tmux 会话 | 核心 Go 判据阈值 | 当前状态 | 实测关键指标与结论 |
| :--- | :--- | :--- | :--- | :--- | :---: | :--- |
| **TASK-01** | 实验一：[模块全称] | [变体范围，如 7 档保留率共 266 组] | `python run_exp1.py`<br/>(session: `exp1_run`) | [如 $r=20\%$ 时 $\text{IoU}<0.35$] | `[ ]` | 待启动 |
| **TASK-02** | 实验二：[模块全称] | [变体范围，如 10 步 $\times$ 18 层] | `python run_exp2.py`<br/>(session: `exp2_run`) | [如深层能量集中度 $R_{90\%} \le 0.08$] | `[ ]` | 待启动 |
| **TASK-03** | 实验三：[模块全称] | [变体范围，如 36 步 $\times$ 6 档] | `python run_exp3.py`<br/>(session: `exp3_run`) | [如跨帧召回率 $\ge 80\%$] | `[ ]` | 待启动 |
| **TASK-04a-1** | 实验 4a: Stage 1 | 13 方法 $\times$ 5 任务 $\times$ 10 种子 | `eval_closed_loop.py`<br/>(session: `exp4a_s1`) | Hybrid 胜出且 SR 逼近 Dense | `[ ]` | 待启动 |
| **TASK-04a-2** | 实验 4a: Stage 2 | Champion + 4 基线 $\times$ 4 档 $r$ | `run_stage2_pareto.py`<br/>(session: `exp4a_s2`) | 绘制 Pareto 成功率与步数曲线 | `[ ]` | 依赖 TASK-04a-1 |
| **TASK-04b** | 实验 4b: 硬件加速 | 10 档正交矩阵 $\times$ 30 步实测 | `profile_speedup.py`<br/>(session: `exp4b_run`) | Prefill 加速 1.5x+，KV < 4MB | `[ ]` | 待启动 |

---

## 3. 任务执行明细日志与判据对账记录 (Detailed Execution Log)

### TASK-01：[子实验一名称]
- **启动时间**：`YYYY-MM-DD HH:MM:SS`
- **后台会话**：`tmux attach -t exp1_run`
- **日志路径**：`outputs/exp1.log`
- **产出检查**：
  - [ ] 定量数据表：`outputs/exp1_metrics.csv`
  - [ ] 可视化图表：`outputs/fig1_plot.png`
  - [ ] 自动化测试门禁：`test_deliverables_e2e.py`
- **实测指标与 Go/No-Go 对账**：
  - 实测数值：`[例如 IoU = 0.28, Recall = 79.2%]`
  - 判据判定：`[通过 (Go) / 未通过 (No-Go)]`
  - 归因与结论：`[简要记录现象原因与后续行动]`

