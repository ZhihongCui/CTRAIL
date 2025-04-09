# 🚗 CTrail: Trust-Aware MCTS for Cooperative Trajectory Planning

CTrail is a **trust-aware, graph-based planning framework** combining Monte Carlo Tree Search (MCTS), Reinforcement Learning, and Large Language Model (LLM)-guided scene reasoning. It is designed for complex autonomous driving scenarios involving multi-agent interaction, trust modeling, and language-guided graph construction.

---

## 📌 Abstract

Trajectory planning in dynamic environments is a paramount challenge for autonomous driving, especially in unseen environments where traditional models struggle to generalize. To address this, we propose \textsf{C-TRAIL}, a \textbf{\underline{C}}ommonsense world framework for \textbf{\underline{TRA}}jectory p\textbf{\underline{L}}anning. Inspired by how humans leverage commonsense when planning, C-TRAIL introduces a \textbf{Commonsense World} that interacts with the environment through a closed-loop three-stage process: \textbf{Recall}, \textbf{Plan}, and \textbf{Update}.



This commonsense world is implemented via three core modules. First, \textbf{Trust Commonsense Recall} module queries LLMs for high-level relations and actions, and filters through a fused trust mechanism combining commonsense trust and kinematic trust, resulting in a trust commonsense representation. Second, the \textbf{Commonsense-Guided Monte Carlo Planning} module integrates this representation into a Dirichlet-based trust policy, which guides Monte Carlo Tree Search (MCTS) for efficient and targeted trajectory exploration. Third, an \textbf{Adaptive Calibration Update} module continuously refines the trust state and planning policy using real-world feedback, ensuring consistency and adaptability over time.

To the best of our knowledge, C-TRAIL is the first to introduce a human-inspired Commonsense World into a trajectory planning loop. Experiments on the Highway-env simulator in four scenarios (i.e., \emph{highway}, \emph{merge}, \emph{intersection}, and \emph{roundabout}) show that C‑TRAIL yields average improvements over state-of-the-art baselines by 53.8\% w.r.t. ADE, 62.5\% w.r.t. FDE, and 35.8\% w.r.t. SR in seen environments, and 42.5\% w.r.t. ADE, 52.2\% w.r.t. FDE, and 27.1\% w.r.t. SR in unseen environments, respectively. Additionally, case studies show that C-TRAIL generates safe and smooth trajectories, underscoring its effectiveness and real-world potential.



---

## 📂 Project Structure

```bash
CTrail/
├── data/                          # Data files
├── exper_figure/                 # Visualizations
│   ├── hyperexperiment/
│   └── hyperparameter.py         # Hyperparameter visualization
├── mcts/                         # MCTS + planning modules
│   ├── mcts_with_prior.py        # Core MCTS with prior knowledge
│   ├── ObservationGraphBuilder.py# Build observation graphs from environments
│   ├── PolicyAdapter.py          # Policy wrapper for planning
│   ├── TrustGraphPlanner.py      # Trust-graph-based trajectory planner
│   └── TrustModel.py             # Trust estimation model
├── ppo_logs/                     # PPO training logs
├── results/                      # Output results
├── scenario/                     # Prompt, trust, and encoder definitions
│   ├── Encoder.py                # Transformer encoder for graphs
│   ├── Prompt.py                 # Prompt construction for language models
│   ├── Trust_commonse_graph.py  # Common-sense trust graph generation
│   └── Trust.py                  # Trust modeling and updates
├── utils/                        # Utilities and test environments
│   ├── agent_propmt.py           # Agent-specific prompt logic
│   ├── data_gather.py            # Data collection scripts
│   ├── test_intersection.py      # Intersection scenario test
│   ├── test_merge.py             # Merging scenario test
│   └── test_rounabout.py         # Roundabout scenario test
├── videos/                       # Rendered simulation videos
├── config.yaml                   # Configuration file
├── license.txt                   # License
├── run_CTRAIL.py                 # 🚀 Main entry point
└── README.md                     # You are here
