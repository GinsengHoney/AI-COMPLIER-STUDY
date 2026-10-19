# AI Compiler Study

个人定制的 **AI 编译器工程师** 36 周学习与技术博客路线。

- 起点：C++ 基础语法已掌握、项目经验较少；CUDA 有过优化经历，需要复健
- 目标岗位：初级 AI 编译器工程师（偏 LLVM/MLIR 中端、张量编译与 GPU 后端协同）
- 计划强度：每周约 **12–15 小时**
- 计划版本：V2.0 / V3 微项目附录｜修订日期：2026-10-18
- 启动周：自 **2026-10-19** 所在周起计（可按实际启动顺延）

本仓库是学习主仓。四年前的 CUDA 练习仓库仅作历史参考，不作为进度前提：

- 本仓库：[AI-COMPLIER-STUDY](https://github.com/GinsengHoney/AI-COMPLIER-STUDY)
- 旧仓参考：[CUDA_Study](https://github.com/GinsengHoney/CUDA_Study)（2023 年前半的 CUDA 笔记与实验）

---

## 学习主线

```text
现代 C++ 工程（前 4 周集中 + 后 32 周持续）
    → 编译原理 / AST / 自定义 IR
    → LLVM IR / Pass
    → MLIR Dialect / Rewrite / Lowering
    → PyTorch 编译链（FX / Dynamo / Inductor）
    → GPU Kernel（CUDA 复健 / Triton）与 TVM 调度
    → MiniTensorCompiler 综合项目
    → 源码阅读 / 开源协作 / 求职作品集
```

**原则**

1. **C++ 贯穿全程**：不只学四周；每周至少提交一个 C++ commit 和一个自动化测试。
2. **旧 CUDA 仓可选**：可重新用 AI 协作写 baseline；自己负责需求边界、正确性、Profiler、解释与重构。
3. **AI 生成 ≠ 已学会**：必须亲自阅读、测试、剖析和解释；无法解释的代码不算完成。
4. **阶段门槛**：能运行、能解释、能测试；达不到就延长一周，不机械推进。
5. **版本固定**：为 LLVM/MLIR、PyTorch、Triton、TVM 分别固定 release/commit，避免跨版本混用教学 API。
6. **写作并行**：每周实验笔记；每两周一篇高质量技术博客（约 18 篇正式文章 + 36 份周记录）。

---

## 每周时间建议（约 14 小时）

| 类别 | 时长 | 说明 |
|------|------|------|
| C++ / 编译器编码 | 7h | 前四周可提到 7–8h |
| 系统学习 | 3h | 文档、教程、论文 |
| CUDA / 性能实验或源码阅读 | 2h | 含 Profiler |
| 博客与复盘 | 2h | 周记或正式长文 |

---

## 36 周里程碑

| 周次 | 主题 | 阶段可验收成果 |
|------|------|----------------|
| 1–4 | CUDA 复健 + C++ 工程基础 | 独立 CUDA/C++ 实验；CMake + 测试 + 性能记录 |
| 5–8 | 编译原理 + AST / IR | 表达式语言 Lexer、Parser、自定义三地址 IR |
| 9–12 | LLVM IR / Pass | LLVM IR 生成 + 优化 Pass + FileCheck |
| 13–16 | MLIR Toy / Dialect | Toy 教程；自定义 Operation / Rewrite |
| 17–20 | MLIR Lowering / 执行 | 张量表达式下降至 CPU 可执行链路 |
| 21–24 | PyTorch 编译链路 | FX 图变换与简单 custom backend |
| 25–28 | Triton + TVM 调度 | 带真实测量结果的算子/调度实验 |
| 29–32 | MiniTensorCompiler | 输入 → MLIR → Pass → Lowering → 执行 |
| 33–36 | 源码阅读 / 开源 / 求职 | 开源尝试、项目说明、面试案例与作品集 |

---

## C++ 全程能力矩阵

| 阶段 | 重点 | 验收 |
|------|------|------|
| W01–W04 | RAII、所有权、模板/STL、CMake、CTest、Sanitizer、Benchmark | MiniTensor 可重建、可测试、可调试 |
| W05–W08 | 类层次、variant/visitor、unique_ptr AST、错误处理 | Lexer → Parser → AST → 自定义 IR |
| W09–W12 | LLVM C++ API、IRBuilder、PassManager | 可编译的 LLVM Pass + FileCheck |
| W13–W20 | MLIR API、TableGen/ODS、Dialect、Rewrite、Conversion | 自定义 Dialect 与 Lowering 端到端 |
| W21–W28 | Python 前端 / C++ 后端、profiling、性能回归 | 能阅读并修改真实编译链模块 |
| W29–W36 | 大型工程组织、CI、审查、源码阅读 | 作品可复现，能讲清 C++ 设计取舍 |

---

## V3 执行法：每次学习做一个小项目

每周建议 **3 次**主学习（每次 2–3 小时），每次只做一个可独立运行的小实验。  
36 周 × 3 ≈ **108 个微型项目**。

**每次固定 5 步**

1. 15–25 分钟：读一个概念，写下今天要验证的单一问题  
2. 60–100 分钟：写最小可运行程序（可 AI 辅助初稿）  
3. 20–30 分钟：加正确性测试、错误输入和边界条件  
4. 15–20 分钟：改一处实现，观察输出 / IR / 速度变化并留证据  
5. 10–15 分钟：写学习卡片（问题、关键代码、结果、解释、下次疑问）

**最低验收线**

- **可运行**：README 写清环境、构建、运行命令  
- **可测试**：≥2 个正常输入 + 1 个边界/异常；Pass 用 lit/FileCheck 或等价测试  
- **可解释**：不看 AI，能解释 3 个关键实现选择  
- **可复现**：单独目录、独立 commit，记录版本与机器信息  
- **可写作**：150–300 字回答「为什么需要 / 做了什么 / 发现了什么」

---

## AI 辅助编程原则

允许 AI 重写 CUDA / C++ 示例与单元测试；**不要求**复用旧 `CUDA_Study` 源码。

每次 AI 产出必须过四关：

1. 运行参考答案 / 误差测试  
2. 检查越界与异常  
3. 固定硬件、数据形状、精度并做基准测试  
4. 逐函数解释关键逻辑  

博客需区分：**原始版本 / AI 建议版本 / 人工修订版本**；公开测试环境、命令与实测结果。  
**严禁**把未经测量的「提升 xx%」写成结论。

---

## 博客机制

面向有 Python / CUDA 基础的工程师，文章结构建议：

> 问题 → 直觉 → IR/代码 → 实验 → 坑点 → 结论

| 节奏 | 产出 |
|------|------|
| 每周 | 300–600 字实验日志 |
| 双周 | 1800–3000 字正式文章 |

**建议专栏**

| 专栏 | 周次 |
|------|------|
| CUDA 回炉：从性能实验重新出发 | 1–4 |
| 手写编译器：从 AST 到 LLVM | 5–12 |
| MLIR 工程实践 | 13–20 |
| AI 编译链路拆解 | 21–24 |
| GPU Kernel 与 Tensor 调度 | 25–28 |
| MiniTensorCompiler 开发日志 | 29–36 |

---

## 每周验收评分卡

| 维度 | 通过条件 | 权重 |
|------|----------|------|
| 正确性 | 可重复测试；错误输入有明确处理 | 30% |
| 工程质量 | 构建说明清楚；可读；版本固定 | 20% |
| 性能/验证 | 有基线、环境、过程与结果（适用时） | 20% |
| 原理理解 | 不看笔记能解释关键 IR / 并行机制 | 15% |
| 知识传播 | 实验日志；双周一篇成稿 | 15% |

建议阶段通过线 **80/100**；正确性不通过则不得标记完成。

---

## 计划中的仓库结构

```text
AI-COMPLIER-STUDY/
├── README.md
├── env/versions.md
├── docs/roadmap.md
├── weekly-log/          # W01.md … W36.md
├── blogs/
│   ├── weekly-notes/
│   └── published/
├── week01/ … week36/    # 每周 3 个微实验目录
├── cpp-tensor/
├── cuda-review/
├── toy-compiler/
├── llvm-passes/
├── mlir-toy/
├── pytorch-compiler/
├── triton-tvm-labs/
├── mini-tensor-compiler/
└── benchmarks/
```

目录会随周次推进逐步落地，不一次性空建全部骨架。

---

## 研究地图（配套阅读）

详细调研见本地文档《实验室和企业研究报告》。摘要：

| 优先级 | 团队 / 项目 | 学习价值 |
|--------|-------------|---------|
| 1 | Stanford Compilers Lab / TACO | 稀疏张量 IR、格式与代码生成 |
| 2 | Cornell / Allo | MLIR、Lowering、硬件映射 |
| 3 | UW SAMPL / TVM | 端到端张量编译与调度 |

**入门论文顺序**

1. TVM（2018）— 端到端深度学习编译与自动调度  
2. MLIR（2020）— 多层次 IR、Dialect、流水线  
3. TACO（2017）— 稀疏张量语言与代码生成  
4. Allo（2024）— 可组合加速器编程与编译  

区分两个概念：

- **AI Compiler**：为 AI 计算设计的编译器  
- **AI for Compiler**：用机器学习改进编译器优化与搜索  

企业侧公开技术栈可关注：NVIDIA（CUDA / TensorRT）、华为昇腾（CANN）、OpenXLA、以及图优化与 Kernel 自动生成相关研究。

---

## 旧 CUDA 仓库怎么用

[`CUDA_Study`](https://github.com/GinsengHoney/CUDA_Study) 是约四年前的 CUDA 学习笔记与 `.cu` 实验，对应当时的博客练习。

在本计划中它是：

- **可选题目库与对照参考**
- **不是**必须恢复、复制或维护的旧实现

可选对照主题包括：向量加计时、卷积、Global/Shared Memory 优化、原子操作等。真正推进时，优先在本仓库新建干净的 CMake 工程与测试。

---

## 第一周行动清单（W01）

| 天 | 任务 | 交付 |
|----|------|------|
| 一 | 记录可用硬件与 CUDA / 编译器环境 | `env/versions.md` |
| 二 | 选定向量加或等价实验：明确计时与正确性 | 注释 + 误差判据 |
| 三 | 跑通 CPU/GPU 对比 | 可运行命令与截图 |
| 四 | 整理为独立目录 + CMake | 最小可构建工程 |
| 五 | 边界 case、`cudaGetLastError`、同步检查 | 正确性测试通过 |
| 六 | 多组 N 做 benchmark，导出 CSV | 曲线图 + 原始数据 |
| 日 | 写 W01 日志与博客初稿 | `weekly-log/W01.md` + 草稿 |

同步完成附录中的 C++ 微实验（生命周期 / RAII / 所有权），并开始第一篇正式博客素材。

---

## 关键资料入口

| 资源 | 链接 |
|------|------|
| LearnCpp | https://www.learncpp.com/ |
| Crafting Interpreters | https://craftinginterpreters.com/ |
| LLVM Kaleidoscope | https://llvm.org/docs/tutorial/MyFirstLanguageFrontend/ |
| LLVM LangRef | https://llvm.org/docs/LangRef.html |
| MLIR Toy Tutorial | https://mlir.llvm.org/docs/Tutorials/Toy/ |
| PyTorch FX | https://docs.pytorch.org/docs/stable/fx.html |
| torch.compile | https://docs.pytorch.org/docs/stable/torch.compiler.html |
| Triton Tutorials | https://triton-lang.org/main/getting-started/tutorials/ |
| Apache TVM | https://tvm.apache.org/docs/ |
| CUDA Programming Guide | https://docs.nvidia.com/cuda/cuda-c-programming-guide/ |

---

## 声明

本计划用于形成**可验证能力与求职作品**，不承诺固定周期内获得岗位。  
机构、开源项目与招聘信息会变化；研究链接仅作继续检索入口，使用前请自行核对官网与最新论文。
