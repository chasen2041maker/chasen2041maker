<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <img src="assets/banner-light.svg" alt="Yong Li: evaluation and verification for AI systems" width="100%">
</picture>

## Hi, I'm Yong Li

I studied bioengineering as an undergrad, then did a master's in artificial intelligence at UNSW Sydney, and now write backend services and AI agents for a living. In my spare time I'm teaching myself autonomous driving by building it: I write each module of a driving stack myself, run it closed-loop in the CARLA simulator, and measure where it goes wrong.

我本科读的是生物工程，之后在悉尼 UNSW 读完人工智能硕士，现在的工作是写后端和 AI Agent。业余时间我在自学自动驾驶，办法是自己动手搭：驾驶系统的每个模块自己写，放进 CARLA 仿真器里闭环跑，再把它出错的地方量出来。

Most of my projects come back to one question: how would I know this result is right?

我的项目最后几乎都绕回同一个问题：怎么证明这个结果是对的。

## What I'm working on · 最近在做

- **Oct 2026 · Multi-object tracking (in progress).** LiDAR tells me how far the car ahead is, about ±0.2 m each frame, but not how fast it's going. Taking the difference of two frames was off by up to 5.5 m/s, so I'm writing a Kalman filter to get a speed the planner can trust.

  **2026-10 · 多目标跟踪（进行中）。** 激光雷达每帧告诉我前车多远（误差约 ±0.2 米），但不告诉我它开多快。直接拿相邻两帧相减，速度最多差 5.5 m/s。我在写卡尔曼滤波，算出规划能放心用的车速。

- **Oct 2026 · Ground removal on a slope.** Cutting the ground at a fixed height works on flat roads. On a 4% upgrade it labelled 3,371 road points as obstacles, which looks like a wall 5 m ahead. Fitting the ground plane with RANSAC brought that to 0.

  **2026-10 · 坡道上去地面。** 按固定高度切地面，平路上没问题；到了 4% 的上坡，3371 个路面点被当成障碍物，相当于前方 5 米立了一堵墙。用 RANSAC 拟合出地面再切，降到 0 个。

- **Oct 2026 · CI for highway-sim-eval.** The very first run failed: I had forgotten scikit-learn in `requirements.txt` because it was already installed on my laptop. That is exactly the kind of mistake CI is there to catch.

  **2026-10 · 给 highway-sim-eval 加上 CI。** 第一次跑就红了：`requirements.txt` 里漏了 scikit-learn，我自己电脑上早就装过，所以一直没发现。这正是 CI 要抓的问题。

## Projects · 项目

### Autonomous driving · 自动驾驶

<table>
<tr>
<td width="50%" valign="top">
<h3><a href="https://github.com/chasen2041maker/highway-sim-eval">highway-sim-eval</a></h3>
<p>My main project. A driving stack written from scratch (vehicle model, PID, Pure Pursuit, IDM car following, a LiDAR pipeline, now tracking), run closed-loop in CARLA 0.9.16 with an evaluation layer on top.</p>
<p>我的主项目：从零写的驾驶系统（车辆模型、PID、Pure Pursuit、IDM 跟车、激光雷达感知，现在在做跟踪），在 CARLA 0.9.16 里闭环跑，上面再搭一层评测。</p>
<p>Favourite finding so far: the LiDAR box for the car ahead is 2.30 m short, because only its rear face is visible, and no clustering setting fixes it.<br>
目前最有意思的发现：前车的激光雷达框中心比真实位置近了 2.30 米，因为雷达只看得到车尾，怎么调聚类参数都没用。</p>
<p><a href="https://chasen2041maker.github.io/highway-sim-eval/">Interactive explainers · 交互动画讲解</a> · 54 tests on CI</p>
</td>
<td width="50%" valign="top">
<h3><a href="https://github.com/chasen2041maker/Bev">Bev</a></h3>
<p>A course I'm writing for myself on BEV perception: 19 lessons from the pinhole camera to end-to-end driving, each with an animation and code I write by hand.</p>
<p>写给自己的 BEV 感知课程：19 课，从针孔相机一路到端到端，每课一个动画、核心代码自己写。</p>
<p>Paused for now while I finish the simulation work. It will pick up again on camera perception.<br>
目前暂停，先把仿真这条线做完，之后从相机感知接着学。</p>
</td>
</tr>
</table>

### AI agents · AI Agent

<table>
<tr>
<td width="50%" valign="top">
<h3><a href="https://github.com/chasen2041maker/GroundGuard">GroundGuard</a></h3>
<p>Checks every number in an agent's answer against the tool results from the same run, without asking another LLM to judge. On a 200-case bilingual test set it flagged all 71 cases that should fail, with 0 false alarms. On <a href="https://pypi.org/project/groundguard-ai/">PyPI</a>.</p>
<p>逐个核对 Agent 回答里的数字，必须对得上同一次运行里工具返回的结果，不靠另一个大模型当裁判。200 条中英文测试里，71 条应该被拦下的全部拦下，0 误报。</p>
</td>
<td width="50%" valign="top">
<h3><a href="https://github.com/chasen2041maker/AgentTrust-Runtime">AgentTrust-Runtime</a></h3>
<p>Policies, human approvals and a tamper-evident log around an agent's tool calls. If a rule can't be checked, the call is blocked rather than allowed.</p>
<p>给 Agent 的工具调用加上规则、人工审批和防篡改的证据记录；规则查不了的时候，默认拦下，而不是放行。</p>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h3><a href="https://github.com/chasen2041maker/BidRadar">BidRadar</a></h3>
<p>A research agent for public tenders. Every conclusion has to quote its source text; anything it can't confirm stays marked "to verify".</p>
<p>做招投标调研的 Agent：每条结论都要引用原文，确认不了的就标“待核实”。</p>
</td>
<td width="50%" valign="top">
<h3><a href="https://github.com/chasen2041maker/research-forge">research-forge</a></h3>
<p>Turns a research idea into an experiment anyone can rerun: the paper, code version, container and metrics are pinned, and a result counts only when they all match.</p>
<p>把研究想法变成别人也能重跑的实验：论文、代码版本、容器、指标都固定下来，全部对得上才算结果。</p>
</td>
</tr>
</table>

## How I work · 我的习惯

- I write the core algorithms myself, and the numbers in my tests are worked out by hand first.
  核心算法自己写，测试里的数字先手算一遍。
- If I can't draw it, I don't understand it yet. Most experiments come with an interactive animation.
  画不出来就说明还没懂，所以大部分实验都配了交互动画。
- Every number in a README points to the script that produced it.
  README 里的每个数字，都能找到算出它的那段脚本。

## Get in touch · 联系我

I'm looking for roles in autonomous-driving simulation, evaluation, or data closed-loop platforms in 2027 (Shanghai or Hangzhou). Email: chasen2041@gmail.com

2027 年在看自动驾驶仿真、评测、数据闭环平台方向的机会（上海、杭州）。邮箱：chasen2041@gmail.com
