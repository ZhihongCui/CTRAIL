# 🚗 CTRAIL:A  Commonsense World Framework for Trajectory Planning in Autonomous Driving


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

## 📄 Data Format

Each `.json` file in `data/*-v0/` directories defines a simulation scenario with specific lane and traffic density settings.

**Filename format:**

<scenario>-v0_lane_<num_lanes>density<traffic_density>.json

- `<scenario>`: One of `intersection`, `merge`, `roundabout`
- `<num_lanes>`: Number of lanes in the environment (e.g., 3)
- `<traffic_density>`: Density of vehicles (e.g., 1.0, 1.5, 2.0, etc.)

**Example:**

merge-v0_lane_3_density_2.5.json → A merging scenario with 3 lanes and vehicle density of 2.5

## ⚙️ Configuration Format

############ Large language model config ############
OPENAI_API_TYPE: 'openai' # 'openai' or 'azure'
# below are for Openai
OPENAI_KEY: your own key
OPENAI_CHAT_MODEL: 'gpt-3.5-turbo' # 'gpt-4-1106-preview' # Alternative models: 'gpt-3.5-turbo-16k-0613' (note: performance may vary)
# below are for Azure OAI service
AZURE_API_BASE: # https://xxxxxxx.openai.azure.com/
AZURE_API_VERSION: "2023-07-01-preview"
AZURE_API_KEY: #'xxxxxxx'
AZURE_CHAT_DEPLOY_NAME: # chat model deployment name
AZURE_EMBED_DEPLOY_NAME: # text embed model deployment name  

############### Settings ############
reflection_module: False # True or False
few_shot_num: 3 # 0 for zero-shot
episodes_num: 2 # run episodes
# memory_path: 'memories/20_mem'
result_folder: 'results'

############ Highway-env config ############
simulation_duration: 20 # step
vehicle_count: 20
other_vehicle_type: "highway_env.vehicle.behavior.IDMVehicle" #other types are: "highway_env.vehicle.behavior.DefensiveVehicle" or "highway_env.vehicle.behavior.AggressiveVehicle"
vehicles_density: 2.0
