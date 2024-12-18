### Dynamic pricing strategy using reinforcement learning

The goal is to frame and solve a dynamic pricing problem using two exploration/exploitation strategies. The basic workflow is:

1. Train a Supervised Learning (SL) model on the Environment: Use the two provided datasets to train a SL to predict utilization based on: {'Start Day of the Week', 'Start Month', 'Start Hour', 'Car ID Hash', 'Car Parking Address Postcode', 'Trip Price', 'Hours Duration', 'Booking Advance Hours Duration', and 'Price to Average Price Per Postcode'} features. This model outputs a prediction of utilization rates for different pricing scenarios, which the RL agent can use to predict revenue outcomes. 

2. Setup the Reinforcement Learning (RL) environment: The environment encapsulates the state of the car rental market (based on environmental features) and provides feedback (rewards) to the RL agent based on the actions it takes (i.e., setting prices). The state all features mentioned in section 1, except for Trip Price. The rewards are calculated based on the utilization rate predicted by the environmental supervised model and the price set by the agent, essentially reward = price * predicted utilization.

3. Implement the RL Agent: The RL agent uses strategies A/B/N and ε-greedy to explore different pricing actions and learn which strategies yield the highest rewards. Over time, the agent learns the agent learns to optimize its choices that maximize its rewards.

### Output
Pricing policy given the simulated environment
1.	A/B/N Strategy
  a.	100% random exploration between the prices of $10-$150 in multiples of $10.
  b.	Achieved a cumulative reward of $5,349,205.34
  c.	Model training time of 75.76 Minutes
2.	ε-greedy Strategy
  a.	90% exploitation / 10% exploration split, both between the prices of $10-$150 in multiples of $10.
    i.	Exploration method: Identical to A/B/N.
    ii.	Exploitation method: Created linear regression supervised learning model of agent’s acquired data, made predictions of all candidate prices, and chose optimal price to maximize current reward.
  b.	Achieved a cumulative reward of $11,314,715.16
  c.	Model training time of 414.81 minutes
3.	Key Tradeoff
  a.	A/B/N: More practical for quicker implementation and lower computational load, but sacrifices cumulative reward relative to ε-greedy.
  b.	ε-greedy: Leads to a higher cumulative reward, but suffers from a higher computational cost due to the more sophisticated optimization methods. 
  c.	Both approaches proved viable in the simulated environment

