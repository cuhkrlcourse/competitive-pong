<img align=right width=300px  src="resources/repo-cover-large.gif" />

# cPong Environment

Competitive Pong (cPong) environment extends the classic Atari Game Pong into a competitive environment, where both side can be trainable agents. It facilitates many exploratory topics such as self-play and population-based training, as well as fun applications such as hosting Pong tournament for a group of users.  In the environment, beside the original rule-based agent to be plugged in, we also provide some pretrained agents from different RL algorithms at various difficulty levels. 

## Installation

```bash
git clone https://github.com/cuhkrlcourse/competitive-pong.git
cd competitive-pong
pip install -e .  # Install the package in-place
```

## Usage

Create the environment after registration:

```python
import gym
import competitive_pong

competitive_pong.register_tournament_envs()

env_single = gym.make("cPong-v0")

env_single.observation_space  # Box(210, 160, 3)
env_single.action_space  # Discrete(3)

env_double = gym.make("cPongDouble-v0")

env_double.observation_space  # Tuple(Box(210, 160, 3), Box(210, 160, 3))
env_double.action_space  # Tuple(Discrete(3), Discrete(3))
```

Action 0 represents "moving the left bat up", 1 for "no operation" and 2 for "moving the left bat down".

In `cPongDouble-v0` environment, both agents receive observations shows that they are controlling the left bat. Namely the observation for second agent (the right-side agent) is mirrored. This design guarantees the agent trained by playing with rule-based agent controlling the left bat can smoothly be evaluated with other agents, even when it controls the right-side bat in reality.

## Visualize builtin agents

We provide a set of trained agents to serve as opponents. We prepared 6 level builtin agents, including:

1. `RANDOM` - A random agent
2. `RULE_BASED` - Rule-based agent that serves as the right-side agent in `cPong-v0`
3. `WEAK` - Weak-level agent with a smaller neural network than yours
4. `MEDIUM` - Medium-level agent with a small neural network
5. `STRONG` - Strong-level agent with a large neural network as yours
6. `ALPHA_PONG` - Boss-level agent that is well trained and may hard to beat down, use a large neural network as yours

You can visualize the performance of arbitrary builtin agents and let them play against each other. Run the script:

```bash
# RULE_BASED agent VS RULE_BASED agent
python vis.py

# ALPHA_PONG agent vs STRONG agent
python vis.py --left ALPHA_PONG --right STRONG --num-episodes 3
```
## Acknowledgement

This environment was originally developed by Belly Ho and Joe Lam, undergraduate students at CUHK, as their Final Year Project (FYP) with Prof. Zhou Bolei. It won the best FYP award in the department. Peng Zhenghao further wrapped up the environment as a part of the assignment in the reinforcement learning course. 


