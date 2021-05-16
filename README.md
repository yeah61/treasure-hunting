# Treasure-hunting

  EECS738 (Spring 2021) assignment 4

  Author: Ye Wang

## Purpose

The purpose of this project is to understand the reinforcement learning. utilize the reinforcement learning to find a best solution all by itself.


## Map

__State space:__ the map has 10x10 = 100 distinct states. The start state is the top left cell. 

　The underscores ' _ ' stand for trees and cannot be moved to.
  
　The * represents the agent.
  
　The + is for the treasure.
  
　The - stands for the monster


__Actions:__ The agent can choose from up to 4 actions (left, right, up, down) to move around.

__Environment Dynamics:__ the map is deterministic, leading to the same new state given each state and action

__Rewards:__ The agent receives +1 reward when it gets the treasure (the one that shows R 1.0), and -1 reward when it meets monsters (R -1.0 is shown for these). 
The state with +1.0 reward is the goal state and resets the agent back to start.



## Algorithm

The action of the agent is a deterministic, finite Markov Decision Process (MDP). Assume the discount factor β=0.9.

We will implement the Q-learning algorithm to learn the Q values for each state-action pair. Assume a small fixed learning rate α=0.01.

We also experiment with different explore/exploit policies:


• ε -greedy (exploit, but once in a while do something random)

> • choose machine with current best expected reward with probability 1-ε

> • choose another machine (action) randomly with probability ε / (N-1)

• Boltzmann exploration (choose probabilistically relative to expected rewards)

> • choose machine k with probability ~ exp(-P(s_k)/T)

> • decrease T (temperature) over time

>   　　-high T: nearly equiprobable (exploration)

>   　　-low T: increasingly biased toward best action (exploitation)


## Approach

(1) The creat_world function create the map and deicde the distributions of the trees, monsters, and treasure. we can change the positions manually. but the start position of the agent is fixed at (0,0).

(2) The q_matrix (q_table) is created and refreshed by the Q-learning algorithm. and it is a simple lookup table where we calculate the maximum expected future rewards for action at each state. Basically, this table will guide us to the best action at each state.

(3) class _EpsilonGreedyPolicy_ and class _BoltzmannExplorationPolicy_ are used to realize the algorithms respectively. and _create_epsilon_greedy_policy_ and  _create_boltzmann_policy_ are used to create an instance of each policy. 

In summary, we will create a map with monsters, trees and a treasure, and then the agent will use ε -greedy and Boltzmann exploration to update the q_table of the Qlearning in every episode. Finally, the agent can choose the best way to the treasure according to the final convergent q_table. 

## Results
(1) The reward map is shown as below. the 1 stands for the treasure, -1 stands for the monster and _ stands for the trees.

![Alt text](https://github.com/yeah61/treasure-hunting/blob/main/images/world%20map.png)

(2) We tested different parameters of the two policy. For the ε -greedy, ε =0.1, 0.2, 0.3, respectively. For Boltzmann exploration, temperature decreases to as the sequence of 2000, 1000, 100, 10, 1. 

![Alt text](https://github.com/yeah61/treasure-hunting/blob/main/images/Qlearning%20approach.png)

As we can see, the larger the ε is, the more time and iterations the trainning approach needs. Because a larger ε means more random actions the agent will take to make sure the whole map is explored.

Meanwile, the higher of the temperature, the Boltzmann exploration takes more time to explore the map. As the temperature decrease, it take much less time to exploit the learned knowledge.

(3) After training, we provide a menu to observe different results.

![Alt text](https://github.com/yeah61/treasure-hunting/blob/main/images/menu.png)

For example, with command q, the final q_table is stored in the data.csv which is in the same folder with the main.py.

with command p, we can see the final route that the agent choose for the treasure. The left is the final route for the treasure in (5,5) and the right is the final route for the treasure in (8,8)

![Alt text](https://github.com/yeah61/treasure-hunting/blob/main/images/final%20path.png) ![Alt text](https://github.com/yeah61/treasure-hunting/blob/main/images/99.png)


## Acknowledgement

Through this project, I get a basic understanding of the neural network. But there is still a long way to utilize the neural network model to do more complex tasks.
such as the image classification in this repository. I made a lot of references to this article: 
https://www.cnblogs.com/further-further-further/p/10430073.html. I am looking forward to further study and practice to get a better understanding of the neutral network.
