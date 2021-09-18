# Q-Learning
### General
- Classic Q-value update; different details and viewpoints
  - ![](https://ethics-of-ai.mooc.fi/cafbf143afe0e7a7325e178699ca7582/q-learning.svg)
  - ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/678cb558a9d59c33ef4810c9618baf34a9577686)
  - ![](https://miro.medium.com/max/6000/1*VItpGaVoIUnh0RUEArqSGQ.png)
  - ![](https://i.stack.imgur.com/OMzXf.png)
- DQN update; squared TD error loss function
  - ![](https://user-images.githubusercontent.com/65429130/133897695-f63debb2-1fda-4353-9569-2a6a22257abc.png)
  - ![](https://miro.medium.com/max/1176/1*ZbMDCGGQWEcgsNxInpb5gA.png)

## Double Q-Learning (& DQN)
### General
- This algorithm is an addtion to Q-learning/DQN for combatting the maximization bias, that leads to overestimating Q-values, by using to Q-functions 
### Research Papers
- [Double Q-Learning, 2010, Hado van Hasselt](https://proceedings.neurips.cc/paper/2010/file/091d584fced301b442654dd8c23b3fc9-Paper.pdf)
  - The original paper that addresses the issue, and includes mathematical proofs for a solution
### YouTube
### Articles
- [Double Q-Learning & Double DQN with Python and TensorFlow](https://rubikscode.net/2021/07/20/introduction-to-double-q-learning/ )
  - (A good background of the maximization problem, solution with Double DQN, and implementation)
  - <ins>Problem</ins>: the maximization in the TD-error update can lead to overestimation of Q-values in **stocastic environments(reward)**
  - <ins>Solution</ins>: (proposed by Hado van Hasselt in his 2010 paper, [Double Q-Learning](https://proceedings.neurips.cc/paper/2010/file/091d584fced301b442654dd8c23b3fc9-Paper.pdf)) use two sets of Q-value estimates (ie. Q-network or Q-table estimators/functions), therefore, each state-action pair now has 2 Q-value estimates.
    - With two Q-functions, QA & QB, the process for updating the present Q-values, QA(s,a), is as follows:
    - 1 find a* that maximizes QA(s',A)
    - 2 use a* to get QB(s',a*)
    - 3 use QB(s',a*) as the TD target in the the boostrapped update for QA(s,a)
    - (Repeat Q-value update for either QA or QB _at random_, for QB(s,a) do this vice versa)
    - ![](https://i2.wp.com/rubikscode.net/wp-content/uploads/2020/01/image.png?resize=492%2C52&ssl=1)
  - <ins>How?</ins>: in the paper, it is mathematically proven that the expected value for QB(s',a*) is less than or equal to the maximum value at QA(s',A) -> QA(s',a*). Therefore, through many iterations, QA(s,a) is not updated maximally and is NOT overestimated
  - The rest of this article goes into detail on the algorithm's pseudocode and Python TensorFlow implementations of double Q-learning and DQN

