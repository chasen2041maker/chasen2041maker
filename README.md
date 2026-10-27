<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.gif">
  <img src="assets/banner-light.gif" alt="Animation from highway-sim-eval in three scenes: a simulated LiDAR sweep turned into object boxes (ground removal, DBSCAN); a Kalman multi-object tracker keeping IDs through an occlusion and dropping a ghost track; a MOBIL decision and a quintic lane change in the Frenet frame, followed with Pure Pursuit" width="100%">
</picture>

<p align="right"><i>See → track → drive: every frame computed by the code in <a href="https://github.com/chasen2041maker/highway-sim-eval">highway-sim-eval</a>.</i></p>

<details>
<summary><b>中文版：点这里展开</b></summary>

## 你好，我是 Yong Li

后端和 AI Agent 工程师，悉尼 UNSW 人工智能硕士（本科生物工程）。业余时间从零写一套自动驾驶系统，放进 CARLA 仿真器里测。顶部的动图是这个项目的代码一帧一帧算出来的：雷达扫一圈、分出物体（SEE）→ 多车跟踪，被挡住也不丢编号（TRACK）→ 判断能不能变道、画曲线、跟着开过去（DRIVE）。

### 最近在做

- **2026-10** · 变道：MOBIL 决定要不要变，五次多项式画曲线，在 Frenet 坐标里规划。90° 弯道里，直接给地图 y 加偏移的那辆车终点又回到了本车道（差 3.50 米），Frenet 那辆正好在左车道中间。
- **2026-10** · 多目标跟踪：卡尔曼滤波 + 匈牙利匹配 + 编号管理，自己手写，并对着真值打分；又用 C++ 重写了一遍（CMake + googletest），整段逐帧和 Python 版一致。车被挡住 0.5 秒，轨迹最多等 10 帧时编号不变，只等 3 帧就会换成新编号；但等得久，护栏一次误检留下的鬼影也多活 7 帧（11 vs 4）。相邻两帧相减算前车车速最多差 5.5 m/s，卡尔曼滤波最多差 0.35 m/s。
- **2026-10** · 4% 上坡上去地面：固定高度切出 3371 个假障碍物，RANSAC 拟合地面后为 0。

### 项目

- **[highway-sim-eval](https://github.com/chasen2041maker/highway-sim-eval)** · 从零写的驾驶系统（控制、跟车、激光雷达感知、跟踪），在 CARLA 0.9.16 里闭环测。80 个测试，每次 push 自动跑 · [交互动画讲解](https://chasen2041maker.github.io/highway-sim-eval/)
- **[Bev](https://github.com/chasen2041maker/Bev)** · 写给自己的 BEV 感知课程，19 课，目前暂停。
- AI Agent 方向的项目（GroundGuard、AgentTrust-Runtime、BidRadar、research-forge）在下面的置顶里。

### 联系

2027 年在看自动驾驶仿真、评测、数据平台方向的岗位（上海、杭州）。chasen2041@gmail.com

</details>

## Hi, I'm Yong Li

Backend and AI-agent engineer with a master's in AI from UNSW Sydney (bioengineering before that). In my spare time I'm building an autonomous-driving stack from scratch and testing it in the CARLA simulator.

### Now

- **Oct 2026** · Lane change: MOBIL decides, a quintic curve shapes it, planned in the Frenet frame. In a 90° curve, the car that added the offset to map y ended back in its own lane (3.50 m off); the Frenet car ended in the centre of the left lane.
- **Oct 2026** · Multi-object tracking: Kalman filter + Hungarian matching + track IDs, hand-written and scored against ground truth, then ported to C++ (CMake + googletest), matching the Python version frame by frame. A car hidden for 0.5 s keeps its ID if tracks wait 10 frames; with 3 frames it comes back under a new one. Waiting longer also keeps a one-frame guardrail ghost alive for 11 frames instead of 4. Two-frame differencing got the lead car's speed wrong by up to 5.5 m/s; the Kalman filter, by at most 0.35 m/s.
- **Oct 2026** · Ground removal on a 4% slope: a fixed height cut made 3,371 false obstacles; a RANSAC ground plane made 0.

### Projects

- **[highway-sim-eval](https://github.com/chasen2041maker/highway-sim-eval)** · Driving stack written from scratch (control, car following, LiDAR perception, tracking), run closed-loop in CARLA 0.9.16. 80 tests on CI · [interactive explainers](https://chasen2041maker.github.io/highway-sim-eval/)
- **[Bev](https://github.com/chasen2041maker/Bev)** · A 19-lesson BEV perception course I'm writing for myself. Paused for now.
- My AI-agent projects (GroundGuard, AgentTrust-Runtime, BidRadar, research-forge) are pinned below.

### Contact

Looking for autonomous-driving simulation, evaluation or data-platform roles in 2027 (Shanghai or Hangzhou). chasen2041@gmail.com
