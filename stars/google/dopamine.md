---
project: dopamine
stars: 10817
description: Dopamine is a research framework for fast prototyping of reinforcement learning algorithms. 
url: https://github.com/google/dopamine
---

Dopamine
========

Getting Started | Docs | Baseline Results | Changelist

  
  

Dopamine is a research framework for fast prototyping of reinforcement learning algorithms. It aims to fill the need for a small, easily grokked codebase in which users can freely experiment with wild ideas (speculative research).

Our design principles are:

-   _Easy experimentation_: Make it easy for new users to run benchmark experiments.
-   _Flexible development_: Make it easy for new users to try out research ideas.
-   _Compact and reliable_: Provide implementations for a few, battle-tested algorithms.
-   _Reproducible_: Facilitate reproducibility in results. In particular, our setup follows the recommendations given by Machado et al. (2018).

Dopamine supports the following agents, implemented with jax:

-   DQN (Mnih et al., 2015)
-   C51 (Bellemare et al., 2017)
-   Rainbow (Hessel et al., 2018)
-   IQN (Dabney et al., 2018)
-   SAC (Haarnoja et al., 2018)
-   PPO (Schulman et al., 2017)

For more information on the available agents, see the docs.

Many of these agents also have a tensorflow (legacy) implementation, though newly added agents are likely to be jax-only.

This is not an official Google product.

Getting Started
---------------

We provide docker containers for using Dopamine. Instructions can be found here.

Alternatively, Dopamine can be installed from source (preferred) or installed with pip. For either of these methods, continue reading at prerequisites.

### Prerequisites

Dopamine supports Atari environments and Mujoco environments. Install the environments you intend to use before you install Dopamine:

**Atari**

1.  These should now come packaged with ale\_py.
2.  You may need to manually run some steps to properly install `baselines`, see instructions.

**Mujoco**

1.  Install Mujoco and get a license here.
2.  Run `pip install mujoco-py` (we recommend using a virtual environment).

### Installing from Source

The most common way to use Dopamine is to install it from source and modify the source code directly:

```
git clone https://github.com/google/dopamine
```

After cloning, install dependencies:

```
pip install -r dopamine/requirements.txt
```

Dopamine supports tensorflow (legacy) and jax (actively maintained) agents. View the Tensorflow documentation for more information on installing tensorflow.

Note: We recommend using a virtual environment when working with Dopamine.

### Installing with Pip

Note: We strongly recommend installing from source for most users.

Installing with pip is simple, but Dopamine is designed to be modified directly. We recommend installing from source for writing your own experiments.

```
pip install dopamine-rl
```

### Running tests

You can test whether the installation was successful by running the following from the dopamine root directory.

```
export PYTHONPATH=$PYTHONPATH:$PWD
python -m tests.dopamine.atari_init_test
```

Next Steps
----------

View the docs for more information on training agents.

We supply baselines for each Dopamine agent.

We also provide a set of Colaboratory notebooks which demonstrate how to use Dopamine.

References
----------

Bellemare et al., _The Arcade Learning Environment: An evaluation platform for general agents_. Journal of Artificial Intelligence Research, 2013.

Machado et al., _Revisiting the Arcade Learning Environment: Evaluation Protocols and Open Problems for General Agents_, Journal of Artificial Intelligence Research, 2018.

Hessel et al., _Rainbow: Combining Improvements in Deep Reinforcement Learning_. Proceedings of the AAAI Conference on Artificial Intelligence, 2018.

Mnih et al., _Human-level Control through Deep Reinforcement Learning_. Nature, 2015.

Schaul et al., _Prioritized Experience Replay_. Proceedings of the International Conference on Learning Representations, 2016.

Haarnoja et al., _Soft Actor-Critic Algorithms and Applications_, arXiv preprint arXiv:1812.05905, 2018.

Schulman et al., _Proximal Policy Optimization Algorithms_.

Giving credit
-------------

If you use Dopamine in your work, we ask that you cite our white paper. Here is an example BibTeX entry:

```
@article{castro18dopamine,
  author    = {Pablo Samuel Castro and
               Subhodeep Moitra and
               Carles Gelada and
               Saurabh Kumar and
               Marc G. Bellemare},
  title     = {Dopamine: {A} {R}esearch {F}ramework for {D}eep {R}einforcement {L}earning},
  year      = {2018},
  url       = {http://arxiv.org/abs/1812.06110},
  archivePrefix = {arXiv}
}
```
