C-TRAIL: A Commonsense World Framework for Trajectory Planning in Autonomous Driving



CTrail/
├── data/                          # Data files
├── exper_figure/                 # Experimental results visualization
│   ├── hyperexperiment/
│   └── hyperparameter.py         # Hyperparameter visualization
├── mcts/                         # MCTS and planning modules
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
│   ├── test.py                   # Intersection scenario test
├── videos/                       # Rendered simulation videos
├── config.yaml                   # Configuration file
├── license.txt                   # License
└── run_CTRAIL.py                 # Main script to launch the framework
