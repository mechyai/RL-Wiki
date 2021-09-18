# Q-Learning

## Double DQN
### Research Papers
### Articles
- [Double Q-Learning & Double DQN with Python and TensorFlow](https://rubikscode.net/2021/07/20/introduction-to-double-q-learning/ )
  - (A good background of the maximization problem, solution with Double DQN, and implementation)
  - Problem: the maximization in the TD-error update can lead to overestimation of Q-values in stocastic environments/reward
  - Solution: (proposed by Hado van Hasselt in his 2010 paper, [Double Q-Learning](https://proceedings.neurips.cc/paper/2010/file/091d584fced301b442654dd8c23b3fc9-Paper.pdf)) use two sets of Q-value estimates (ie. Q-network or Q-table estimators/functions), therefore, each state-action pair now has 2 Q-value estimates.
    - With two Q-functions, QA & QB, the process for updating the present Q-values, QA(s,a), is as follows:
    1. find a* that maximizes QA(s',A)
    1. use a* to get QB(s',a*)
    1. use QB(s',a*) as the TD target in the the boostrapped update for QA(s,a)

