# Q-Learning
### General
- **Bellman Equation** for Q-Learning
  - This recursive relation for the Q-value of a state-action pair is what the classical Q-learning and DQN Q-function algorithms are trying to learn, through boostrapping and temporal difference learning. Once the Q-function is sufficiently learned, the agent can act optimally by selecting actions with the maximal Q-value for each state.
  - <img src="https://miro.medium.com/max/1400/1*lTVHyzT3d26Bd_znaKaylQ.png" width="50%" height="50%">
- <ins>Classic Q-value update</ins>
  - This algorithm is useful for discrete state/action environments, with low dimensionality, and off-policy and online or offline implementations.
  - (below, different details and viewpoints of the same learning update) 
  - <img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/678cb558a9d59c33ef4810c9618baf34a9577686" width="75%" height="75%">
  - <img src="https://miro.medium.com/max/6000/1*VItpGaVoIUnh0RUEArqSGQ.png" width="75%" height="75%">
  - <img src="https://i.stack.imgur.com/OMzXf.png" width="75%" height="75%">
  - <img src="https://miro.medium.com/max/1838/1*7AWfjw8YDfoRqnIO71DjiA.png" width="75%" height="75%">
- <ins>DQN update</ins>
  - Below, squared TD error is the loss function using target (static) and policy (learned) network to push the network towards satisfying the Bellman Equation
  - Two Q-networks are used to help the optimization avoid "chasing its own tail". If only 1 network is used, every update to Q(s,a) (comptuted with Qmax(s',A)) will update Qmax(s',A) further away from satisfying the Bellman Equation.
  - If we have a network that we hold static (Target Network) for X episodes and use it to calculate Q(s',a*), our optimization has stationary points to optimize for. Then, every X episodes, we will update the Target Network with the parameters of the current learned Policy Network.
  - In further sections below, we will add improvements to this vanilla DQN framework. 
  - <img src="https://user-images.githubusercontent.com/65429130/133897695-f63debb2-1fda-4353-9569-2a6a22257abc.png" width="30%" height="30%">
  - ![](https://miro.medium.com/max/1176/1*ZbMDCGGQWEcgsNxInpb5gA.png)

## Table of Contents 
### Deep Q-Learning Components
1. Experience Replay, Fixed Q-targets - [__Playing Atari with Deep Reinforcement Learning__](https://arxiv.org/abs/1312.5602) (Mnih et.al, 2013, DeepMind)
1. Prioritized Experience Replay - [__Prioritzed Experience Replay__](https://arxiv.org/abs/1511.05952) (Schaul et .al, 2015, DeepMind)
2. [Double DQN](#double-q-learning--dqn) - [__Deep Reinforcement Learning with Double Q-Learning__](https://arxiv.org/abs/1509.06461) (van Hasselt et. al, 2015, DeepMind)
3. Dueling DQN - [__Dueling Network Achitectures for Deep Reinforcement Learning__](https://arxiv.org/abs/1511.06581) (Wang et. al, 2016, DeepMind)
4. Reccurent DQN for POMDPs - [__Deep Recurrent Q-Learning for Partially Observable MDPs__](https://arxiv.org/abs/1507.06527) (Hausknecht et. al, 2017)
5. Branching DQN - [__Action Branching Architectures for Deep Reinforcement Learning__](https://arxiv.org/abs/1711.08946) (Tavakoli et. al, 2019)
- (more...)


## Double Q-Learning (& DQN)
### General
- This algorithm is an addtion to Q-learning/DQN for combatting the maximization bias, that leads to overestimating Q-values, by using to Q-functions
- <ins>Problem</ins>: the maximization in the TD-error update can lead to overestimation of Q-values in **stocastic environments(reward)**
  - <ins>Solution</ins>: (proposed by Hado van Hasselt in his 2010 paper, [Double Q-Learning](https://proceedings.neurips.cc/paper/2010/file/091d584fced301b442654dd8c23b3fc9-Paper.pdf)) use two sets of Q-value estimates (ie. Q-network or Q-table estimators/functions), therefore, each state-action pair now has 2 Q-value estimates.
    - With two Q-functions, QA & QB, the process for updating the present Q-values, QA(s,a), is as follows:
    - 1 find a* that maximizes QA(s',A)
    - 2 use a* to get QB(s',a*)
    - 3 use QB(s',a*) as the TD target in the the boostrapped update for QA(s,a)
    - (Repeat Q-value update for either QA or QB _at random_, for QB(s,a) do this vice versa)
    - ![](https://i2.wp.com/rubikscode.net/wp-content/uploads/2020/01/image.png?resize=492%2C52&ssl=1)
    - ![](https://miro.medium.com/max/534/1*NvvRn59pz-D1iSkBWpuIxA.png)
  - <ins>How?</ins>: in the paper, it is mathematically proven that the expected value for QB(s',a*) is less than or equal to the maximum value at QA(s',A) -> QA(s',a*). Therefore, through many iterations, QA(s,a) is not updated maximally and is NOT overestimated
  - <ins>Solution [DQN]</ins>: 
### Research Papers
- [Double Q-Learning, 2010, Hado van Hasselt](https://proceedings.neurips.cc/paper/2010/file/091d584fced301b442654dd8c23b3fc9-Paper.pdf)
  - The original paper that addresses the issue, and includes mathematical proofs for a solution
### YouTube
  - [Increasing Training Stability with Double DQNs](https://www.youtube.com/watch?v=ILDLT97FsNM&t=398s) by TheComputerScientist
### Articles
- [Double Q-Learning & Double DQN with Python and TensorFlow](https://rubikscode.net/2021/07/20/introduction-to-double-q-learning/ )
  - A good background of the maximization problem, solution with Double DQN, and implementation
  - The rest of this article goes into detail on the algorithm's pseudocode and Python TensorFlow implementations of double Q-learning and DQN

## Dueling DQN
### General
### Research Papers
### YouTube
### Articles
