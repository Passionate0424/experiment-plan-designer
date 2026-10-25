# Experiment Plan Designer (`experiment-plan-designer`)

面向系统、算法与具身智能 (VLA / Robotics) 软硬件协同研究的**专业实验计划制定与闭环验证技能规范**。

---

## 🌟 技能定位与核心价值

在具身大模型 (VLA) 与体系结构软硬件协同等跨学科前沿探索中，科研人员常面临**“算力爆炸、样本量小导致虚高、缺乏假说递进链条、设计与执行脱节”**等痛点。

本技能沉淀自实战研究，旨在帮助研究人员与 AI Agent 在启动具体实验前，建立严密、专业、标准化的实验手册：
1. **拒绝盲目试错**：从第一性原理与硬件 Profiling 瓶颈出发，打磨与升维 Idea，证明优化假说的物理可行性与天花板；
2. **递进式假说矩阵**：建立清晰的因果链条（$\text{机理必要性} \to \text{物理特征真实性} \to \text{算法连接} \to \text{真实任务效果} \to \text{系统端到端收益}$）；
3. **专业实验手册规范**：每个子实验严格遵循**标准 5 部法**，用表格化与公式前置理清自变量、消融维度与量化判据；
4. **设计与执行彻底解耦**：方案设计文档 (`plan_<idea>.md`) 保持相对静态，独立的动态执行看板 (`TASK_LIST.md`) 依据矩阵实时追踪进度与判据闭环。

---

## 📂 仓库结构

```text
experiment-plan-designer/
├── SKILL.md                                 # 主技能定义文件 (含 YAML frontmatter 与全流程指导规范)
├── README.md                                # 仓库说明文档
└── references/                              # 配套开箱即用模板 (渐进式披露)
    ├── experiment_plan_template.md          # 专业实验计划设计模板 (Plan Template)
    └── experiment_task_list_template.md     # 独立执行 Task 追踪看板模板 (Task Checklist Template)
```

---

## 🚀 核心工作流速览

### 1. 两大前置阶段 (Two Phases)
- **阶段一：第一性原理与 Profiling 剖析 (打磨 Idea)**
  - Amdahl 定律全链路收益测算（FLOPs 瓶颈 vs 访存瓶颈）；
  - 核心痛点与空间/物理错配剖析（如 Perception Salience $\neq$ Action Salience）；
  - 提炼逻辑自洽、软硬件协同闭环的成熟方案。
- **阶段二：确立成熟 Idea，设计系统化实验矩阵 (验证 Idea)**
  - 将核心方案拆解为层层递进的子实验链条；
  - 每个子实验严格落实标准 5 部结构。

### 2. 子实验标准 5 部结构 (Standard 5-Part Section)
每个子实验模块必须严格包含：
1. **实验名称 (Name)**：明确模块全称与代号；
2. **实验目的 (Objective)**：阐述解答的核心科学问题与在整体验证链中的定位；
3. **实验矩阵 (Matrix)**：
   - *主要指标定义与计算方式表*：公式与物理含义前置；
   - *独立消融维度矩阵*：解耦正交消融维度（如 $3 \times 3$）；
   - *完整实验执行配置表*：自变量配置、评测任务、轮次与成对随机种子范围；
4. **实验方案 (Protocol)**：硬件环境、输入数据源（连续真实 Rollout）、Hook 拦截点与单行复现命令；
5. **实验结果与交付物 (Deliverables & Criteria)**：
   - 定量数据产出 (CSV Schema)
   - 可视化绘图规划 (Composite Panel 布局)
   - 实验报告沉淀 (独立报告或汇入总报告)
   - 实验可复现记录 (Git Hash、环境快照、Seeds、数据 SHA256)
   - 量化判据 (Go / No-Go Criteria)

### 3. 独立执行看板 (Decoupled Task Tracking)
实验计划制定完成后，依据实验矩阵独立派生 `TASK_LIST.md`，使用 4 档标准状态标识实时更新：
- `[ ]` 未开始 (Pending)
- `[-]` 运行中 (In Progress，记录 PID / tmux 会话)
- `[x]` 已完成并通过 (Passed / Go，实测指标严格达标)
- `[!]` 受阻或未达标 (Failed / No-Go，触发归因与排查)

---

## 🛠️ 安装与使用方法

### 方式 1：作为项目级 Agent Skill (推荐)
将本仓库克隆至目标项目的 `.agents/skills/` 目录下：
```bash
cd your_project_root
mkdir -p .agents/skills
git clone https://github.com/Passionate0424/experiment-plan-designer.git .agents/skills/experiment-plan-designer
```

### 方式 2：作为机器全局 Agent Skill
克隆至机器级全局配置目录：
```bash
mkdir -p ~/.gemini/config/skills
git clone https://github.com/Passionate0424/experiment-plan-designer.git ~/.gemini/config/skills/experiment-plan-designer
```

启动支持 Antigravity / Gemini 规范的 AI Coding Agent 后，Agent 将自动发现并按需加载本技能！
