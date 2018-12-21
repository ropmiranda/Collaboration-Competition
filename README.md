[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135623-e770e354-7d12-11e8-998d-29fc74429ca2.gif "Trained Agent"

# Udacity Nanodegree "Deep Reinforcement Learning
# Project 3: Collaboration and Competition

### Introduction

For this project, we will work with the [Tennis](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#tennis) environment and solve it using RLdeep learning based models for multi-agent continuous controls and actions.

![Trained Agent][image1]

In this environment, two agents control rackets to bounce a ball over a net. If an agent hits the ball over the net, it receives a reward of +0.1.  If an agent lets a ball hit the ground or hits the ball out of bounds, it receives a reward of -0.01.  Thus, the goal of each agent is to keep the ball in play.

The observation space consists of 8 variables corresponding to the position and velocity of the ball and racket. Each agent receives its own, local observation.  Two continuous actions are available, corresponding to movement toward (or away from) the net, and jumping. 

### Solving the environment

The task is episodic, and in order to solve the environment, the agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents). Specifically,

- After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 2 (potentially different) scores. We then take the maximum of these 2 scores.
- This yields a single **score** for each episode.

The environment is considered solved, when the average (over 100 consecutive episodes) of those **scores** is at least +0.5.

### Instructions

See the main file `Tennis.ipynb` to get an introduction to the environment and follow the steps to solving the environment. The main classes are defined in the file `MADDPG_agent.py`.

### Approach and solution

The reinforcement learning approach we use in this project is called Multi Agent Deep Deterministic Policy Gradients (MADDPG). see this [paper](https://papers.nips.cc/paper/7217-multi-agent-actor-critic-for-mixed-cooperative-competitive-environments.pdf). In this model every agent itself is modeled as a Deep Deterministic Policy Gradient (DDPG) agent (see this [paper](https://arxiv.org/pdf/1509.02971.pdf)) where, however, some information is shared between the agents.

In particular, each of the agents in this model has its own actor and critic model. The actors each receive as input the individual state (observations) of the agent and output a (two-dimensional) action. The crit`ic model of each actor, however, receives the states and actions of all actors concatenated.

Throughout training the agents all use a common experience replay buffer (a set of stored previous 1-step experiences) and draw independent samples.

Details of the implementation including the neural nets to model actor and critic models can be found in the modules `MADDPG_agent.py` and `models.py` as well as the report (report.pdf`). With the current set of models and hyperparameters the environment can be solved in around 3200 steps.

## Getting Started
In order to run this code, install the following dependencies:

`pip install unityagents`

`pip install torch`

`pip install matplotlib`

`pip install numpy`

### Download the environment
For this project, you will not need to install Unity - this is because we have already built the two environments for you, and you can download it from one of the links below. You need only select the environment that matches your operating system:

Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis_Linux.zip)

Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis.app.zip)

Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis_Windows_x86.zip)

Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis_Windows_x86_64.zip)

## Executing the solution
Given that jupyter has been installed http://jupyter.org/install, execute the following command on terminal:
```shell
$ jupyter notebook
```
After Jupyter Notebook has opened, navegate to the directory `Collaboration-Competition/` and double click in Tennis.ipynb. There you can follow the instructions to execute the solution. 
